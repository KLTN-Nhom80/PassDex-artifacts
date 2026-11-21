# Hand check of the automatic series-name scorer

## The scorer

The answer key for a photo is the series name taken from the seller's listing title. A model's reading counts as right
if it matches the key or one of the series' recorded aliases. It also counts as right under three **loose rules**,
applied after both strings are lower-cased and stripped of diacritics, spaces and punctuation:

1. one string contains the other;
2. at least 80% of the words of the shorter string are shared;
3. the edit distance is at most 20% of the longer string.

The loose rules exist because seller titles contain typos and translated titles. They can also accept a reading with
misread letters, or one that names a different book.

## The check

`loose-matches-categorized.csv` lists every test-photo answer (868 photos) accepted only through a loose rule:

| Model | Loose matches |
|---|--:|
| Gemini, pinned run | 40 |
| Qwen2.5-VL-7B | 61 |
| Qwen3.5-9B, run 745 | 51 |
| Qwen3.5-9B, setting B, run 772 | 61 |

Columns: `method`, `image` (photo id, not shared), `answer_key`, `model_reading`, `rule`, `category`.

Each pair was read by hand and given one category:

| Category | Meaning |
|---|---|
| A | Correct. Differs only in diacritics, case, punctuation, word order, a known alias or a subtitle, or the seller's title holds the typo |
| B | Right series, misread letters. The seller would have to correct the name |
| C | Another book, or a person's name |
| D | Cannot be decided without the photo |

## Result

Harm on the 868 test photos. D is counted both ways, which gives the range in the last column.

| Model | A | B | C | D | Automatic | B and C counted as wrong |
|---|--:|--:|--:|--:|--:|--:|
| Gemini | 32 | 0 | 1 | 7 | 3.2% | 3.3–4.1% |
| Qwen2.5-VL | 18 | 36 | 3 | 4 | 20.7% | 25.2–25.7% |
| Qwen3.5-9B (745) | 17 | 32 | 1 | 1 | 28.6% | 32.4–32.5% |
| Qwen3.5-9B, setting B (772) | 19 | 40 | 1 | 1 | 24.4% | 29.1–29.3% |

The automatic score therefore favors the local models. One team member assigned the categories; a second, blind rating
is in progress.
