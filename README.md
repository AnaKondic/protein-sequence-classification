# Klasifikacija proteinskih sekvenci upotrebom metoda mašinskog učenja

## Opis projekta

Ovaj projekat predstavlja praktičnu realizaciju diplomskog rada čiji je cilj razvoj i evaluacija metoda mašinskog i dubokog učenja za klasifikaciju proteinskih sekvenci organizma *Homo sapiens* prema biološkoj funkciji i subcelularnoj lokalizaciji, isključivo na osnovu aminokiselinske sekvence.

Razmatrana su dva klasifikaciona problema:
- **Biološka funkcija** – klasifikacija proteina u pet funkcionalnih kategorija: hidrolaze, receptori, strukturni proteini, transkripcijski faktori i transportni proteini.
- **Subcelularna lokalizacija** – klasifikacija proteina prema pet kategorija: jedro, citoplazma, ćelijska membrana, mitohondrija i sekretorni proteini.

Oba problema razmatrana su kroz dvije formulacije:
- **Single-label classification (SLC)** – svakom proteinu dodjeljuje se jedna klasa.
- **Multi-label classification (MLC)** – proteinu se može dodijeliti više klasa istovremeno.

## Podaci

Proteinske sekvence i pripadajući metapodaci preuzeti su iz baze [UniProt](https://www.uniprot.org/) u martu 2026. godine, iz ručno kuriranog UniProtKB/Swiss-Prot dijela baze, uz ograničenje na organizam *Homo sapiens*.

Preuzeti podaci prolaze kroz postupak čišćenja, filtriranja, uklanjanja duplikata i formiranja SLC i MLC podskupova.

Obrađeni skupovi podataka čuvaju se u direktorijumu `data/processed/`, dok se generisane reprezentacije sekvenci i istrenirani modeli čuvaju u direktorijumima `data/features/` i `data/models/`.

## Korištene metode

U projektu su implementirane sljedeće reprezentacije proteinskih sekvenci:

- Aminokiselinski sastav (AAC-CV).
- TF-IDF reprezentacija sa redukcijom dimenzionalnosti pomoću SVD-a.
- Fizičko-hemijski deskriptori (PH).
- Embedinzi dobijeni pomoću proteinskog jezičkog modela ESM-2.

Za klasifikaciju su korišteni sljedeći modeli:
- Logistička regresija (LR).
- Slučajne šume (Random Forest – RF).
- Metoda potpornih vektora (Support Vector Machine – SVM).
- Višeslojni perceptron (Multilayer Perceptron – MLP).

Performanse modela procijenjene su odgovarajućim metrikama za single-label i multi-label klasifikaciju.

## Struktura projekta

```text
project/
│
├── data/
│   ├── raw/          # Originalno preuzeti podaci
│   ├── processed/    # Obrađeni skupovi podataka
│   ├── features/     # Generisane reprezentacije sekvenci
│   └── models/       # Sačuvani istrenirani modeli
│
├── notebooks/
│   ├── function/     # Eksperimenti za biološku funkciju
│   └── localization/ # Eksperimenti za subcelularnu lokalizaciju
│
├── results/
│   ├── eda/          # Rezultati eksploratorne analize
│   ├── figures/      # Generisani grafikoni
│   └── metrics/      # Rezultati evaluacije modela
│
├── .gitignore
├── README.md
└── requirements.txt
```

## Organizacija eksperimenata

Notebookovi su organizovani u dva direktorijuma, prema klasifikacionom problemu:

- `notebooks/function/` – klasifikacija prema biološkoj funkciji.
- `notebooks/localization/` – klasifikacija prema subcelularnoj lokalizaciji.

U oba direktorijuma notebookovi su organizovani prema sljedećem redoslijedu:

| Notebook | Opis |
|---|---|
| 01 | Preuzimanje i čišćenje podataka |
| 02 | Eksploratorna analiza podataka |
| 03 | Ekstrakcija klasičnih reprezentacija |
| 04 | Klasični ML modeli – SLC |
| 05 | Ekstrakcija ESM-2 embedinga |
| 06 | Modeli dubokog učenja – SLC |
| 07 | Klasični ML modeli – MLC |
| 08 | Modeli dubokog učenja – MLC |
| 09 | Evaluacija i poređenje rezultata |

Notebookove je potrebno izvršavati redom, zasebno za svaki klasifikacioni problem, jer pojedini koraci generišu podatke i modele koji se koriste u narednim koracima.

## Pokretanje projekta

1. Klonirati repozitorijum.
2. Instalirati potrebne biblioteke navedene u datoteci `requirements.txt`.
3. Pokrenuti notebookove iz direktorijuma `notebooks/function/` ili `notebooks/localization/`, počevši od prvog notebooka.

Originalni podaci preuzimaju se iz UniProt baze, a ostale datoteke generišu se izvršavanjem odgovarajućih notebookova.