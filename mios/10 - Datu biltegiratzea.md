# Datu biltegiratzea

## Motorrak

1. OLTP: Transakzioetarako
   - Eskakizun asko
   - Azkarra
   - Denbora errealean
   - Bottleneck -> disgo gogorraren seek denbora (toki batetik bestera salto egiteko beharreko denbora)
2. OLAP: Analitikarako
   - Datuen analisia egiteko
   - Eskakizun gutxiago
   - Kontsulta bakoitzak datu asko behar ditu
   - Bottleneck -> diskoaren banda zabalera

## Datu modeloa

Datu elementuak nola antolatu eta elkarrik eta mundu errealeko propietateekin nola erlazionatzen diren errepresentatzen duen eredua.

Erlazio motak:

- One to one
- One to many
- Many to many
- Many to one

## Fitxategi sistema

Egitura logiko bat, hardwarean datuak nola biltegiratu, antolatu eta irakurtzen diren definitzen duena.

**HDFS (Hadoop Distributed File System )**:

- Distribuitua
- Errendimendu altua
- Akats tolerantzia altua datuak erreplikatuz
- Datu modeloa: Fitxategi blokeak
- Erabilera: Big data edo analitika
- Ekosistema: Apache Hadoop

## Korronte biltegiratzea - Streaming storage

- Datu-fluxuak denbora errealean erabiltzeko diseinatutako biltegiratzea
- Ezaugarriak:
  - Denbora errealeko datu irenstea (datu bolumen handiak hartu eta gorde denbora errealean)
  - Errendimendu handia eta eskalagarritasuna (tasa handiak jasateko eta hrizontalki eskalatzeko diseinatua)
  - Latentzia txikia
  - Iraunkortasuna eta fidagarritasuna (datu erreplikazioari esker)
  - Gertaerak prozesatzea eta analisia
- Apache kafka
  - Mota: gertaera streaming plataforma
  - Datu modeloa: gertaera korronteak
  - Prozesamendua: denbora errealean eta sortaka

## Zutabe biltegiratzea

- Datu basetan datuak antolatzeko era bat, tauletako datuak lerroetan ordez zutabetan biltegiratzen dituena.

    ```t
    ID   → [1, 2, 3]
    Name → [Ana, Jon, Lee]
    Age  → [25, 30, 22]
    ```

- Datu kantitate handien analisiak eta prozesamendua burutzeko aproposa -> Data Warehouse
- Ezaugarriak:
  - Biltegiratze eraginkorra -> konpresioa erraztu mota berekoak direlako datuak
  - Kontsulten errendimendua hobetzea
  - Optimizazioa irakurketa-eragiketetarako
  - Bektorizazioa -> bizkortu agregazio eta eragiketa matematikoak datuetan
- Abantailak:
  - Errendimendu handia
  - Datuen konpresio eraginkorra
  - Datuak azkar kargatzea
- Desabantailak:
  - Hain eraginkorrak ez diren idazketak
  - Diseinuaren eta mantentze lanen konplexutasuna
- Zutabe biltegiratze motor -> Apache Cassandra
- Zutabe biltegiratze fitxategi format -> Apache Parquet

## Indizeak

Edozein biltegiratze sistemaren eginkizun garrantzitsuenak:

1. Datuak gordetzea
2. Datuak itzultzea

- An index is a data structure that improves query performance by providing fast access to rows based on column values
- Ondo aukeratutako indizeek irakurketa kontsultak azkartzen dituzte, baina indize bakoitzak idazketa eragiketak moteltzen ditu

**Teknkikak**:

1. a

## Erreplikazioa

- Datu beraren hainbat kopia nodo ezberdinetan mantentzea, potentzialki kokaleku ezberdinetan
- Abantailak:
  - Eskuragarritasuna handitu
  - Irakurketa banda zabalera handitu
  - Datuak geografikoki hurbildu latentzia murriztuz
- Desabantailak:
  - Datu aldaketak kudeatzea

**Motak**:

1. Sinkronoa
   - El líder manda mensaje de que hay que escribir datos y se queda pendiente de la respuesta de los seguidores.
   - Pros: coherencia de datos, los seguidores tienen copias actualizadas y si el lider falla pueden tirar de estas
   - Cons: si uno de los seguidores tiene algún error, el líder se queda bloqueado esperando
2. Asinkronoa
   - El líder manda mensaje de que hay escribir pero no espera
   - Pros: si un seguidor falla el líder no se bloquea
   - Cons: los seguidores quedan con datos inconsistentes
3. Mezcla
   - Muchas veces se usan los dos tipos, poniendo 1 sincrono y el resto asincronos, por ejemplo
   - Si un sincrono falla, uno de los asincronos se convierte sincrono
   - Esto hace que por lo menos el lider y un seguidor sincrono tengan una copia actualizada

**Liderrak**:

1. Lider bakarra
   - Bakarrik lider 1
   - Failover = liderra erortzea
     - Jarraitzaile bat lider bezala aukeratu
     - Bezeroak birkonfiguratu
     - Jaraitzaileek lider be
2. Hainbat liderrak
3. Liderless
