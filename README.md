# Detekcia anomálií pri nedostatku anomálnych dát

## O projekte

Tento repozitár obsahuje zdrojové kódy a experimenty vytvorené v rámci bakalárskej práce zameranej na detekciu anomálií pomocou metód strojového učenia v podmienkach nedostatku anomálnych dát.

Cieľom práce bolo analyzovať a porovnať vlastnosti troch metód detekcie anomálií:

* Isolation Forest
* One-Class Support Vector Machine (One-Class SVM)
* Autoencoder

Experimenty boli realizované na troch datasetoch reprezentujúcich rôzne typy dát:

* NAB (Numenta Anomaly Benchmark) – priemyselné časové rady,
* ECG5000 – biomedicínske EKG signály,
* NASA Battery Dataset – degradačné dáta lítiovo-iónových batérií.

Všetky modely boli trénované výlučne na normálnych dátach a anomálne vzorky boli použité iba počas testovania.

---

# Štruktúra repozitára

```text
BachelorThesis-Anomaly-Detection-SK
│
├── Autoencoder_ECG5000.ipynb
├── Autoencoder_NAB.ipynb
├── Autoencoder_NASA.ipynb
│
├── Isolation_Forest_ECG5000.ipynb
├── Isolation_Forest_NAB.ipynb
├── Isolation_Forest_NASA.ipynb
│
├── OneClass_SVM_ECG5000.ipynb
├── OneClass_SVM_NAB.ipynb
├── OneClass_SVM_NASA.ipynb
│
├── nab.ipynb
├── nasa_battery.ipynb
│
├── data_raw/
├── data_processed/
│
└── README.md
```

---

# Popis jednotlivých súborov

### Predspracovanie dát

**nab.ipynb**

Notebook určený na predspracovanie datasetu NAB. Vykonáva načítanie dát, vytvorenie odvodených príznakov, označenie anomálií a vytvorenie výsledného datasetu použitého pri experimentoch.

**nasa_battery.ipynb**

Notebook určený na predspracovanie datasetu NASA Battery. Vytvára odvodené príznaky z vybíjacích cyklov batérií a generuje výsledný súbor:

```text
data_processed/nasa_battery_features_rolling.csv
```

Tento súbor je následne využívaný všetkými experimentmi realizovanými na datasete NASA Battery.

### Experimenty

Pre každý dataset boli implementované tri metódy:

#### Isolation Forest

* Isolation_Forest_NAB.ipynb
* Isolation_Forest_ECG5000.ipynb
* Isolation_Forest_NASA.ipynb

#### One-Class SVM

* OneClass_SVM_NAB.ipynb
* OneClass_SVM_ECG5000.ipynb
* OneClass_SVM_NASA.ipynb

#### Autoencoder

* Autoencoder_NAB.ipynb
* Autoencoder_ECG5000.ipynb
* Autoencoder_NASA.ipynb

Každý notebook obsahuje kompletný experiment vrátane načítania dát, trénovania modelu, vyhodnotenia metrík, vytvorenia konfúznych matíc a grafických výstupov.

---

# Použité datasety

## NASA Battery Dataset

Dataset obsahuje merania lítiovo-iónových batérií počas nabíjacích a vybíjacích cyklov.

Zdroj:

https://www.kaggle.com/datasets/patrickfleith/nasa-battery-dataset/data/code?select=cleaned_dataset

---

## NAB (Numenta Anomaly Benchmark)

Dataset priemyselných časových radov s označenými anomáliami.

Zdroj:

https://www.kaggle.com/datasets/boltzmannbrain/nab

---

## ECG5000

Dataset elektrokardiografických záznamov využívaný pri detekcii anomálií v EKG signáloch.

Zdroj:

https://www.kaggle.com/code/mineshjethva/ecg-anomaly-detection

---

# Inštalácia

Projekt bol vytvorený v prostredí:

* Python 3.x
* Jupyter Notebook
* Anaconda

Odporúča sa vytvoriť samostatné virtuálne prostredie.

---

# Použité knižnice

Pri implementácii boli použité najmä tieto knižnice:

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

# Postup spustenia

## Dataset NASA Battery

1. Stiahnite pôvodný dataset NASA Battery.
2. Umiestnite dáta do adresára `data_raw`.
3. Spustite notebook:

```text
nasa_battery.ipynb
```

4. Notebook automaticky vytvorí súbor:

```text
data_processed/nasa_battery_features_rolling.csv
```

5. Následne je možné spúšťať experimenty:

```text
Isolation_Forest_NASA.ipynb
OneClass_SVM_NASA.ipynb
Autoencoder_NASA.ipynb
```

## Dataset NAB

1. Stiahnite dataset NAB.
2. Spustite notebook:

```text
nab.ipynb
```

3. Po vytvorení predspracovaných dát je možné spustiť experimentálne notebooky.

## Dataset ECG5000

Dataset sa načítava priamo v experimentoch:

```text
Isolation_Forest_ECG5000.ipynb
OneClass_SVM_ECG5000.ipynb
Autoencoder_ECG5000.ipynb
```

---

# Hodnotenie modelov

Výsledky experimentov boli hodnotené pomocou metrík:

* Accuracy
* Precision
* Recall
* F1-score

Súčasťou analýzy boli aj:

* konfúzne matice,
* histogramy skóre anomálnosti,
* histogramy rekonštrukčnej chyby (Autoencoder).

---

# Autor

**Ievgeniia Ievgrafova**

Fakulta elektrotechniky a informatiky

Slovenská technická univerzita v Bratislave

Bakalárska práca
