# Gökhan Yetişken

Senior software engineer with 11 years building and modernizing enterprise systems, primarily for U.S. bar admissions and professional licensing organizations. My work covers backend development, system architecture, legacy modernization and cross-jurisdiction integration.

More recently I have been integrating LLMs into production systems, with human approval required on every action that writes.

Based in Sarasota, Florida.

## Projects

### Xvoria · [xvoria.com](https://xvoria.com) · [architecture notes](https://github.com/gyetisken/xvoria)

A 3D countertop designer and quoting tool for stone fabricators. The customer draws a counter in the browser, places sink and cooktop cutouts, selects a slab, and receives a price as the design changes.

I built the designer and the domain engine behind it: edge profiles, seam placement, slab layout, the conversion from a drawing into fabrication pieces, and the pricing rules that turn those pieces into quote lines. DXF import and export keeps the tool compatible with the CAD files a shop already runs on.

Three.js, TypeScript, Next.js.

### LeedIQ · [leediq.com](https://leediq.com) · [architecture notes](https://github.com/gyetisken/leediq)

A lead generation and direct mail platform for pool builders. Property records are ingested daily from five Florida county sources, deduplicated by parcel ID, and filtered against county characteristics, permit history and Claude vision on satellite imagery to identify homes without a pool. Qualifying records become targeted postcard campaigns.

Next.js, TypeScript, PostgreSQL, Drizzle, Stripe, Lob, Anthropic API.

## Selected work

**Cross-platform integration.** I own the integration between our bar admissions platform and our investigations platform. The two systems were developed separately, with different data models and no shared vocabulary. I authored a canonical JSON schema of just over 5,000 lines and a tag-driven mapping layer that converts each jurisdiction's character-and-fitness forms, both individual and entity, into a single investigation model. It is in production for three jurisdictions, with forms mapped for six more.

**Event-driven migration.** I led the move from a five-minute polling sync to per-flow Cloud Tasks. Removing the delay surfaced a race condition it had been masking; I identified it during load testing and redesigned the attachment flow to retry safely. The final load test delivered 100 of 100 messages in 44 seconds with no errors, and per-flow database toggles allow rollback without a redeploy.

**Platform modernization.** I migrated a production exam platform from Java 8, Struts 2.5 and Spring 5 to Java 17, Struts 7, Spring 6 and Jakarta EE across 124 files, then diagnosed a post-migration framework security restriction that had silently disabled a core search feature.

**Financial systems.** I replaced a 1,000-line hard-coded general ledger export with a configuration-driven rules engine and an administrative interface with zero-balance validation, allowing accounting to manage mappings without a release. I also own Authorize.Net payments, refunds and reconciliation across multiple GL accounts, and a TransUnion credit report integration over mTLS with idempotent scheduled processing.

**AI-assisted delivery.** I built an internal development pipeline on Claude Code and the Model Context Protocol covering ticket triage, fix drafting, pull request creation, code review and Playwright end-to-end runs, with human approval required at every write and deploy. It approximately doubled monthly delivery across eight repositories.

## Technical skills

Java 8–21 · Spring 6 · Jakarta EE · Python · TypeScript · SQL · PostgreSQL · Google Cloud (Cloud Run, Cloud Tasks, Cloud Scheduler, Secret Manager) · Docker · REST and SOAP · mTLS · Anthropic API · Model Context Protocol · Playwright

## Contact

gyetisken@gmail.com · [LinkedIn](https://linkedin.com/in/gokhanyetisken)
