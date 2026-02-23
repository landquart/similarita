# similarita

`similarita` is a small browser app that compares words by two metrics:

- **Graphic similarity** — normalized Levenshtein distance for plain text.
- **Phonetic similarity** — normalized weighted distance for IPA tokens.

## Features

- Graphic similarity calculator.
- Phonetic similarity calculator for IPA strings.
- Optional explanation modal with formulas and intermediate data.
- Light/dark theme toggle with saved preference.
- Shift-aware bonus score (`shiftSimilarity`) to better handle prefix/suffix offsets.

## How scoring works

### 1) Graphic similarity

Base score:

```text
1 - (Levenshtein distance / max length)
```

Then the app computes `shiftSimilarity` and uses the best value:

```text
final = max(base score, shiftSimilarity)
```

`shiftSimilarity` checks if strings align after a short shift (0..3 symbols)
and gives a bonus score:

- shift 0 -> 1.0
- shift 1 -> 0.5
- shift 2 -> 0.4
- shift 3 -> 0.3

Bonus is applied only when at least 3 starting symbols match after the shift.

### 2) Phonetic similarity

- Input is tokenized with support for multi-character IPA symbols.
- Weighted substitution cost is used for selected similar sounds.
- Result is normalized by max token length.
- `shiftSimilarity` is also applied to token arrays and merged with `max(...)`.

## Run locally

This is a static app, so you can simply open `index.html` in a browser.

If you prefer a local server:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Project structure

- `index.html` — UI, styles, and all JavaScript logic.
- `phonetica.html` — reserved/empty file.

## Notes

- Theme preference is stored in `localStorage` under key `similarita.theme`.
- Calculators require both fields to be filled in.
