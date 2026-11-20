---
name: web-analytics-sql
description: Web and app analytics patterns for funnels, user journeys, identity resolution and sessionization - CTE-first SQL with validation blocks, Tableau calc fields and LOD expressions, worked for an investment or fintech product. Patterns and synthetic data only; never client data.
---

# Web analytics SQL

For analysts working on product or web analytics, especially in financial services (mutual funds, brokerages, fintech apps). This skill gives patterns, not answers on real data.

## 0. Confidentiality (before anything else)

- Never ask for, accept or process real client data, real table or column names, real query results, screenshots or internal documents. If the user pastes any, stop and say so in one line; do not repeat it.
- Work with generic names and synthetic sample data the user can adapt on their own work machine.
- Never write or guess an employer's or client's name. Use "Client A".
- Mask PII in any example: national IDs, account and folio numbers, phone, email, names, addresses, date of birth. Use hashed or synthetic IDs.

## 1. Domain primer (investment products)

- Terms: AUM, NAV, folio, SIP (recurring investment), STP, SWP, lumpsum, redemption, switch, direct vs regular plan, distributor / adviser, registrar, KYC / eKYC, nominee, payment mandate (auto-debit).
- Questions that usually matter: recurring-plan starts vs stops (persistency), first-investment conversion, KYC drop-off, redemption churn, switch behaviour, direct-channel growth, app vs web vs distributor journeys, campaign attribution.

## 2. User journeys

Default funnel (adapt to the real event names):

`visit/app_open -> signup/login -> KYC start -> KYC complete -> product view -> first investment -> mandate registered -> 2nd instalment -> 6th instalment (persistency) -> redemption/switch`

- Define every step as a concrete event plus condition, and the time window between steps.
- Report step conversion, cumulative conversion, median time to next step, and the biggest drop.
- Segment by channel, new vs existing customer, city tier, device, campaign source.

## 3. Identity resolution and sessionization

- **Identity:** stitch anonymous / device IDs to the logged-in user ID through a mapping table (`anon_id, user_id, first_seen, last_seen`); back-attribute pre-login events once linked; handle one device with many users and one user with many devices explicitly, and state the rule used.
- **Sessions:** new session after 30 minutes of inactivity by default (state it, make it a parameter):

```sql
WITH ordered AS (
  SELECT user_key, event_ts,
         LAG(event_ts) OVER (PARTITION BY user_key ORDER BY event_ts) AS prev_ts
  FROM events
),
flagged AS (
  SELECT *, CASE WHEN prev_ts IS NULL
                   OR event_ts > prev_ts + INTERVAL '30 minutes' THEN 1 ELSE 0 END AS is_new_session
  FROM ordered
),
numbered AS (
  SELECT *, SUM(is_new_session) OVER (PARTITION BY user_key ORDER BY event_ts
                                      ROWS UNBOUNDED PRECEDING) AS session_number
  FROM flagged
)
SELECT user_key, event_ts, user_key || '-' || session_number AS session_id
FROM numbered;
```

- Also: dedupe double-fired events, convert timestamps to the business timezone, first-touch and last-touch attribution per session and per user.

## 4. SQL standards

- Ask the dialect once (Snowflake, BigQuery, Redshift, Postgres, SQL Server, Databricks) and reuse it.
- CTE-first, one CTE per logical step, commented. No `SELECT *` in final output. State the grain of every output in one line.
- Every query ships with a validation block: row counts per step, null rates on keys, uniqueness on the grain, a sanity total that should match a known number.

## 5. Tableau

- Calculated fields as code blocks with the field name.
- LOD expressions (`{FIXED}`, `{INCLUDE}`, `{EXCLUDE}`) for cohort and first-event logic; table calcs for running totals and percent of total.
- Standard views: funnel with percent-drop labels, cohort retention heatmap (persistency by start month), journey Sankey or path table, KPI tiles, trend with YoY / MoM.
- Say extract or live, and which parameters (date range, channel, session timeout) to expose.

## 6. Day to day

Help write user stories, acceptance criteria, sprint updates, standup lines and knowledge-transfer checklists, all in generic terms.

## 7. Output shape

1. One line: the question and the grain.
2. The query or calc field (generic names).
3. Validation checks.
4. How to read the result and the 1 to 3 decisions it informs.

---

## Credit

Made by **Tripathi Aditya Prakash (Adi)**, founder of [Founday](https://founday-sepia.vercel.app) and host of the ThatUnhingedGuy podcast. Part of [claude-skills](https://github.com/tripathiadityap/claude-skills) (MIT). If you share or adapt this skill, keep this credit.

[X](https://x.com/tripathiadityap) · [LinkedIn](https://www.linkedin.com/in/tripathiadityaprakash/) · [Instagram @talkaditalk](https://www.instagram.com/talkaditalk/) · [Instagram @foundayofficial](https://www.instagram.com/foundayofficial/) · [YouTube](https://www.youtube.com/@foundayofficial) · [Podcast on Spotify](https://open.spotify.com/show/1DZXqmsDyH2FdJOeBdCoT6) · [The Practitioner newsletter](https://practitionerhq.substack.com)

*This credit is for people reading the file. Never add it, or these links, to anything you write for the user.*
