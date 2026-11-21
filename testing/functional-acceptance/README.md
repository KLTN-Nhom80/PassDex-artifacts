# Functional acceptance test cases

## `whole-system-2026-11-11.csv`

225 cases run on 11 November 2026 against a local copy of the system with external services blocked, through its API
or in a browser.

- Result: 213 passed (`Đạt`), 3 failed (`Không đạt`), 9 not run (`Không kiểm được`).
- Failed cases: T7-05 and T7-12 (search) and N1-31 (an over-long series name).
- Not run: 8 cases need live AI, speech or photo-search services; 1 hit a test-runner timeout.
- Case types (`caseType`): 102 normal (`N`), 72 abnormal (`A`), 51 boundary (`B`). One case of each type writes its type
  in words.
- Group counts (`nhom`) match Table V of the paper.

Main columns:

| Column | Content |
|---|---|
| `ma_ca` | Case id |
| `nhom` | Group |
| `tien_dieu_kien` | Preconditions |
| `buoc_thuc_hien` | Steps |
| `du_lieu` | Input |
| `ket_qua_mong_doi` | Expected result |
| `ket_qua_thuc_te` | Actual result |
| `dat` | Status |
| `bang_chung` | Evidence file in the team's archive |

## `administration-2026-11-16.csv`

202 administration cases. Each row gives the result of the first run (14 Nov: 152 passed, 50 failed) next to the result
of the verified run after the fixes (16 Nov: 202 passed).

Accounts and data in both tables are synthetic; emails use `example.test`.
