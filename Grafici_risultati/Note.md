### Note
Il codice qui presente funziona con la nomenclatura/struttura adottata nel mio drive, per farla funzionare nel proprio bisogna modificare i path che riferiscono a:
- input, ovvero laddove sono salvati i file CSV (ottenuti da Wandb runnando il codice per le reti nella cartella "Codice_generatore_esperimenti") 
- output, ovvero dove si vuole salvare i grafici ottenuti

### Exp3 Details
    epochs = 20
    semi = (0, 1, 42)
    layers = (8, 16, 32, 64, 128, 256, 512)
    sample_size = (8000, 12000, 25000, 32000, 40000, 47000, 55000)

### Exp4 Details
    epochs = 20
    semi = (0, 1, 42)
    layers = (8, 16, 32, 64, 128, 256, 512, 1024)
    sample_size = (8000, 12000, 25000, 32000, 40000, 47000, 55000)

Ogni linea del plot è ottenuta mediando sui tre seed. <br> 
Le linee tratteggiate indicano la deviazione standard. <br>
L'accuracy e loss di riferimento sono quelle ottenute dal test, fatto esclusivamente a fine training e non epoca per epoca.
