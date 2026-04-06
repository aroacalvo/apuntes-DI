# Kontenedoreak

## Sistema eragilea

Bi osagai/geruza nagusi:

- Kernela (the central part of the OS that controls hardware and allows programs to run)
  - Prozesuen kontrol eta kudeaketa
  - Memoria kudeaketa
  - I/O (irteera/sarrera) kudeaketa
- Erabiltzaile espazioa/geruza (where user applications run. principalmente librerías que ofrece el OS, nos dejan interacuar con el kernel usandno syscall)
  - Libreria estatikoak eta dinamikoak
  - Aplikazioak

## OS vs VM vs LX

Aplikazio bat non instalatzen den arabera:

| Feature        | Direct OS | Virtual Machine | Container            |
| -------------- | --------- | --------------- | -------------------- |
| Isolation      | ❌ Low    | ✅ High         | ⚠️ Medium            |
| Performance    | ✅ Best   | ❌ Lower        | ✅ Near-native       |
| Resource usage | ✅ Low    | ❌ High         | ✅ Low               |
| Portability    | ❌ Low    | ⚠️ Medium       | ✅ High              |
| OS included    | ❌ No     | ✅ Yes          | ❌ No (shares kernel)|

## Kontenedoreen oinarriak

1. Zerk osatzen du kontenedore irudi bat?
   - Interesatzen zaizkigun aplikazioek
   - Aplikazio hauek behar dituzten libreriak
2. Martxan dagoenean, zer da kontenedore instantzia bat?
   - A container instance is a running container created from a container image
     - Image → static blueprint (like a template)
     - Instance (container) → live, running version of that image
   - Instantzia bakoitza independientea da (prozesu, sare, memoria etc. propiak ditu)
3. Zein kernel ezaugarrik ahalbidetzen dituzte kontenedoreak?
   - cgroups -> resource control (limit and monitor CPU, memory...)
   - namespaces -> procesos, red, file system
   - capabilities -> break root privileges into smaller pieces, containers get only what they need
   - syscalls / seccomp-bpf
     - syscall: the interface that allows applications (in user space) to request services from the kernel.
     - seccomp-bpf: security mechanism that filters and restricts which syscalls a container can use, reducing the attack surface
   - chroot -> isolates a process by limiting its view of the filesystem
   - copy-on-write -> shares data between containers and only copies it when changes are made

## OCI

Kontenedoreak nola sortzen, exekutatzen eta gordetzen diren espezifikatzen duen estandarra.

## Aplikazio/Sistema kontenedoreak

Bi kontenedore mota hauek kernelaren ezaugarri berdinetan oinarritzen dira (aurretikan aipatutakoak).

**Aplikazio kontenedoreak**:
Apikazio edo zerbitzu bakarra exekutatzeko diseinatuta.

![kontenedoreak1](kontenedoreak1.png)

**Sistema kontenedoreak**:
Sistema operatibo oso bat bezala funtzionatzeko diseinatutako kontenedoreak.

![kontenedoreak2](kontenedoreak2.png)

## Kernel ezaugarriak

### Control groups

Linux kernel feature used to limit, prioritize, and monitor the resources that processes (or containers) can use.

- Prozesuak -> kudeatu, mugatu, ikusi
- kontrolatutako errekurtsoak -> CPU, memoria, I/O, sarea
- Bi bertsioak daude, gaur egun v2 erabiltzen da nahiz eta v1-en kontrol guztiak ez jasan
- Sistema hierarkikoa da eta prozesu jakin bat cgroup bakarrean egon daiteke
  - Adibidea:

    ````t
    cg1 (parent)        - CPU max 50%, Memory max 2GB
    ├─ cg2 (child)      - CPU max 20% (further limited), Memory max 1GB
    └─ cg3 (child)      - CPU max 30%, Memory max 500MB
    ```
- Prozesu bat sortzerakoan, jatorrizko prozzesuaren cgroup-a heredatzen du.

### Namespaces  

Namespaces isolate what a process can see and access, making it feel like it has its own resources.

8 mota:

| Namespace type | What it isolates                                         | Example in containers                           |
| -------------- | -------------------------------------------------------- | ----------------------------------------------- |
| **PID**        | Process IDs                                              | Container sees only its own processes           |
| **NET**        | Network interfaces and routing                           | Each container has its own IP and network stack |
| **MNT**        | Mount points / filesystem                                | Container has its own view of filesystems       |
| **UTS**        | Hostname and domain name                                 | Container can set its own hostname              |
| **IPC**        | Inter-process communication (semaphores, message queues) | Container processes can only talk to each other |
| **USER**       | User and group IDs                                       | Map container user IDs to host IDs              |
| **CGROUP**     | Control group hierarchy                                  | Limit processes to cgroups they belong to       |
| **TIME**       | System clocks                                            | Container can have its own time offset (v5.6+)  |

### Capabilities

- Root-en pribilegio guztiak zati txikietan zatitu, prozesu bakoitzari beharrezkoak dituen pribilegioak besterik ez emateko.

### syscalls eta seccomp-bpf

**syscalls**:

- Edozein aplikazioak kernelarekin komunikatu nahi duenean erabiltzen duen komunikazio interfazea
- Kopurua arkitekturaren araberakoa da (gaur egun +- 300)

**seccomp-bpf** (*secure computing berkeley packet filter*):

- Prozesu batek erabili ditzakeen syscall multzoa mugatzeko mekanismoa
- Syscall erabili aurretik pasa beharreko filtroa

### chroot

- Prozesu bati erro karpeta aldatzeko syscall-a
- Changes the apparent root directory for a process, making it see only a subset of the filesystem

![kontenedoreak3](kontenedoreak3.png)

### copy-on-write

- a technique where multiple processes or containers share the same data until someone modifies it, at which point a copy is created.
- snapshot-ak sortzeko erabiltzen den mekanismoa da. Normalean, aldatutako datuak bakarrik gordetzen dituzte
- Layer-ak (OverlayFS):
  - Base image layer → minimal OS (Ubuntu, Alpine, etc.)
  - Intermediate layers → software installed, libraries added
  - Top layer → container-specific changes (writable, CoW applies)

## Docker

- PaaS, softwarea kontenedoreetan banatzea ahalbidetzen du.
- Dockerfile -> Docker CLI -> Demonioa (daemon)
