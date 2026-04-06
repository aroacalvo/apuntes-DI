# Definizioak

## Kluster

- Konputagailu multzo bati egiten dio errefentzia, elkarrekin lan egiten dutenak entitate bakar bat balira bezala
- Baliabideak partekatzea  eta datuak biltegiratzea ahalbidetzen du

**Motak**:

- High availability (HA)
  - Sistema batek erabiltzaileentzat erabilgarri eta irisgarri izaten jarraitzeko duen gaitasuna, nahiz eta huts egin.
  - Failover mekanismoak: huts eginez gero, ordezkapen automatikoa
- Errendimendu Handiko Klusterrak (HPC)
  - Prozesatzeko ahalmen masiboa. Eragiketa konplexuak edo datu multzo masiboak paraleloki banatzen dute.
- Load-balancing
  - Erabiltzaileen eskaerak hainbat zerbitzariren artean banatzen dituzte, baliabideen erabilera optimizatzeko, erantzuteko denbora hobetzeko eta zerbitzuaren erabilgarritasuna ziurtatzeko.
- Biltegiratze banatuaren klusterrak
  - Datuak hainbat nodotan gordetzeko aukera ematen dute, datuen biltegiratzearen eskalagarritasuna eta fidagarritasuna areagotuz

## Eskalabilitatea - scalability

- Sistemaren ahalmena handitu errendimendu eta lan kargari erantzuteko
- Lan karga izan daiteke: eskariak segunduko, eragiketak segunduko, transakzioak segunduko...
- Motak
  - Bertikala - scale up
    - Makina bakar baten errekurtsoak handitu (adb: +RAM)
    - Erraza egiteko eta azpiegitura ez da aldatzen, baina ezin da betirako egin (hardware limitea)
    ![scale up](scale-up.png)
  - Horizontala - scale out
    - Makina gehiago gehitu sisteman
    - Eskalagarria baina konplexua, load balancing behar du
    ![scale-out](scale-out.png)

## Elastikotasuna - elasticity

- Sistema batek bere baliabideak eskariaren arabera automatikoki doitzeko duen gaitasuna.
  - Goruntz
  - Beheruntz
  - Zerora

## Eskuragarritasuna - availability

- IT zerbitzu edo osagai bat erabilgarri dagoen denboraren ehunekoa

## Fidagarritasuna - reliability

- Denbora tarte batean aurrez definitutako funtzionamendu estandarea betetzeko sistemaren probabilitatea.
- Akatsen aurrean ere behar den bezala funtzionatzeko gaitasuna,akats-tolerantzia edo erresilientzia
- Fidagarritasuna ⬇️ -> eskuragarritasuna ⬇️
- Elastikotasuna ⬆️ -> fidagarritasuna ⬆️

## Cloud Computing

- baliabide informatikoak (zerbitzariak, biltegiratzea, datu-baseak, networkinga, softwarea eta gehiago) Interneten bidez entregatzea, erabiltzaileek nahi dutenean eskura ditzaten, hardware fisikorik eduki gabe.

## Infrastructure as a Service (IaaS)

- Hodeiko konputazio-eredua, non azpiegitura informatikoak (makina birtualak, biltegiratzea eta sareak) Internet bidez alokatzen diren, hornitzaileak hardware fisikoa kudeatzen duen bitartean.

## Platform as a Service (PaaS)

- Hodeiko konputazio-eredu bat, non aplikazioak garatzeko, exekutatzeko eta kudeatzeko prest dagoen plataforma bat alokatzen den, azpiko zerbitzariez, biltegiratzeaz edo sare-lanaz arduratu gabe.

## Software as a Service (SaaS)

- Softwarearen lizentziamendu eta banaketa eredua, softwarea harpidetza bidez lizentziatu eta modu zentralizatuan ostatzen duena

## Function as a Service (FaaS)

- Hodeiko konputazio-eredu bat, zeinean funtzio indibidualak edo kode-zatiak exekutatzen diren gertaeren aurrean, zerbitzaririk eta azpiegiturarik kudeatu gabe. Serverless computing ere esaten zaio.

## Serverless

- Hodeian kodea hedatzen eta exekutatzen uzten dizu zerbitzariez arduratu gabe, eskariz automatikoki eskalatuz.
- Zerora, goruntz edo beheruntz eskalatu daiteke
- Kontsultak kontsumitzen dituen datu kantitateagatik eta gordetako datuengatik ordaintzen da.
- Puntu bat ailegatzen da non serverless zure azpiegitura izatea baino garestiagoa den
