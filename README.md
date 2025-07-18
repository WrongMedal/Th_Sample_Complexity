# Tesi sample complexity WiP

Codice inerente al lavoro di tesi su sample complexity di tre FNN. <br>
⚠️ Tutto il materiale caricato è ancora un Work in Progress ⚠️

### News
_18 luglio_ <br>
Carimento dei CSV e dei grafici del terozo esperimento. Modificato il codice per generare i grafici per visualizzare la std. dev. delle reti.

_14 luglio_ <br>
Modifica al codice della rete B per inizializzazione Xavier dei pesi del layer non addestrabile. Riscontrato (offline) significativo miglioramento in questo modo.

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

### Struttura delle reti
Nel terzo esperimento _n_ è scelto da _(8, 16, 32, 64, 128, 256, 512)_ <br> 
Rete A:
| Input Layer | 1st Hidden Layer | 2nd Hidden Layer | 3rd Hidden Layer | Output Layer |
|-------------|------------------|------------------|------------------|--------------|
| 28×28       | n                | n                | n                | 10           |

Rete B & C:

| Input Layer | 1st Hidden Layer | 2nd Hidden Layer | 3rd Hidden Layer | 4th Hidden Layer | Output Layer |
|-------------|------------------|------------------|------------------|------------------|--------------|
| 28×28       | n                | n                | n                | n                | 10           |

La differenza tra B e C sta tra Input Layer e 1st Hidden Layer. I pesi tra questi due layer non sono allenabili, una volta inizializzati restano fissi, la backpropagation non ha effetto su di loro.
<br>

### Inizializzazione & Ottimizzatore delle reti
L'inizializzazione delle reti A e C è quella di default di Pytorch Lightning:
<pre> weight ~ U(−√(1 / in_features), √(1 / in_features)) </pre>
Dove U è distribuzione uniforme. <br>
Source: https://github.com/pytorch/pytorch/blob/main/torch/nn/modules/linear.py <br>
Per la rete B è stata scelta una inizializzazione **esclusivamente** sui pesi non addestrabili. <br>
Questa inizializzazione è quella Xavier/Glorot su distribuzione uniforme:
<pre> weight ~ U(−√(6 / (in_features + out_features)), √(6 / (in_features + out_features))) </pre>

L'ottimizzatore usato è SGD.

### Source esterne
Documentazione di Pytorch Lightning <br>
Documentazione di Wandb<br>
Understanding Machine Learning: From Theory to Algorithms (Shai Shalev-Shwartz et al.)<br>
Deep Learning (Ian Goodfellow et al.) <br>
Note/Slide deck del corso "Applicazioni Informatiche del Machine Learning" @ Sapienza del Prof. Silvestri

### Nei prossimi episodi
- Esperimento numero 3 con grafici
- Considerazioni e migliorie tramite Margin Based Bounds 
