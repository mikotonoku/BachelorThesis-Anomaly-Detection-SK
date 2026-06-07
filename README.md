# Detekcia anomálií pri nedostatku anomálnych dát

![Python](https://img.shields.io/badge/Python-3.11-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-yellow)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)
![Bachelor Thesis](https://img.shields.io/badge/Bachelor-Thesis-success)

## O projekte

Tento repozitár obsahuje zdrojové kódy, predspracovanie dát a experimenty vytvorené v rámci bakalárskej práce zameranej na detekciu anomálií pomocou metód strojového učenia v podmienkach nedostatku anomálnych dát.

Cieľom práce bolo analyzovať a porovnať vlastnosti troch metód detekcie anomálií:

* Isolation Forest
* One-Class Support Vector Machine (One-Class SVM)
* Autoencoder

Experimenty boli realizované na troch datasetoch reprezentujúcich rôzne typy dát:

* NAB (Numenta Anomaly Benchmark) – priemyselné časové rady,
* ECG5000 – biomedicínske EKG signály,
* NASA Battery Dataset – degradačné dáta lítiovo-iónových batérií.

Vo všetkých experimentoch boli modely trénované výlučne na normálnych dátach. Anomálne vzorky boli použité iba počas testovania a hodnotenia modelov.

---

# Štruktúra repozitára

```text
BachelorThesis-Anomaly-Detection-SK
│
├── notebooks/
│   │
│   ├── Autoencoder_ECG5000.ipynb
│   ├── Autoencoder_NAB.ipynb
│   ├── Autoencoder_NASA.ipynb
│   │
│   ├── Isolation_Forest_ECG5000.ipynb
│   ├── Isolation_Forest_NAB.ipynb
│   ├── Isolation_Forest_NASA.ipynb
│   │
│   ├── OneClass_SVM_ECG5000.ipynb
│   ├── OneClass_SVM_NAB.ipynb
│   ├── OneClass_SVM_NASA.ipynb
│   │
│   ├── nab.ipynb
│   └── nasa_battery.ipynb
│
├── data_raw/
│   │
│   ├── ECG5000/
│   ├── NAB/
│   └── nasa_battery/
│
├── data_processed/
│
├── results/
│
└── README.md
```

---

# Popis datasetov

## NASA Battery Dataset

Dataset obsahuje merania lítiovo-iónových batérií počas ich životného cyklu.

Pri predspracovaní boli použité iba vybíjacie cykly. Z pôvodných meraní boli vytvorené odvodené príznaky charakterizujúce stav batérie počas jej degradácie.

Použité vstupné veličiny:

* Voltage_measured
* Current_measured
* Temperature_measured
* Current_load
* Voltage_load
* Time

Okrem pôvodných veličín boli vytvorené:

* rozdielové príznaky (first-order differences),
* kĺzavé priemery,
* smerodajné odchýlky,
* minimálne a maximálne hodnoty v kĺzavom okne.

Anomálne cykly boli identifikované na základe kapacity batérie. Cykly s kapacitou nižšou ako 20. percentil boli označené ako anomálne.

---

## NAB (Numenta Anomaly Benchmark)

Dataset NAB predstavuje priemyselný časový rad obsahujúci merania teploty priemyselného zariadenia.

Počas predspracovania boli vytvorené odvodené príznaky:

* hodnota signálu,
* prvá diferenciácia,
* kĺzavý priemer,
* kĺzavá smerodajná odchýlka,
* kĺzavé minimum,
* kĺzavé maximum.

Anomálie boli označené podľa oficiálnych intervalov definovaných v datasete NAB.

---

## ECG5000

Dataset ECG5000 obsahuje elektrokardiografické záznamy pozostávajúce zo 140 bodov reprezentujúcich jeden srdcový cyklus.

Trieda 1 predstavuje normálne EKG záznamy.

Triedy 2–5 boli považované za anomálne.

Pri experimentoch:

* modely boli trénované iba na normálnych vzorkách,
* anomálne vzorky boli použité iba počas testovania,
* bola použitá Z-normalizácia založená na trénovacích dátach.

---

# Popis notebookov

## Predspracovanie dát

### nab.ipynb

Notebook vykonáva:

* načítanie datasetu NAB,
* označenie anomálnych intervalov,
* vytvorenie odvodených príznakov,
* uloženie výsledného datasetu pre experimenty.

### nasa_battery.ipynb

Notebook vykonáva:

* načítanie NASA Battery datasetu,
* výber vybíjacích cyklov,
* vytvorenie príznakov,
* označenie anomálnych cyklov,
* uloženie spracovaného datasetu.

Výsledný súbor:

```text
data_processed/nasa_battery_features_rolling.csv
```

je následne využívaný všetkými experimentmi na datasete NASA Battery.

## Experimentálne notebooky

### Isolation Forest

* Isolation_Forest_ECG5000.ipynb
* Isolation_Forest_NAB.ipynb
* Isolation_Forest_NASA.ipynb

Implementácia zahŕňa trénovanie modelu, výpočet anomaly score, aplikáciu rozhodovacieho prahu a vyhodnotenie výsledkov.

### One-Class SVM

* OneClass_SVM_ECG5000.ipynb
* OneClass_SVM_NAB.ipynb
* OneClass_SVM_NASA.ipynb

Implementácia využíva RBF kernel a klasifikáciu na základe decision score.

### Autoencoder

* Autoencoder_ECG5000.ipynb
* Autoencoder_NAB.ipynb
* Autoencoder_NASA.ipynb

Autoencoder využíva neurónovú sieť implementovanú pomocou TensorFlow/Keras. Detekcia anomálií je založená na rekonštrukčnej chybe.

---

# Spoločné nastavenia experimentov

Vo všetkých experimentoch boli použité nasledovné princípy:

* modely boli trénované iba na normálnych dátach,
* anomálne vzorky boli použité iba počas testovania,
* hodnotenie bolo realizované pomocou metrík Accuracy, Precision, Recall a F1-score,
* výsledky boli doplnené o konfúzne matice,
* výsledky boli doplnené o histogramy skóre.

## Isolation Forest

Vo všetkých experimentoch s metódou Isolation Forest boli použité tieto základné parametre:

* n_estimators = 300
* contamination = "auto"
* random_state = 42 pri datasetoch ECG5000 a NAB
* pri NASA Battery boli použité seeds = [42, 43, 44, 45, 46]

---

## One-Class SVM

Vo všetkých experimentoch s metódou One-Class SVM boli použité tieto základné parametre:

* kernel = "rbf"
* nu = 0.05
* gamma = "auto"
* pri NASA Battery boli použité seeds = [42, 43, 44, 45, 46]

---

## Autoencoder

Vo všetkých experimentoch s metódou Autoencoder bola použitá rovnaká základná architektúra:

* hidden_dim = 32
* encoding_dim = 8
* batch_size = 64
* learning_rate = 0.001
* epochs = 100
* patience = 10
* validation_split = 0.2
* optimizer = Adam
* loss function = Mean Squared Error (MSE)
* pri NASA Battery boli použité seeds = [42, 43, 44, 45, 46]

---

# Najlepšie výsledky

Nasledujúca tabuľka sumarizuje najlepšie konfigurácie a výsledky dosiahnuté jednotlivými metódami.

| Metóda | Dataset | Threshold | Train fraction | Accuracy (%) | Precision (%) | Recall (%) | F1-score (%) |
|---------|---------|---------:|---------:|---------:|---------:|---------:|---------:|
| iForest | NASA Battery | 0.065 | 0.90 | 85.28 | 85.58 | 94.09 | 89.54 |
| iForest | ECG5000 | 0.0 | – | 93.42 | 90.09 | 94.61 | 92.29 |
| iForest | NAB | -0.15 | 0.80 | 99.29 | 96.68 | 97.71 | 97.19 |
| OCSVM | NASA Battery | 20.0 | 0.90 | 78.86 | 87.85 | 79.42 | 83.39 |
| OCSVM | ECG5000 | -0.3 | – | 96.87 | 94.59 | 98.08 | 96.30 |
| OCSVM | NAB | -5.0 | 0.80 | 97.59 | 90.89 | 89.77 | 90.33 |
| AE | NASA Battery | 0.002 | 0.90 | 86.91 | 86.63 | 95.75 | 90.84 |
| AE | ECG5000 | 0.7 | – | 94.53 | 94.43 | 92.31 | 93.36 |
| AE | NAB | 0.00006 | 0.80 | 95.85 | 80.22 | 88.71 | 84.25 |

---

# Ukážka výstupov experimentu

Ako reprezentatívny príklad je uvedený Autoencoder na datasete ECG5000 s rozhodovacím prahom:

```text
Threshold = 0.7
```

### Tabuľka metrík

<img width="1455" height="720" alt="metrics_table" src="https://github.com/user-attachments/assets/f2c3491c-e7c8-4def-b5dc-d55e8c933367" />

### Konfúzna matica

<img width="1753" height="1385" alt="confusion_matrix" src="https://github.com/user-attachments/assets/da42f92c-027d-43b4-82ce-505a46988ca0" />

### Histogram rekonštrukčnej chyby

<img width="2967" height="1470" alt="reconstruction_error_histogram" src="https://github.com/user-attachments/assets/c4a6ada0-98c9-42d2-ae01-b7f14df2e169" />

### Rekonštrukcia normálneho a anomálneho EKG signálu

<img width="2969" height="1769" alt="ecg_reconstruction_examples" src="https://github.com/user-attachments/assets/653ece48-bb41-4944-87fc-268187dd8bc2" />

Na histograme rekonštrukčnej chyby je možné pozorovať oddelenie normálnych a anomálnych vzoriek pomocou rozhodovacieho prahu.

Graf rekonštrukcie EKG signálov ukazuje schopnosť Autoencodera presnejšie rekonštruovať normálne vzorky, zatiaľ čo pri anomálnych vzorkách vzniká výraznejšia rekonštrukčná chyba.

---

# Inštalácia

Projekt bol vytvorený v prostredí:

* Python 3.x
* Jupyter Notebook
* Anaconda

Použité knižnice:

* pandas
* numpy
* scikit-learn
* tensorflow
* keras
* matplotlib
* seaborn
* scipy
* pathlib

---

# Spustenie projektu

## NASA Battery

Dataset NASA Battery nie je súčasťou repozitára z dôvodu veľkosti dát.

Pred spustením experimentov:

1. Stiahnite dataset NASA Battery.
2. Skopírujte jeho obsah do priečinka:

```text
data_raw/nasa_battery/
```

3. Spustite:

```text
notebooks/nasa_battery.ipynb
```

Notebook automaticky vytvorí:

```text
data_processed/nasa_battery_features_rolling.csv
```

Následne je možné spustiť experimentálne notebooky pre NASA dataset.

### Poznámka

Priečinok `data_processed` musí existovať.

Ak súbor `nasa_battery_features_rolling.csv` neexistuje, notebook ho vytvorí automaticky.

---

## NAB

Dataset NAB je už súčasťou repozitára.

Pre vytvorenie spracovaných dát spustite:

```text
notebooks/nab.ipynb
```

Následne je možné spustiť experimentálne notebooky.

---

## ECG5000

Dataset ECG5000 je už súčasťou repozitára.

Nie je potrebné vykonávať samostatné predspracovanie.

Experimentálne notebooky načítavajú dataset priamo.

---

# Autor

**Ievgeniia Ievgrafova**

Bakalárska práca

Fakulta elektrotechniky a informatiky

Slovenská technická univerzita v Bratislave

2026
