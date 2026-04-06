# Batch, Stream eta Service sistemak

## Sistema motak

1. Service
   - Zerbitzuak bezero batek eskakizun bat bidali arte itxaroten du
     - Eskakizun bat heltzean, sistema ahalik eta azkarren erantzuten ahalegintzen da
   - Zerbitzu baten errendimendua neurtzeko erantzun denbora erabiltzen da
     - Eskuragarritasuna garrantzitsua da mota honetako sistemetan
2. Batch
   - Mota honetako sistema batek sarrera datu asko jasotzen ditu, hauen gainean prozesamendu bat burutu eta erantzun bat sortzen du
     - Prozesamenduak normalean denbora asko behar izaten du, bezeroa ez da itxaroten gelditzen
     - Batch lanak normalean modu errepikakor batean exekutatzeko programatzen dira
     - Banda zabalera garrantzitsua da mota honetako sistemetan
3. Stream
   - Service eta batch arteko nahasketa
   - Stream prozesamendu motako sistemek sarrera datuak jaso (hauek sortu eta bereala), hauen gainean prozesamendua burutu eta irteera datuak sortzen ditu
   - Batch baino latentzia txikiagoa
