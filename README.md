# Tesi sample complexity WiP

Codice inerente al lavoro di tesi su sample complexity di tre FNN. <br>
⚠️ Tutto il materiale caricato è ancora un Work in Progress ⚠️

### News
_9 luglio_ <br>
Caricati grafici dei primi due esperimenti con codice e note ausiliarie. <br>
Questi primi due esperimenti servono per prendere una mira più accurata prima di produrne altri con parametri più rilevanti per la successiva analisi.<br>

_8 luglio_ <br>
Aggiunti tre colab: ciascuno genera esperimenti al variare della profondità, grandezza di sample, seed di 3 reti neurali (A,B,C). <br>
La rete A e C sono della stessa tipologia, la C ha solo un hidden layer in più. La B si colloca a metà in quanto ha un layer in più di A ma questo non è allenabile.

### Librerie & Pacchetti
Il file **_requirements.txt_** è stato autogenerato dal Colab della Rete A, quindi può includere anche dei pacchetti non utilizzati. I seguenti sono quelli, in generale, 
introdotti nel codice per gli specifici obiettivi di questo progetto:

    pytorch-lightning 
    torch
    torchvision
    torchmetrics
    seaborn
    matplotlib
    pandas
    wandb


### Source esterne
Documentazione di Pytorch Lightning <br>
Documentazione di Wandb<br>
Understanding Machine Learning: From Theory to Algorithms (Shai Shalev-Shwartz et al.)<br>
Note/Slide deck del corso "Applicazioni Informatiche del Machine Learning" del Prof. Silvestri

### Nei prossimi episodi
- Gestione della generazione iniziale dei pesi da parte di lightning, se possibile, scelta di una distribuzione fissa. 
