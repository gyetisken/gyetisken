# Gökhan Yetişken

Senior software engineer with 11 years building and modernizing enterprise systems, primarily for U.S. bar admissions and professional licensing organizations. My work covers backend development, system architecture, legacy modernization and cross-jurisdiction integration.

More recently I have been integrating LLMs into production systems, with human approval required on every action that writes.

Based in Sarasota, Florida.

## Projects

### rulecheck · [source](https://github.com/gyetisken/rulecheck)

Five US cities regulate short-term rentals, all five require a licence, and all five write it differently. This reads the five ordinances and puts them in one table.

A model reads each one and returns a list of requirements, each carrying the sentence it came from. A second pass maps those onto seventeen shared identifiers, so *operator's license* in Austin and *permit* in New Orleans end up in the same row. Everything after that is ordinary code: the comparison is a loop, and checking a property against a city is a comparison, not an inference.

The part I would defend in a review is what happens when it does not know. A rule it cannot settle is reported as unsettled rather than guessed, and the two reasons for that are kept apart: a question you have not answered, and a rule no program can decide.

Python, Pydantic, FastAPI, the Anthropic API with strict tool use.

### Xvoria · [xvoria.com](https://xvoria.com) · [architecture notes](https://github.com/gyetisken/xvoria)

A 3D countertop designer and quoting tool for stone fabricators. The customer draws a counter in the browser, places sink and cooktop cutouts, selects a slab, and receives a price as the design changes.

I built the designer and the domain engine behind it: edge profiles, seam placement, slab layout, the conversion from a drawing into fabrication pieces, and the pricing rules that turn those pieces into quote lines. DXF import and export keeps the tool compatible with the CAD files a shop already runs on.

Three.js, TypeScript, Next.js.

### LeedIQ · [leediq.com](https://leediq.com) · [architecture notes](https://github.com/gyetisken/leediq)

A lead generation and direct mail platform for pool builders. Property records are ingested daily from five Florida county sources, deduplicated by parcel ID, and filtered against county characteristics, permit history and Claude vision on satellite imagery to identify homes without a pool. Qualifying records become targeted postcard campaigns.

Next.js, TypeScript, PostgreSQL, Drizzle, Stripe, Lob, Anthropic API.

## Selected work

**Cross-platform integration.** I own the integration between our bar admissions platform and our investigations platform. Two problems at once: every jurisdiction writes its own character-and-fitness form, so the same question lives in a different field with different wording, and the investigations side had no data model of its own. I was not mapping one model onto another, I had to design the target first.

What set the bar was what happens downstream: the investigations platform generates letters and emails to the applicant from this data, so a field in the wrong place means a real person receives a wrong letter inside a legal process. I wrote a canonical JSON schema of just over 5,000 lines, then put the mapping in tags on the form definitions rather than in per-jurisdiction code, so onboarding a jurisdiction means tagging a form rather than writing an integration. Nothing is sent until it validates against the schema. Three jurisdictions are live, forms for six more are mapped.

**Event-driven migration.** I led the move from a five-minute sequential sync to per-flow Cloud Tasks. The old pipeline processed steps in order, so a single stuck step held up everything behind it, and under load it ran several instances whose in-memory context diverged and repeated each other's work. The worst case was a file that downloaded successfully and was never recorded as downloaded, so the next run fetched it again. I isolated each flow into its own task with its own retry and moved run state out of memory and into the database. The final load test delivered 100 of 100 messages in 44 seconds with no errors, behind per-flow database toggles that allow rollback without a redeploy.

**Platform modernization.** I migrated a production exam platform from Java 8, Struts 2.5 and Spring 5 to Java 17, Struts 7, Spring 6 and Jakarta EE across 124 files. Four upgrades at once, and two of them were not mechanical: the javax to jakarta namespace move, and tearing out Apache Tiles, which the new Struts release no longer supports, which meant rebuilding the page layer rather than renaming imports. I verified the application end to end myself before handing it to QA.

**Financial systems.** I rebuilt a monthly general ledger export as a configuration-driven rules engine. The export is double-entry: money arriving in the bank is a positive line and the revenue it corresponds to is a negative one, so a healthy fee contributes both and nets out. The batch summing to zero is the proof that nothing was recorded on only one side, which is what accounting checks before they accept it. The rules producing all of that lived inside a 591-line Java file as a single hard-coded query: 33 blocks joined by UNION, feeding 26 ledger accounts. Mapping a new application type to an account meant editing a string and shipping a release, so accounting waited on engineering for what was really a bookkeeping decision.

The rule set now lives in two configuration tables and the query is assembled at run time, which turns a code change into an INSERT from an admin screen that validates the balance before anything is exported. The part I would do the same way again is the migration: I seeded the new configuration to reproduce the old query bug for bug, then ran both side by side for months. Keeping the refactor separate from the fixes is what made it possible to tell which change caused a difference. I also wrote an imbalance explainer that groups the output by fee rather than by account, so when a month does not balance it points at the records responsible instead of leaving someone to read SQL. Authorize.Net payments, refunds and reconciliation across multiple ledger accounts sit underneath all of it.

**AI-assisted delivery.** I built a delivery pipeline on Claude Code, MCP and a written set of agent skills. It reads the ticket, proposes an implementation plan, and waits. Once I approve, it drafts the fix, shows me the diff, asks before opening the pull request, shows me the review comment it intends to post, then writes the QA note on the ticket and moves it along through the ticketing system's own MCP.

The part I did not plan for is what happened next. Implementation got faster, so the work simply pooled in QA instead. The constraint had moved rather than disappeared, so I extended the pipeline into QA: it deploys the branch to a development server, waits for the build, writes test cases and runs them under Playwright, and queries a development database when a check needs real data. Every write, every deploy and every query is proposed before it runs, and there is no path to production at all.

It also keeps memory files about each codebase and updates them as it learns, so tickets of a familiar shape now go through cleanly on the first attempt. Closed tickets roughly doubled across eight repositories, which is a count rather than a controlled measurement, but the direction is not subtle.

## Technical skills

Java 8–21 · Spring 6 · Jakarta EE · Python · TypeScript · SQL · PostgreSQL · Google Cloud (Cloud Run, Cloud Tasks, Cloud Scheduler, Secret Manager) · Docker · REST and SOAP · mTLS · Anthropic API · Model Context Protocol · Playwright

## Contact

gyetisken@gmail.com · [LinkedIn](https://linkedin.com/in/gokhanyetisken)
