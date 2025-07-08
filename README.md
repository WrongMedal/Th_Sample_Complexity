# Tesi sample complexity WiP

Codice inerente al lavoro di tesi su sample complexity di tre FNN. <br>
⚠️ Tutto il materiale caricato è ancora un Work in Progress ⚠️

### News
_8 luglio_ <br>
Aggiunti tre colab: ciascuno genera esperimenti al variare della profondità, grandezza di sample, seed di 3 reti neurali (A,B,C). <br>
La rete A e C sono della stessa tipologia, la C ha solo un hidden layer in più. La B si colloca a metà in quanto ha un layer in più di A ma questo non è allenabile.

### Librerie & Pacchetti
    pytorch-lightning 
    torch
    torchvision
    torchmetrics
    seaborn
    matplotlib
    wandb

### Source esterne
Documentazione di Pytorch Lightning <br>
Documentazione di Wandb<br>
Understanding Machine Learning: From Theory to Algorithms (Shai Shalev-Shwartz et al.)<br>
Note/Slide deck del corso "Applicazioni Informatiche del Machine Learning" del Prof. Silvestri

### Dettagli da curare in programma
- Gestione della generazione iniziale dei pesi
- Grafici sulla relazione diretta tra sample size e test_accuracy/test_loss
