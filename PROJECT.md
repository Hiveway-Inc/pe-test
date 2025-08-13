Great brief. Here’s a compact, ready-to-run structure for a 30–45 minute prompt‑engineering exercise that hits your three phases (Explore → Plan → Execute), keeps everything local, and lets you evaluate how well candidates use AI to think, plan, and build.

⸻

1) Assessment structure (30–45 minutes)

Phase 1 — EXPLORE (8–10 min)
Goal: show how they use AI to extract requirements from messy inputs.
Candidate outputs:
	•	A one‑page “clarified requirements” note with: assumptions, open questions, acceptance criteria, and 6–8 edge cases.
	•	A short “prompt log” (3–5 prompts they used, each with a 1‑line purpose).

Phase 2 — PLAN (8–10 min)
Goal: see decomposition + prompt design.
Candidate outputs:
	•	A minimal build plan (steps, function list, data shapes).
	•	A prompt template (or two) they’d reuse for coding/tests (“Write a CLI function that… format your answer as…”).
	•	Test plan: 5–7 test cases tied to acceptance criteria.

Phase 3 — EXECUTE (15–25 min)
Goal: deliver a small working tool with at least one iteration.
Candidate outputs:
	•	A tiny CLI or notebook that reads local files, processes them, and writes results.
	•	A short README with how to run it, decisions made, and one “we improved it by…” iteration note.
	•	Final artifacts (e.g., results.csv + summary.md).

Scoring rubric is below; first, here’s a complete scenario you can hand candidates.

⸻

2) Scenario A (recommended): Discount Engine Validator

(Fits a lot of real‑world prompting: ambiguity handling, I/O design, test coverage, and edge‑case thinking.)

Candidate brief (handout)

Business sketch
You’re shipping a tiny coupon application tool that evaluates whether a coupon should apply to an order and what the final price should be. It runs locally (no APIs), reads a CSV of orders and a JSON of coupon definitions, and produces both a results.csv and a human‑readable summary.md.

Files given to the candidate (you provide these locally):
	•	orders.csv (sample below)
	•	coupons.json (sample below)
	•	messy_notes.txt (stakeholder notes below)

What to build
	1.	CLI or notebook that:
	•	Reads orders.csv and coupons.json.
	•	For each order, decides whether the coupon applies; computes discount; outputs:
	•	order_id, original_total_cents, discount_cents, final_total_cents, status, reason
	•	Writes a summary.md with: totals, counts by status (applied | rejected | invalid | expired | none), and any anomalies.
	2.	Rounding/precision: use cents (integers). For % discounts, round to nearest cent.
	3.	Statuses:
	•	applied: coupon valid and applied.
	•	rejected: coupon present but not applicable (e.g., min total not met).
	•	invalid: coupon code not found.
	•	expired: coupon found but expired.
	•	none: no coupon provided.
	4.	Deliverables: the tool, results.csv, summary.md, and a short DECISIONS.md that lists assumptions.

Constraints
	•	Python or Node preferred. No external APIs.
	•	You may use AI to plan, code, and test—but keep a short prompt log.

⸻

orders.csv (sample data)

order_id,customer_id,total_cents,created_at,coupon_code
1001,C001,2500,2025-08-13T09:01:00Z,WELCOME10
1002,C002,900,2025-08-13T09:05:00Z,5OFF
1003,C003,12000,2025-08-13T09:20:00Z,5OFF
1004,C001,199,2025-08-13T09:40:00Z,WELCOME10
1005,C004,5000,2025-08-13T10:00:00Z,HALFPAST
1006,C005,75,2025-08-13T10:10:00Z,
1007,C006,350,2025-08-13T10:15:00Z,BOGUS
1008,C007,1000,2025-08-13T10:30:00Z,HALFPAST
1009,C008,499,2025-08-13T10:45:00Z,5OFF
1010,C009,200,2025-08-13T11:00:00Z,WELCOME10
1011,C010,60,2025-08-13T12:00:00Z,HALFPAST

coupons.json

[
  {"code": "WELCOME10", "type": "percent_off", "percent": 10, "expires_at": "2025-12-31T23:59:59Z"},
  {"code": "5OFF", "type": "amount_off", "amount_cents": 500, "min_total_cents": 1000, "expires_at": "2025-08-31T23:59:59Z"},
  {"code": "HALFPAST", "type": "percent_off", "percent": 50, "expires_at": "2025-08-15T00:00:00Z"}
]

messy_notes.txt (intentionally ambiguous)

- Only ONE coupon per order. No stacking.
- Apply coupon to ORDER TOTAL (ignore taxes for now).
- Stripe min charge is $0.50. If final total < $0.50, we *might* allow free checkout to reduce friction,
  OR we could block checkout and ask for top-up… let's decide later.
- Percent coupons: cap at 100%. Amount coupons: cents. Never negative totals.
- Expiry is exclusive at the second? (e.g., expires at timestamp is last valid moment?)
- Some coupons require a minimum total (e.g., 5OFF requires $10+).
- Rounding: use cents. For % discounts, round to nearest cent. (Banker’s vs half-up? TBD)
- Invalid coupon codes should not fail the order; just mark them.
- Currencies: USD only for this tool.
- We'll want a summary of outcomes + any anomalies (e.g., invalid codes, expired coupons, totals < $0.50).


⸻

What success looks like (for the candidate)
	•	Explore: a crisp list of requirements, assumptions (e.g., “If final < $0.50 → treat as free and set final to 0”), and acceptance criteria.
	•	Plan: a short step list, function signatures, and 5–7 tests tied to criteria.
	•	Execute: a working tool that runs on the sample files, plus results.csv and summary.md, and at least one round of prompt‑driven improvement (documented).

⸻

3) Scoring rubric (100 points)

A. Prompting & Iteration (35 pts)
	•	Context packed into prompts; constraints & formats specified (10)
	•	Iterative refinement (show at least one critique/rewrite) (10)
	•	Prompt templates with variables/placeholders (5)
	•	Verifies AI output; spots mistakes, asks for fixes (10)

B. Technical Correctness & Design (35 pts)
	•	Correct application of coupons incl. min_total, expiry, rounding (15)
	•	Clean I/O (reads CSV/JSON, writes results & summary) (8)
	•	Clear structure (functions, small surface area) (6)
	•	Tests or demonstrable checks matching acceptance criteria (6)

C. Requirements & Planning (20 pts)
	•	Extracts unambiguous acceptance criteria (8)
	•	Identifies key edge cases & risks (6)
	•	Makes and documents sensible assumptions (6)

D. Communication & Hygiene (10 pts)
	•	README with run instructions & decisions (5)
	•	Short prompt log; concise commit messages or change notes (5)

Pass threshold suggestion: 70. Strong hire: 85+ with evidence of iteration and sound assumptions.

⸻

4) Proctor key (expected results on the sample data)

(Don’t give this to candidates.)
Assuming:
	•	Expiry is inclusive up to the expires_at instant (i.e., not expired if created_at < expires_at).
	•	If final total would fall below $0.50, treat as free (final = 0; status = applied; reason includes free_below_min_charge).
	•	Rounding: nearest cent.

Expected outcomes:

order_id	code	status	discount_cents	final_total_cents	reason
1001	WELCOME10	applied	250	2250	percent_off 10
1002	5OFF	rejected	0	900	min_total_not_met
1003	5OFF	applied	500	11500	amount_off 500
1004	WELCOME10	applied	20	179	percent_off 10
1005	HALFPAST	applied	2500	2500	percent_off 50
1006	(none)	none	0	75	no_coupon
1007	BOGUS	invalid	0	350	code_not_found
1008	HALFPAST	applied	500	500	percent_off 50
1009	5OFF	rejected	0	499	min_total_not_met
1010	WELCOME10	applied	20	180	percent_off 10
1011	HALFPAST	applied	30	0	free_below_min_charge (50% of 60 = 30)

If you prefer to block < $0.50 instead: set 1011 → rejected with below_min_charge.

⸻

5) What you’re actually measuring
	•	Prompt discipline: Do they pack the right context, constraints, examples, and output formats into prompts? Do they iterate intelligently?
	•	Judgment under ambiguity: Do they call out contradictions and make defensible assumptions quickly?
	•	Scoping: Do they size the solution to fit the clock, not boil the ocean?
	•	Engineering hygiene: Simple I/O, testable units, clear run instructions.
	•	Self‑review: At least one deliberate improvement pass driven by an AI critique.

⸻

6) Two alternative scenarios (swap‑ins)

B) Log Anomaly Sniffer (Azure/Stripe‑ish)
	•	Inputs: small events.jsonl (20–40 lines of mixed info|warn|error), plus messy rules (“errors within 2m of a deploy are ‘hot’; duplicate event_ids are anomalies”).
	•	Output: report.md + alerts.json with matches.
	•	Same three phases and rubric.

C) FAQ Summarizer & Gap Finder
	•	Inputs: 6–8 short FAQ markdown files with overlaps/gaps and a messy product note.
	•	Task: generate a single canonical_faq.md + gaps.md + prompt_templates.md for future Q&A generation.
	•	Measures prompt structure, synthesis, and format control.

⸻

7) Logistics & admin tips
	•	Timeboxing: Put a visible timer per phase. Encourage shipping even if imperfect.
	•	Environment: Let them pick Python or Node. Provide a minimal starter folder, but no code—you want to see their prompting.
	•	Artifacts to collect: code folder, README, results.csv, summary.md, DECISIONS.md, prompt_log.md.
	•	Interview follow‑up (5–10 min): Ask which prompt made the biggest difference and why; what they’d do with 30 more minutes.

⸻

8) Want me to package this for you?

I can generate a downloadable kit (folders/files ready to hand to candidates) including:
	•	/candidate → README.md, orders.csv, coupons.json, messy_notes.txt
	•	/proctor → rubric, expected results, sample grading sheet
	•	Blank prompt_log.md, DECISIONS.md templates

Tell me which scenario (A, B, or C) you want and the preferred language (Python or Node). I’ll build the kit and give you download links.