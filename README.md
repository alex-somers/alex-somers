------------------------------------------------------------------------------------------------------------------------------------------------

# Me!

DECA President, Young Investment Society CFO, The Unspoken Project Co-Founder and Board Member, Rice Business Case Champion, Eagle Scout, NHS member, National circuit debater, Harvard SA Economics and Finance Scholar, UPenn Wharton YIC Scholar and Competitor, NHS member, Finance Club Member, 300 hours of service, Finance enthusiast.

Currently: leveling the playing field of literacy in finance through Finance for Others (abv. ffo), a non-profit initiative that blends AI with real people to create real results. Read below. 

Building in: .jsx, .tsx, .js, .py 

Socials: --- Insta: @tripp_somers, or @financeforothers. 
         --- LinkedIn: @alexander "tripp" somers, or @Finance for Others, or @Mochi, or @The Unspoken Project.
         --- You've already found the GitHub, good on you!

------------------------------------------------------------------------------------------------------------------------------------------------

# ffo!

Finance for Others is a nonprofit built on a simple idea: understanding money shouldn't depend on who you know or where you grew up. Right now, financial literacy is one of the strongest predictors of long-term stability — but it's also one of the most unevenly taught. Some people grow up with parents who explain credit scores and investing at the dinner table; most people don't.

FFO tries to close that gap in four ways:

Courses — Free, AI-guided lessons on budgeting, credit, investing, and markets, built for people with zero finance background, not people who already speak the language.
The Stock Pitch Challenge — A real competition where student teams research an actual public company, build an investment case, and pitch it live to real analysts and portfolio managers — with prize funding and internship placements for the winners.
Career Connect — Direct partnerships with banks, asset managers, and fintechs, aimed specifically at people who don't have a family connection or a warm introduction into the industry.
Publications & Podcast — Plain-language writing on markets and economics, plus a podcast with long-form interviews with investors and economists, written and produced for people who are new to finance, not just fluent in it.

The throughline across all four: nothing here assumes you already know anything. It's built for the person who's curious about money but has never been handed a way in — and it's all free.

------------------------------------------------------------------------------------------------------------------------------------------------

# forge

An agent framework built around a strict split between how an agent behaves *within* a task (inner loop) and how it improves *across* tasks (outer loop). See `AGENTS.md` for the full philosophy — this README covers the practical side: the agent contract, how to run evals, and what the dashboard shows.

## The outer-loop / inner-loop split

The inner loop is a single agent run: it takes a task, works it, and produces a result. The outer loop sits above that — it's what accumulates memory across runs and feeds it back into future inner loops. Keeping these separate is a deliberate design choice, not an implementation detail; the reasoning for why is written up in full in `AGENTS.md`. Read that before touching either loop.

## The agent contract

Every agent lives in `agents/current/` and is defined by five files. Together, these five files are the contract — an agent isn't "done" until all five exist and agree with each other. Check that directory directly for the current file names and structure; this README won't drift out of sync with the code by trying to restate it here.

## Running evals

Two scripts matter day to day:

```bash
python evals/run_eval.py
```
Runs a single evaluation pass for an agent.

```bash
python evals/learning_curve.py --memory on
python evals/learning_curve.py --memory off
```
Runs the same eval across multiple passes, with the outer-loop memory either enabled or disabled, so you can directly compare an agent with and without memory turned on.

## Dashboard

`dashboard/index.html` is a static file — there's no build step and no server to start. Open it directly in a browser and it reads from the ledger files to show run history and learning curves.

## Does the memory loop actually work?

Pulled straight from `ledger/learning_curves/github_triage_memory_{on,off}.jsonl`:

| Pass | Memory ON (holdout accuracy) | Memory OFF (holdout accuracy) | Memory size (entries) |
|------|-------------------------------|--------------------------------|-------------------------|
| 1    | 28.6%                         | 28.6%                          | 44                       |
| 2    | 42.9%                         | 28.6%                          | 65                       |
| 3    | 35.7%                         | 28.6%                          | 80                       |

Memory-on climbs then dips; memory-off stays completely flat. That's a real signal that memory is *doing something* — but this is a 14-task holdout split, so each task is worth ~7 percentage points. A single task flipping accounts for most of that swing. Treat this as a promising early result, not a validated trend, until it's been run on a larger holdout.

## Known issues

- **`cost_per_task` reads 0.0 across the entire committed ledger.** This is a pricing bug — `PRICING_PER_MTOK` is missing an entry for `claude-sonnet-4-6`. The fix exists on `ao/forge-38/fix-sonnet-4-6-pricing` but hasn't merged yet, so the current ledger predates it. Don't cite the cost numbers in the ledger as evidence of anything until that fix lands and the ledger is regenerated.
- **`coderepair`'s learning-curve ledger files are empty (0 lines).** No full run has happened for that domain yet — there's no data to draw conclusions from there.

------------------------------------------------------------------------------------------------------------------------------------------------
