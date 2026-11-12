# CSLR Polito 2026: manuale di Cybersecurity Laws and Regulations

Manuale in LaTeX, scritto da studenti, del corso **Cybersecurity Laws and Regulations** (Politecnico di Torino,
A.A. 2026/27, Prof. Giuseppe Vaciago; laboratori con Gianluca Gilardi). Copre GDPR e data breach, ISO/IEC 27001 e
risk management, Cyber Resilience Act, Cybersecurity Act, NIS2, DORA e AI Act. Si aggiorna lezione per lezione.

> ⚠️ **Non è materiale ufficiale.** Sono appunti rielaborati: possono contenere errori. Per l'esame fanno fede le
> slide, i testi normativi e le indicazioni del docente. Le parti aggiunte da noi, cioè non dette a lezione e non
> presenti nelle slide, sono sempre in un riquadro viola **"Integrazione – non dal corso"**. I punti incerti sono
> nei riquadri arancioni **"Da verificare"**.

## Struttura del repository

```
CSLR_Polito_2026/
├── README.md
├── .gitignore              whitelist: entrano solo i sorgenti .tex (e latexmkrc)
└── manuale/
    ├── main.tex            documento principale: ordine delle parti e degli \input
    ├── preambolo.tex       pacchetti, riquadri (esame, integrazione, verifica, …), macro
    ├── premessa.tex        "Come leggere questo manuale": legenda e fonti
    ├── latexmkrc           configurazione di latexmk (output in build/)
    ├── lezioni/            Parte I  – Diario: una lezione per file, AAAA-MM-GG.tex (+ _template.tex)
    ├── manuale/            Parte II – Manuale: un capitolo per norma, 01-introduzione … 09-csa
    ├── laboratori/         Parte III – Laboratori: lab-NN-nome.tex
    ├── ripasso/            Parte IV – Schemi di ripasso: scadenze, mappe, schede
    ├── esame/              Parte V – Quiz ed esame: formato, tema precedente, simulazioni, quiz
    └── appendice/          Glossario e acronimi
```

### Le parti del manuale

| Parte | Contenuto |
|---|---|
| **Diario delle lezioni** | Cronaca lezione per lezione: sintesi, avvisi pratici, contenuti, punti segnalati per l'esame. Serve a seguire il corso in tempo reale. |
| **Manuale del corso** | Un capitolo per norma che unisce lezioni, slide e testi normativi, con rimandi al diario. |
| **Laboratori** | I casi del venerdì: contesto, consegna, metodo (es. severità ENISA, risk register, audit CRA), soluzione ragionata. |
| **Schemi di ripasso** | Tabella comparativa delle notifiche, mappe concettuali, schede. |
| **Quiz ed esame** | Formato dell'esame, tema precedente, simulazioni, quiz per argomento con soluzioni e rimando alla lezione. |
| **Appendice** | Glossario e acronimi. |

### Riquadri (definiti in `preambolo.tex`)

| Riquadro | Uso |
|---|---|
| `esame` (rosso) | punto indicato dal docente come rilevante per l'esame |
| `integrazione[titolo]` (viola) | contenuto aggiunto dai redattori, **non dal corso** |
| `verifica` (arancione) | informazione non confermata: da controllare |
| `nota[titolo]` (grigio) | nota generica, fonti |
| `soluzione[titolo]` (verde) | soluzioni di quiz, simulazioni, lab |
| `\dacompletare{…}` (giallo) | parte ancora da scrivere |
| `\lezione{data}{titolo}{docenti}{argomenti}` | intestazione di una voce del diario |
| `domanda[tema]` + `opzioni`, `\rif{AAAA-MM-GG}{GG/MM}` | domande dei quiz e rimando cliccabile alla lezione |

## Copertura attuale

15 lezioni, dal 21/09 al 09/11/2026, tutte nel diario, inclusi i 4 laboratori.

| Data | Argomento |
|---|---|
| 21/09 | Lezione introduttiva: i regimi del corso, approccio basato sul rischio |
| 25/09, 28/09 | GDPR: ruoli, principi, basi giuridiche, diritti, accountability, art. 32, DPIA |
| 02/10 | Severity assessment ENISA (simulazione) |
| 05/10 | DPIA e data breach (artt. 33–34) |
| 09/10 | Lab 1: caso Arvenza (data breach) |
| 12/10 | Debrief del Lab 1, introduzione a ISO/IEC 27001 |
| 16/10 | Lab 2: caso Sylvane Retraite (severità, notifica) |
| 19/10, 23/10 | ISO/IEC 27001: clausole, Annex A, controlli 8.x |
| 26/10 | Risk management ISO, introduzione al CRA |
| 30/10 | Lab 3: risk register ISO 27001 |
| 02/11 | CRA e simulazione Pulse K (CRA + GDPR) |
| 06/11 | Lab 4: conformity audit CRA (Sestante Mobility) |
| 09/11 | Hard e soft law; Cybersecurity Act |

NIS2, DORA e AI Act non sono ancora stati trattati a lezione. I loro capitoli contengono per ora un inquadramento,
quasi tutto in riquadri `integrazione`.

## Come compilare

**In locale (macOS):**

```sh
brew install --cask mactex-no-gui            # una volta (~5 GB; chiede la password)
eval "$(/usr/libexec/path_helper)"           # oppure riapri il terminale
cd manuale && latexmk                        # PDF in manuale/build/main.pdf
```

`latexmkrc` imposta pdfLaTeX e la cartella `build/`, che è esclusa da git. Alternativa leggera senza installare
MacTeX: `brew install tectonic`, poi `cd manuale && tectonic -X compile main.tex --outdir build` (scarica i
pacchetti al primo avvio). Come editor vanno bene VS Code con
l'estensione *LaTeX Workshop* oppure TeXShop. Su Linux si usa TeX Live (`texlive-full`), su Windows MiKTeX.

**Su Overleaf:** crea uno zip della cartella `manuale/`, poi *New Project → Upload Project*. Il documento principale
è `main.tex`.

## Pipeline di lavoro

Il manuale nasce dalle registrazioni delle lezioni:

```
registrazione → audio ottimizzato per ASR → trascrizione (Whisper) → bozza LaTeX → revisione → commit
```

1. **Audio:** si estrae dal video l'audio in FLAC mono a 16 kHz, con filtro passa-alto, riduzione del rumore e
   normalizzazione (ffmpeg).
2. **Trascrizione:** si usa Whisper `large-v3-turbo` (mlx-whisper, in locale su Apple Silicon). Si correggono i loop
   del modello, si tolgono i riempitivi e le parti non utili (pause, prove microfono).
3. **Diario:** per ogni lezione si scrive una voce `lezioni/AAAA-MM-GG.tex` dalla trascrizione, confrontata con le
   slide. Numeri, date e articoli si prendono **sempre** dalle slide o dai testi normativi, perché la trascrizione su
   questi punti è inaffidabile.
4. **Manuale, laboratori, ripasso, quiz:** si aggiornano i capitoli per norma partendo da diario, slide e materiale.
   Ciò che non viene dal corso va nei riquadri `integrazione`.
5. **Controllo:** il documento deve compilare senza errori né riferimenti indefiniti. Si rilegge, poi si fa commit e
   push.

**Registrazioni, audio, trascrizioni, slide e materiale del docente non sono e non saranno nel repository**, per
il diritto d'autore dell'ateneo e del docente. Restano solo sul computer di chi cura la pipeline. Il `.gitignore`
lascia entrare solo i sorgenti `.tex`.

## Come contribuire

- Correzioni e aggiunte sono benvenute: crea un branch (`git checkout -b fix/gdpr-art6`), fai le modifiche, compila,
  apri una pull request. Per una segnalazione rapida basta una *issue*.
- **Nuova lezione:** copia `lezioni/_template.tex` in `lezioni/AAAA-MM-GG.tex` e aggiungi
  `\input{lezioni/AAAA-MM-GG}` in `main.tex`, in ordine cronologico.
- Scrivi in italiano. Sintassi LaTeX: `art.~33`, virgolette ``` ``…'' ```.
- Segnala sempre la fonte. Ciò che non viene da lezioni o slide va in `integrazione`, i dubbi in `verifica`.
- Non caricare slide, PDF del corso, registrazioni o trascrizioni. Non scrivere nomi di altri studenti né voti.
