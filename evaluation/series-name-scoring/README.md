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

Two team members rated every reading **independently, without seeing each other's ratings**, and could open the
photo (22 Nov 2026). The categories in these tables are theirs only.

**Two checks.**
1. *Loose rules.* The answers the scorer accepts only through a loose rule, after its alias step rejected them:
   213 answers, 164 distinct readings (`loose-matches-categorized.csv`).
2. *Short names.* The alias step also accepts an answer when one normalized title contains the other: 429 answers in
   the four runs (123, 103, 104, 99). The 110 of them with a string of at most six characters (62 distinct pairs) were
   rated (`short-containment-categorized.csv`). The other 319, with longer strings, were not.

Columns: `method`, `image` (photo id; photos are not shared), `answer_key`, `model_reading`, `rule` or
`shorter_length`, `category_rater_1`, `category_rater_2`.

Categories:

| Category | Meaning |
|---|---|
| A | Correct. Differs only in diacritics, case, punctuation, word order, a known alias or a subtitle, or the seller's title holds the typo |
| B | Right series, misread letters. The seller would have to correct the name |
| C | Wrong: another book or a person's name |
| D | Cannot be decided |

B and C both count as wrong.

## Result

| Check | Distinct readings | Same right / wrong / undecided | Judged wrong by at least one rater |
|---|--:|--:|--:|
| Loose rules | 164 | 147 (89.6%, Cohen's κ = 0.79) | 102 |
| Short names | 62 | 59 (95.2%) | 5 |

Harm on the 868 test photos after both checks, counting a reading wrong if **either** rater judged it wrong. The one
undecided reading is counted both ways, which gives the range for Gemini.

| Model | Automatic harm | Corrected harm |
|---|--:|--:|
| Gemini | 3.2% | 3.6–3.7% |
| Qwen2.5-VL | 20.7% | 25.6% |
| Qwen3.5-9B (745) | 28.6% | 32.9% |
| Qwen3.5-9B, setting B (772) | 24.4% | 29.7% |

An earlier version of this table (21 Nov) used categories proposed by Claude and checked by the first author as rater 1;
it is replaced by these two human ratings.

The automatic score therefore favors the local models.
