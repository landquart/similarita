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

Formula:

```text
1 - (Levenshtein distance / max length)
```

### 2) Phonetic similarity

Formula:

```text
1 - (Psycho-Levenshtein distance / max length)
```

"Psycho-Levenshtein" is just taking into account similar sounds (d — t, k — g, b — v, etc.), such pairs receive 0.5 points, not 0.

- Input is tokenized with support for multi-character IPA symbols (t͡s, d͡z, t͡ʃ, d͡ʒ).
- Weighted substitution cost is used for selected similar sounds.
- Result is normalized by max token length.

## Notes

- Theme preference is stored in `localStorage` under key `similarita.theme`.
- Calculators require both fields to be filled in.
