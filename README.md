# Finlens OSS

This package is the open-source version.
It does not assume Longbridge or any private broker connector is available.
If the user has configured Longbridge, Futu, or IBKR, the workflow can use it.
Otherwise, the analysis falls back to official disclosures, reputable public market-data sources, and web search with explicit freshness labeling.

## Files

* `SKILL.md` = open-source analysis skill
* `AGENTS.md` = repo routing rules
* `references/ownership-positioning.md` = new ownership and positioning module
* `references/report-template.md` = updated report template with ownership section
* `references/fundamental-analysis.md` = updated fundamental workflow with market-structure hook

## Suggested install

Project scope:

```bash
mkdir -p .agents/skills/finlens-oss/references
cp SKILL.md .agents/skills/finlens-oss/SKILL.md
cp AGENTS.md .
cp -R references .agents/skills/finlens-oss/
```

## Notes

* Keep private connectors optional.
* Label all market data freshness clearly.
* Do not make a local CCASS connector a required dependency.
