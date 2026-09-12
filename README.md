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
