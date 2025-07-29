### Dati rilevati - Rete A
| Size Hidden Layer | Parametri allenabili | Parametri NON allenabili |
|-------------------|----------------------|---------------------------|
| 8                 | 6480 — 6.5K          | 0                         |
| 16                | 13216 — 13.2K        | 0                         |
| 32                | 27456 — 27.5K        | 0                         |
| 64                | 59008 — 59K          | 0                         |
| 128               | 134400 — 134K        | 0                         |
| 256               | 334336 — 334K        | 0                         |
| 512               | 930816 — 931K        | 0                         |

### Dati rilevati - Rete B
| Size Hidden Layer | Parametri allenabili | Parametri NON allenabili |
|-------------------|----------------------|---------------------------|
| 8                 | 272 — 0.3K           | 6272 — 6.3K               |
| 16                | 928 — 0.9K           | 12544 — 12.5K             |
| 32                | 3392 — 3.4K          | 25088 — 25K               |
| 64                | 12928 — 13K          | 50176 — 50K               |
| 128               | 50432 — 50K          | 100352 — 100K             |
| 256               | 199168 — 200K        | 200704 — 200K             |
| 512               | 791552 — 792K        | 401408 — 401K             |

### Dati rilevati - Rete C
| Size Hidden Layer | Parametri allenabili | Parametri NON allenabili |
|-------------------|----------------------|---------------------------|
| 8                 | 6544 — 6.5K          | 0                         |
| 16                | 13472 — 13.5K        | 0                         |
| 32                | 28480 — 28K          | 0                         |
| 64                | 63104 — 63K          | 0                         |
| 128               | 150784 — 151K        | 0                         |
| 256               | 399872 — 400K        | 0                         |
| 512               | 1192960 — 1.2M       | 0                         |


## Osservazioni
Secondo la teoria della **sample complexity** e in particolare il **Teorema Fondamentale dell’Apprendimento Statistico** (Thm 6.7 "Understanding Machine Learning" - Shai et al.):

$$
C_2 \cdot \frac{\text{VCdim}(\mathcal{H}) + \log\left(\frac{1}{\delta}\right)}{\epsilon^2} \leq \text{sample complexity}(\mathcal{H}) \leq C_1 \cdot \frac{\text{VCdim}(\mathcal{H}) + \log\left(\frac{1}{\delta}\right)}{\epsilon^2}
$$

> *Nota*: questa è una versione semplificata, mancano dettagli legati alle ipotesi del teorema circa la classe H. Ciò nonostante è a fronte di questi risultati e affini (sul rilassamente di alcune ipotesi) che interessa la VCdim di una rete neurale.

---

#### Parametri $\varepsilon$ e $\delta$

$\varepsilon$ e $\delta$ dovrebbero esser fissati a priori per avere assicurazioni. Poichè sto considerando molteplici casistiche senza richieste specifiche su precisione e affidabilità non le dichiaro a priori. Dati gli esperimenti potrei calcolarne la versione empirica, al solito, ciò non da informazioni generali ma solo approssimative.
Un prosieguo interessante sarebbe indagare meglio la classe H fissando epsilon e permetttendo al training di avanzare per più epoche (max_epochs>=20, early stopping su validation_accuracy --> Obiettivo per i prossimi esperimenti).

Circa la loro importanza nel thm. precedente ecco alcune considerazioni.

* Se **$\delta = 0.00001$** (cioè più del 99.999% di confidenza): <br>
  $\log\left(\frac{1}{\delta}\right) \approx \log(10^5) \approx 5 \cdot \log(10) \approx 5 \cdot 2.3 = 11.5$

* Se **$\varepsilon = 0.1$** (cioè errore massimo del 10% o 90% di accuratezza): <br>
  $\frac{1}{\varepsilon^2} = 100$
  
  
Quindi:

  $$
  \text{sample complexity} \propto 100 \cdot \text{VCdim}
  $$

---

#### VC-Dimension delle Reti Neurali

Per una rete neurale con spazio ipotesi $\mathcal{H}$, la VC-dimension è dell’ordine di:

$$
\text{VCdim}(\mathcal{H}) = \mathcal{O}(|E| \cdot \log |E|)
$$

dove $|E|$ è il **numero di archi (parametri)** nella rete, anche se proprio come per le ipotesi del thm. precedente ci sono dei caviat su loss e altri dettagli implementativi. Comunque è questa la complessità che si imputa ad una rete neurale classicamente. Vediamo se rispecchia i risultati degli esperimenti.

La VC-dimension è **proporzionale al numero di archi**, con una costante moltiplicativa logaritmica. Tuttavia, otteniamo **buona accuratezza anche con molte meno risorse** rispetto a questi valori.
<br>

Inoltre confrontando l'andamento del numero di parametri addestrabili:

| Layers | Parametri addestrabili (B) | Parametri non addestrabili (B) | % addestrabili su tot (B) | Parametri addestrabili (A) | Differenza A - B |
|--------|-----------------------------|----------------------------------|----------------------------|------------------------------|------------------|
| 8      | 272                         | 6272                             | 4,16%                      | 6480                         | 6208             |
| 16     | 928                         | 12544                            | 6,89%                      | 13216                        | 12288            |
| 32     | 3392                        | 25088                            | 11,91%                     | 27456                        | 24064            |
| 64     | 12928                       | 50176                            | 20,49%                     | 59008                        | 46080            |
| 128    | 50432                       | 100352                           | 33,45%                     | 134400                       | 83968            |
| 256    | 199168                      | 200704                           | 49,81%                     | 334336                       | 135168           |
| 512    | 791552                      | 401408                           | 66,35%                     | 930816                       | 139264           |
| **1024** | **3155968**               | **802816**                       | **79,72%**                 | **2910208**                  | **-245760**      |

si nota una correlazione tra l'aumento dei pesi allenabili di B e la crescita dell'accuracy.

Sapendo ciò e notando che nel caso layer_512, nonostante la differenza del numero di parametri sia sostanziale tra le due reti (A e B), le performance sono molto simili, si possono formulare queste due ipotesi:
* o l'accuracy è ormai alta, potremmo star andando incontro a saturazione. Quindi influenza molto di più la quantità di informazioni dello specifico dataset che la struttura della rete.
* oppure le due perfomance si avvicinano grazie al contributo dei pesi non addestrabili di B.

Per discriminare tra le due (potrebbero anche essere entrambe valide) si possono fare le seguenti cose:
* verificare se un dataset più complesso (es: Cifar10 o Cifar100) conduca a conclusioni diverse.
* analizzare il caso critico layer_1024

Il caso layer_1024 è critico per due motivi: è il primo momento in cui la rete B ha più parametri allenabili di A, inoltre è l'unico caso non presente nel grafico (ancora da addestrare).

Prevalesse la prima ipotesi si potrebbe concludere che la sample complexity dipenda da esclusivamente dai parametri che possono variare durante il training e non da quelli che una volta scelti restano fissi. Piuttosto ha maggiore impatto il dataset stesso, ovvero la distribuzione di partenza. Il che è in realtà rispecchiato in letteratura dalla Rademacher complexity.

Nel secondo caso invece la conclusione è opposta: l'apprendibilità di una classe non prescinde da un preprocessing, da una predigestione delle informazioni anche con mezzi deterministici o che non variano nel training, ma anzi ne è influenzata anche in maniera variabile. Diventa allora interessante provare varie inizializzazioni dei parametri.

La mia intuizione è che entrambe le conclusioni sia valide, e che tutti e tre i fattori concorrano a modificare l'espressività e quindi la sample complexity di una classe.
