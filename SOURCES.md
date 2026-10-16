# Sources, terms and quirks (checked October 2026)

All data comes from official state open-data portals through their public Socrata (SODA) APIs. No website scraping. The portals' robots.txt allow `/resource/`, and we pace at about 1 request/second (Crawl-delay 1).

| State | Dataset (publisher) | API endpoint | License / terms | Freshness | Quirks |
|---|---|---|---|---|---|
| Colorado | Business Entities in Colorado (Colorado Dept. of State) | https://data.colorado.gov/resource/4ykn-tg5h.json | Public Domain (dataset). Portal terms (https://data.colorado.gov/terms) require the disclaimer reproduced in README | Daily | All statuses; future-effective filings appear once effective |
| Connecticut | Business Registry – Business Master (Secretary of the State) | https://data.ct.gov/resource/n7gp-d28j.json | Public Domain (dataset); portal terms https://data.ct.gov/terms (as-is) | Daily | Rejected filings excluded; NAICS where filed. Business email and owner-demographic columns not used |
| New York | Active Corporations (NYS Dept. of State) | https://data.ny.gov/resource/n9v6-gdp6.json | OPEN-NY Terms of Use (free reuse incl. commercial): https://data.ny.gov/en/dataset/OPEN-NY-Terms-Of-Use/77gx-ii52 | Daily in practice | Active entities only. When no physical location is filed, city/state/ZIP come from the service-of-process address (street and addressee not used) |
| Oregon | Active Businesses – ALL (Oregon Secretary of State) | https://data.oregon.gov/resource/tckn-sxa6.json | Public domain per ORS 276A.368, no warranty | Weekly | One row per associated name/address; merged to one row per registry number. DBAs, reserved and registered names excluded. Registered agent kept only if an organization |
| Pennsylvania | Registered Businesses in PA (PA Dept. of State) | https://data.pa.gov/resource/xvd7-5r2c.json | "Public Domain U.S. Government"; data policy https://data.pa.gov/data-policy (free, without restriction) | About every 1–2 weeks | The file repeats each business once per officer/organizer; only entity columns are requested and grouped, so one row per filing number |
| Texas | Active Franchise Taxpayers (Texas Comptroller of Public Accounts) | https://data.texas.gov/resource/9cir-efmm.json | Comptroller policy: "Information on CPA's sites is public domain" (https://comptroller.texas.gov/about/policies/privacy.php) | Weekly; new charters appear ~3–5 weeks after the charter date | Franchise-tax roll, SOS-registered entities only (record types U/V); person-type taxpayers excluded; taxpayer street line not used |

States not included: Florida's official bulk files are "for informational purposes" with no open API. Delaware, Nevada and most other states publish no entity-registration dataset on an open-data API.

How this sample was drawn: for each day Sep 14–20, 2026, the first 29 entities by state ID with that formation date (Pennsylvania de-duplicated server-side). Rows missing an ID or name were dropped.
