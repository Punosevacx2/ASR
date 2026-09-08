# Uticaj kvantizacije i veličine modela na brzinu i tačnost transkripcije srpskog govora

Istraživački projekat koji ispituje kako veličina Whisper modela i tip kvantizacije utiču na performanse automatskog prepoznavanja govora (ASR) na srpskom jeziku.

## Opis

Eksperiment koristi **Mozilla Common Voice 25.0** srpski test skup i **faster-whisper** biblioteku za pokretanje transkripcije na CPU-u. Testira se 6 kombinacija modela i kvantizacije, a mere se dve metrike:

- **WER** (Word Error Rate) — stopa greške na nivou reči u poređenju sa referentnim transkriptom
- **RTF** (Real-Time Factor) — odnos između vremena transkripcije i trajanja audio snimka (RTF < 1 = brže od realnog vremena)

### Testirane kombinacije

| Model  | Kvantizacija |
|--------|-------------|
| tiny   | int8        |
| tiny   | float32     |
| base   | int8        |
| base   | float32     |
| small  | int8        |
| small  | float32     |

### Rezultati

| Model | Kvantizacija | WER    | RTF    |
|-------|-------------|--------|--------|
| tiny  | int8        | 1.1284 | 0.1160 |
| tiny  | float32     | 1.1014 | 0.1554 |
| base  | int8        | 1.0811 | 0.1379 |
| base  | float32     | 1.0676 | 0.2193 |
| small | int8        | 1.0608 | 0.2532 |
| small | float32     | 1.0676 | 0.3476 |

Svi modeli rade brže od realnog vremena (RTF < 1). Veći modeli postižu bolji WER, ali sporiji RTF. `small/int8` pruža najbolji kompromis između tačnosti i brzine.

## Struktura projekta

```
drugiProjekatZvuk/
├── Untitled.ipynb          # Glavna Jupyter sveska sa eksperimentom
├── rezultati.png           # Vizualizacija WER i RTF rezultata
├── requirements.txt        # Python zavisnosti
├── data/                   # Dataset (nije u git tracking-u)
│   └── cv-corpus-25.0-2026-03-09/sr/
│       ├── test.tsv        # Test skup sa putanjama i referencama
│       └── clips/          # MP3 audio snimci
└── venv/                   # Python virtuelno okruženje
```

## Instalacija

### Preduslovi

- Python 3.9+
- pip

### Koraci

```bash
# Kloniraj repozitorijum
git clone <repository-url>
cd drugiProjekatZvuk

# Kreiraj i aktiviraj virtuelno okruženje
python -m venv venv
source venv/bin/activate        # Linux/macOS
# venv\Scripts\activate         # Windows

# Instaliraj zavisnosti
pip install -r requirements.txt
```

## Podaci

Projekat koristi **Mozilla Common Voice 25.0** srpski jezički korpus. Dataset nije uključen u repozitorijum zbog veličine.

1. Preuzmi srpski deo dataseta sa [Common Voice](https://commonvoice.mozilla.org/sr/datasets)
2. Raspakuj u `data/cv-corpus-25.0-2026-03-09/sr/`

## Pokretanje

Pokreni Jupyter Notebook i izvršavaj ćelije redom:

```bash
jupyter notebook Untitled.ipynb
```

Eksperiment ce automatski:
1. Učitati test skup (1430 snimaka) i uzeti uzorak od 30
2. Za svaku od 6 kombinacija pokrenuti transkripciju
3. Izračunati WER i RTF
4. Prikazati i sačuvati grafik u `rezultati.png`

## Tehnologije

- [faster-whisper](https://github.com/SYSTRAN/faster-whisper) — optimizovana CTranslate2 implementacija OpenAI Whisper modela
- [jiwer](https://github.com/jitsi/jiwer) — izračunavanje WER metrike
- [PyAV](https://github.com/PyAV-Org/PyAV) — čitanje trajanja MP3 fajlova
- [Hugging Face Datasets](https://huggingface.co/docs/datasets) — učitavanje dataseta
- [pandas](https://pandas.pydata.org/) — obrada tabularnih podataka
- [matplotlib](https://matplotlib.org/) — vizualizacija rezultata
