# PassDex: test and evaluation artifacts

Supplementary material for the paper *PassDex: Photo-Based Listing Assistant for Second-Hand Books Using Local Models and
the Gemini API* (SSRC 2026). It holds the full test-case tables behind Tables V and VI, the measurements on the deployed
site behind Table IV, and the hand check of the automatic series-name scorer (Section IV).

The application source and the listing photos are not published here: the photos belong to their sellers.

| Folder | Paper | Content |
|---|---|---|
| `testing/functional-acceptance/` | Tables V and VI | All functional acceptance cases: 225 whole-system cases (11 Nov 2026) and 202 administration cases (first run 14 Nov, after fixes 16 Nov) |
| `testing/deployed-site/` | Table IV, Section III | Sequential latency and read-only load test (20 Nov 2026); photo-to-draft with 3 and 5 drafts sent at the same moment, and search by photo (21 Nov 2026), on https://passdex.site |
| `evaluation/series-name-scoring/` | Section IV, *Automatic scoring* | Every series-name answer that the automatic scorer accepts only through a loose rule, with a category read by hand |

Each folder has its own README. Case descriptions in the test tables are in Vietnamese, as they were written and run.
