# similarita

`similarita` is a small browser app that compares words by two metrics:

- **Graphic similarity** — normalized Levenshtein distance for plain text.
- **Phonetic similarity** — normalized weighted distance for IPA tokens.

## Features

- Graphic similarity calculator.
- Phonetic similarity calculator for IPA strings.
- Optional explanation modal with formulas and intermediate data.
- Light/dark theme toggle with saved preference.

## How scoring works

### 1) Graphic similarity

Base score:

```text
1 - (Levenshtein distance / max length)
```

### 2) Phonetic similarity

- Input is tokenized with support for multi-character IPA symbols.
- Weighted substitution cost is used for selected similar sounds.
- Result is normalized by max token length.

## Run locally

This is a static app, so you can simply open `index.html` in a browser.

If you prefer a local server:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.


## Notes

- Theme preference is stored in `localStorage` under key `similarita.theme`.
- Calculators require both fields to be filled in.
