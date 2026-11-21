# Hand check of the automatic series-name scorer

## The scorer

The answer key for a photo is the series name taken from the seller's listing title. A model's reading counts as right
if it matches the key or one of the series' recorded aliases. It also counts as right under three **loose rules**,
applied after both strings are lower-cased and stripped of diacritics, spaces and punctuation:

1. one string contains the other;
2. at least 80% of the words of the shorter string are shared;
3. the edit distance is at most 20% of the longer string.

The loose rules exist because seller titles contain typos and translated titles. They can also accept a reading with
misread letters (for example "Chú Thuat Hai Chien" for *Chú thuật hồi chiến*), or one that names a different book.

## The check

`loose-matches-categorized.csv` lists every answer on the 868 test photos that the scorer accepts only through a loose rule.

| Model | Loose matches |
|---|--:|
| Gemini, pinned run | 40 |
| Qwen2.5-VL-7B | 61 |
| Qwen3.5-9B, run 745 | 51 |
| Qwen3.5-9B, setting B, run 772 | 61 |

Two team members categorized each of the 164 distinct readings **independently and blind to each other**. The second
rater could open the photo.

Columns:
- `method`, `image` (photo id; photos are not shared), `answer_key`, `model_reading`, `rule`;
- `category_rater_1`, `category_rater_2`;
- `note_rater_2` (in Vietnamese).

Categories:

| Category | Meaning |
|---|---|
| A | Correct. Differs only in diacritics, case, punctuation, word order, a known alias or a subtitle, or the seller's title holds the typo |
| B | Right series, misread letters. The seller would have to correct the name |
| C | Wrong: another book or a person's name. The second rater also used C for many misread names |
| D | Cannot be decided |

B and C both count as wrong.

## Result

The raters gave the same right / wrong / undecided judgement on 139 of the 164 readings (84.8%, Cohen's κ = 0.71).

Harm on the 868 test photos, counting a reading wrong if **either** rater judged it wrong. The undecided readings are
counted both ways, which gives the range.

| Model | Judged wrong by either rater | Automatic harm | Corrected harm |
|---|--:|--:|--:|
| Gemini | 6 of 40 | 3.2% | 3.9–4.4% |
| Qwen2.5-VL | 43 of 61 | 20.7% | 25.7–25.8% |
| Qwen3.5-9B (745) | 35 of 51 | 28.6% | 32.6–32.7% |
| Qwen3.5-9B, setting B (772) | 44 of 61 | 24.4% | 29.5–29.6% |

The automatic score therefore favors the local models.
