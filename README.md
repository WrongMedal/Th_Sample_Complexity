# Tesi sample complexity WiP

Codice inerente al lavoro di tesi su sample complexity di tre FNN. <br>
⚠️ Tutto il materiale caricato è ancora un Work in Progress ⚠️

### News
_30 luglio_ <br>
introduzione dei grafici sull'architettura delle reti in questo README. <br>
Esperimento 4 (ovvero Exp3 + Layer_critico 1024) con osservazioni e analisi [sempre qui](https://github.com/WrongMedal/Th_Sample_Complexity/blob/main/Grafici_risultati/Osservazioni.md)
.

_29 luglio_ <br>
Osservazioni e commenti sui grafici [in questo file](https://github.com/WrongMedal/Th_Sample_Complexity/blob/main/Grafici_risultati/Osservazioni.md).

_18 luglio_ <br>
Caricamento dei CSV e dei grafici del terzo esperimento. Modificato il codice per generare i grafici per visualizzare la std. dev.

_14 luglio_ <br>
Modifica al codice della rete B per inizializzazione Xavier dei pesi del layer non addestrabile. Riscontrato (offline) significativo miglioramento in questo modo.

_9 luglio_ <br>
Caricati grafici dei primi due esperimenti con codice e note ausiliarie. <br>
Questi primi due esperimenti servono per prendere una mira più accurata prima di produrne altri con parametri più rilevanti per la successiva analisi.<br>

_8 luglio_ <br>
Aggiunti tre colab: ciascuno genera esperimenti al variare della profondità, grandezza di sample, seed di 3 reti neurali (A,B,C).

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
Struttura dimensionale rete A
| Input Layer | 1st Hidden Layer | 2nd Hidden Layer | 3rd Hidden Layer | Output Layer |
|-------------|------------------|------------------|------------------|--------------|
| 28×28       | n                | n                | n                | 10           |

_[Details] <br>
Rete A - Fully connected - Tutti i pesi allenabili_

![Rete A](https://github.com/WrongMedal/Th_Sample_Complexity/blob/main/Codice_generatore_esperimenti/ReteA.drawio.png)

Struttura dimensionale reti B & C:
| Input Layer | 1st Hidden Layer | 2nd Hidden Layer | 3rd Hidden Layer | 4th Hidden Layer | Output Layer |
|-------------|------------------|------------------|------------------|------------------|--------------|
| 28×28       | n                | n                | n                | n                | 10           |

_[Details] <br>
Rete B - Fully connected - Pesi del primo hidden layer NON allenabili (una volta inizializzati restano fissi, la backpropagation non ha effetto su di loro)_

![Rete B](https://github.com/WrongMedal/Th_Sample_Complexity/blob/main/Codice_generatore_esperimenti/ReteB.drawio.png)

_[Details] <br>
Rete C - Fully connected - Tutti i pesi allenabili_

![Rete C](https://github.com/WrongMedal/Th_Sample_Complexity/blob/main/Codice_generatore_esperimenti/ReteC.drawio.png)

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
- Analisi spettrale delle reti
- Test su diverse inizializzazioni
- Test su diverso criterio di arresto in allenamento 
