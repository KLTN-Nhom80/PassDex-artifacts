# Measurements on the deployed site (https://passdex.site)

Release v1.0.2 (20 Nov 2026), v1.0.3 (21 Nov 2026) and v1.0.4 (22 Nov 2026) on one AWS EC2 t3.xlarge (4 vCPUs, 16 GB). All runs came from one
client in Vietnam over the internet, so the times include the network.

| File | Measurement |
|---|---|
| `latency-sequential-2026-11-20.json` | 30 requests per endpoint, 320 ms apart: p50, p90, p95 per endpoint |
| `load-browse-2026-11-20.json` | Closed-loop read-only browsing (search → filter → listing page, 1 s pause) at 10, 50, 100 and 200 virtual users, 60 s each: 37,674 requests, no errors |
| `photo-to-draft-concurrent-2026-11-21.csv` | 3, then 5 photos sent at the same moment from different accounts. Seconds from the start of the upload to a filled draft, and which fields were filled. The backend ran one photo analysis at a time |
| `photo-to-draft-concurrent-2026-11-22.csv` | The same eight photos and rounds, with 1, 2 and 3 photo analyses allowed at a time (`analyses_at_once`; level 1 on v1.0.3, levels 2 and 3 on v1.0.4, which run the same photo-analysis code; v1.0.4 adds the setting and raises the model memory limit from 4 to 6 GB). Gemini used one paid key only. Last of five drafts ready after 57.8, 36.5 and 28.2 s; no errors; the same grades and series names at every level |
| `search-by-photo-2026-11-21.csv` | Search by photo on three photos of Conan books: who read the title (local gallery or Gemini), time, catalog match, active listings returned |

The photos are the team's own. Account names, upload URLs and full responses are left out.
