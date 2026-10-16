# US new business filings: free weekly sample from official state open data

A free, small sample of **newly registered US businesses** (LLCs, corporations, partnerships, nonprofits) from six official state open-data portals: **Colorado, Connecticut, New York, Oregon, Pennsylvania and Texas**. All six are normalized into **one shared schema**.

- `data/2026-09-14_to_2026-09-20/<STATE>.csv`: entities formed in the week of Sep 14–20, 2026. There are up to 200 per state (about 29 per day), 1,145 rows in total. Oregon has 145, because its file has one row per associated address and the per-day cap trimmed it.
- `SOURCES.md`: the exact dataset for each state, its publisher, license or terms, refresh lag, and quirks.
- No login, no sign-up. Plain CSV with a UTF-8 header row.

> **Disclosure:** this repo is published by **CPT Engineering PLLC**, which also sells an automated, scheduled version of the same data on Apify (link below). The sample here is free to use.

## Schema

| Column | Meaning |
|---|---|
| `state` | Two-letter state the record comes from |
| `entity_id` | The state's own ID (SOS file number, DOS ID, registry number, etc.) |
| `entity_name` | Registered business name, as filed |
| `entity_type` | Normalized: `LLC`, `CORPORATION`, `PARTNERSHIP`, `NONPROFIT`, `OTHER` |
| `entity_type_raw` | The state's own type label or code |
| `domestic` | `True` if formed in that state, `False` if a foreign registration |
| `jurisdiction_of_formation` | State/country of formation, where published |
| `status` | Status as published (several states publish active entities only) |
| `formation_date` | Formation or registration date (YYYY-MM-DD) |
| `principal_city`, `principal_state`, `principal_zip` | Principal office city/state/ZIP (**no street line**) |
| `county` | County, where published (NY, PA) |
| `naics`, `naics_description` | Industry code, where published (CT) |
| `registered_agent_organization` | Registered agent **only when it is an organization** (CO, OR) |
| `record_url` | Link to the state's own record, where available (OR) |
| `source_dataset_url` | The official dataset the row came from |

## What is deliberately *not* here

Entity-level fields only. **No personal names** (members, managers, officers, organizers, incorporators, individual registered agents, service-of-process addressees). No street addresses, emails, phone numbers or owner-demographic flags. Those columns are not requested from the states at all. Also excluded:
- Oregon assumed business names (DBAs), which are often sole proprietors.
- Texas sole proprietorships and general partnerships of individuals.

A business *name* can still contain a person's name (for example "Smith Consulting LLC"), because that is the registered name of the entity.

## How many new businesses per week?

Distinct new entities by formation date in each official dataset. These are counts, queried Oct 16, 2026:

| State | Week of 2026-09-14 | Week of 2026-09-21 | Week of 2026-09-28 | Week of 2026-10-05 |
|---|---|---|---|---|
| CO | 3,311 | 3,363 | 3,316 | 3,351 |
| CT | 1,233 | 1,181 | 1,210 | 1,106 |
| NY | 5,072 | 5,023 | 4,866 | 5,059 |
| OR | 1,442 | 1,406 | 1,507 | 1,436 |
| PA | 2,399 | 2,419 | 1,489 | 0 |
| TX | 9,864 | 8,132 | 196 | 21 |
| **Total** | **23,321** | **21,524** | **12,584** | **10,973** |

The last two weeks are low for **Texas and Pennsylvania** only because those publishers post late (TX ~3–5 weeks, PA ~2 weeks). Complete weeks run at about **21,000–23,000 new entities a week** across the six states.

## Caveats

- This is a **sample**, not a complete register. Check the official source before relying on any record.
- States publish on their own schedules, and some publish active entities only (NY, OR, PA, TX), so dissolved-in-the-same-week filings may be missing.
- Data is as published, with no enrichment.
- Not affiliated with, endorsed by, or sponsored by any state government.

## Want it daily or for other dates?

The full feed runs on Apify as a pay-per-result Actor: all six states, any date range, deduped across scheduled runs, plus lookup by name or state ID. It costs $3 per 1,000 records.
**https://apify.com/cpt_engineering/us-business-registrations-open-data**

You can also query each state's official API yourself. The endpoints are in `SOURCES.md`.

## License

- Our normalization and compilation in this repo: **CC0 1.0** (see `LICENSE`).
- The underlying records stay subject to each publisher's terms, which are summarized in `SOURCES.md`. All six allow reuse, including commercial use.

## Source data disclaimer (required by the State of Colorado)

The data made available here has been modified for use from its original source, which is the State of Colorado. THE STATE OF COLORADO MAKES NO REPRESENTATIONS OR WARRANTY AS TO THE COMPLETENESS, ACCURACY, TIMELINESS, OR CONTENT OF ANY DATA MADE AVAILABLE THROUGH THIS SITE. THE STATE OF COLORADO EXPRESSLY DISCLAIMS ALL WARRANTIES, WHETHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF MERCHANTABILITY, OR FITNESS FOR A PARTICULAR PURPOSE. The data is subject to change as modifications and updates are complete. It is understood that the information contained in the Web feed is being used at one's own risk.

## Contact

Corrections or questions: open an issue, or email cpt-datatools@mail.grokbot.com.
