# Detekcia anomálií pri nedostatku anomálnych dát

## O projekte

Tento repozitár obsahuje implementáciu a experimentálne výsledky bakalárskej práce zameranej na detekciu poruchových stavov v podmienkach nedostatku anomálnych dát pomocou metód strojového učenia.

Cieľom práce bolo analyzovať a porovnať schopnosť vybraných algoritmov identifikovať anomálie v situáciách, keď sú počas trénovania dostupné prevažne normálne dáta a iba obmedzené množstvo anomálnych vzoriek.

V práci boli implementované a porovnané nasledujúce metódy:

* Isolation Forest
* One-Class Support Vector Machine (One-Class SVM)
* Autoencoder

Experimenty boli realizované na troch verejne dostupných datasetoch:

* NASA Battery Dataset
* NAB (Numenta Anomaly Benchmark)
* ECG5000

---

## Štruktúra repozitára

```text
.
├── notebooks/
│   ├── Isolation_Forest_NASA.ipynb
│   ├── Isolation_Forest_NAB.ipynb
│   ├── Isolation_Forest_ECG5000.ipynb
│   ├── OneClass_SVM_NASA.ipynb
│   ├── OneClass_SVM_NAB.ipynb
│   ├── OneClass_SVM_ECG5000.ipynb
│   ├── Autoencoder_NASA.ipynb
│   ├── Autoencoder_NAB.ipynb
│   └── Autoencoder_ECG5000.ipynb
│
├── data_raw/
├── data_processed/
├── results/
└── README.md
```

---

## Použité datasety

### NASA Battery Dataset

Dataset obsahuje merania získané počas vybíjacích cyklov lítiovo-iónových batérií. Anomálie boli určené na základe poklesu kapacity batérie pod stanovenú hranicu.

### NAB (Numenta Anomaly Benchmark)

Dataset časových radov obsahujúci merania teploty priemyselného zariadenia spolu s označenými intervalmi výskytu anomálií.

### ECG5000

Dataset elektrokardiografických záznamov. Trieda normálnych srdcových úderov bola použitá ako normálna trieda, zatiaľ čo ostatné triedy boli považované za anomálie.

---

## Implementované metódy

### Isolation Forest

Metóda založená na náhodnej izolácii dátových vzoriek pomocou binárnych stromov. Vzorky, ktoré sa izolujú rýchlejšie, sú považované za anomálne.

### One-Class SVM

Metóda vytvára rozhodovaciu hranicu okolo normálnych dát a vzorky nachádzajúce sa mimo tejto hranice klasifikuje ako anomálie.

### Autoencoder

Neurónová sieť trénovaná na rekonštrukciu normálnych dát. Anomálie sú identifikované na základe veľkosti rekonštrukčnej chyby.

---

## Experimentálna metodika

Všetky modely boli trénované výhradne na normálnych dátach.

Vyhodnotenie bolo realizované na testovacích množinách obsahujúcich normálne aj anomálne vzorky.

Počas experimentov boli skúmané:

* rôzne pomery rozdelenia dát,
* rôzne rozhodovacie prahy (threshold),
* viacero náhodných inicializácií (seed),
* priemerné výsledky z piatich nezávislých behov.

Výkonnosť modelov bola hodnotená pomocou metrík:

* Accuracy,
* Precision,
* Recall,
* F1-score.

Súčasťou analýzy boli aj konfúzne matice a histogramy skóre anomálnosti.

---

## Použité technológie

Projekt bol implementovaný v jazyku Python s využitím prostredia Jupyter Notebook.

Použité knižnice:

* NumPy
* Pandas
* Scikit-learn
* TensorFlow / Keras
* Matplotlib
* Seaborn

---

## Autor

**Ievgeniia Ievgrafova**

Bakalárska práca

Fakulta elektrotechniky a informatiky

Slovenská technická univerzita v Bratislave
