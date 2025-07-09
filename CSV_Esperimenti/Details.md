In questa cartella sono caricati i CSV dei vari esperimenti. <br>
In questo file alcuni dettagli sui parametri scelti negli esperimenti già fatti o da caricare.

### Exp1
    semi = (0, 1, 42)
    layers = (16, 32, 64)
    sample_size = [200, 8500, 55000]
    max_epochs = 10 #early stopping

### Exp2
    epochs = 15 #da qui eliminato early stopping
    semi = (0, 1, 42)
    layers = (8, 16, 32, 64, 128)
    sample_size = [500, 8500, 30000, 55000]

### Exp3 [To do]
    epochs = 20
    semi = (0, 1, 42)
    layers = (32, 128, 256, 512)
    sample_size = [8000, 25000, 40000, 55000]
