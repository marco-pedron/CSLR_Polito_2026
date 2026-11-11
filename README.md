# Manuale CSLR — Cybersecurity Laws and Regulations (PoliTo, A.A. 2026/27)

Compilare `main.tex` (pdfLaTeX). Su Overleaf: *New Project → Upload Project* e caricare lo zip.

## Struttura

| Cartella   | Contenuto                                                          |
|------------|--------------------------------------------------------------------|
| `lezioni/` | Diario: una lezione per file, `AAAA-MM-GG.tex`, ordine cronologico |
| `manuale/` | Capitoli tematici, scritti a partire da slide e diario             |
| `ripasso/` | Tabella delle scadenze, mappe concettuali, schede                  |
| `esame/`   | Formato dell'esame, tema precedente, simulazioni, quiz             |

## Aggiungere una lezione

1. Copia `lezioni/_template.tex` in `lezioni/AAAA-MM-GG.tex`.
2. Aggiungi `\input{lezioni/AAAA-MM-GG}` in `main.tex`, sotto le lezioni precedenti.

## Riquadri disponibili (definiti in `preambolo.tex`)

- `esame`: ciò che il docente ha indicato come rilevante per l'esame
- `nota[titolo]`: nota generica
- `verifica`: informazioni non confermate o calcolate, da controllare
- `soluzione[titolo]`: soluzioni di quiz e simulazioni
- `\dacompletare{...}`: segnaposto per parti da scrivere
- `\lezione{data}{titolo}{docenti}{argomenti}`: intestazione di una lezione
- `domanda[tema]` + `opzioni`: domande dei quiz
