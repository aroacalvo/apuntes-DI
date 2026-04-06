# Datu Fluxua

- Prozesu batetik baste batetara igarotzean datuek jarraitzen duten bidea

## Datu bidezko datu fluxua

- Bi prozesuak hartzen dute parte:
  1. DB idaztean datuak kodifikatzen dituen prozesua
  2. DB irakurtzean datuak dekodifikatzen dituen prozesua
- Datu base erlazionalek eskema bat behar dute

## Zerbitzu bidezko datu fluxua

- Bi prozesu sare bidez komunikatzea ahalbidetzen du
- Bi talde nagusi:
  - HTTP protokolo erabiltzen denean -> Web zerbitzuak
  - Bestela -> RMI (Remote Method Invocation)

**Web zerbitzuak**:

1. REST
   - Ez da protokolo bat
   - HTTP printzipioetan oinarrituta
2. SOAP
   - XMLen oinarritutako protokoloa
   - HTTP gainetik erabiltzen da normalean baina independientea da
   - API-a XML-n oinarritutako lengoai batean oinarrituta egon behar da

**RMI/RPC**:

- A mechanism that allows a program to call methods on an object located on another machine as if it were local

**REST vs RPC**:

RCP + kodifikazio bitarra errendimendu hobea REST + JSON baino

## Asynchronous Message Passing bidezko datu fluxua

- DB eta RPC-ren arteko zerbait
- Komunikazioa norabide bakarrekoa
- Mezuak tarteko nodo batera bidaltzen dira -> message broker
- Abantailak (RPC-rekin alderatuta)
  - Bidaltzailea eta jasotzailea ez dute eskuragarri egon behar aldi berean
  - Errore bat egonez gero automatikoki berbidaltzen dira mezuak
  - Mezu bat hainbatek jasotzea ahalbidetzen du
- Adibidez: RabbitMQ, Apache Kafka
