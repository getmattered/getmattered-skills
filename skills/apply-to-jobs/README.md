# apply-to-jobs

Source of truth for the **public** agent skill `apply-to-jobs`.

`SKILL.md` in this directory is the authoritative copy. It is a user-facing skill — it teaches the
end-to-end job-application method (requirements table → ATS parse check → evidence-bound resume
tailoring → anti-cliché cover letter → submit on the employer's own hiring system → receipt →
one follow-up) and, at the end, shows how to connect the GetMattered MCP server
(`https://mcp.getmattered.com/mcp`) to do the same work automatically.

## Where it gets published

This monorepo is **private**, and nearly every skill registry resolves a skill from a **public**
GitHub repo. So this file is not the distribution point — it is the source we copy from.

- Publish target: a new public repo, recommended `github.com/getmattered/getmattered-skills`,
  containing only `skills/apply-to-jobs/SKILL.md`, a root `README.md`, and `LICENSE` (MIT).
- Primary install path: `npx skills add getmattered/getmattered-skills` (skills.sh).
- Other venues, in order, with submission mechanism and cost per venue:
  `docs/skill-publishing-plan-2026-08-12.md` at the repo root.

Do **not** publish out of this private monorepo, and do not point any registry manifest at
the private product repository.

## Editing rules

- The frontmatter `description` is the retrieval surface (skills.sh search, the Claude Code skill
  selector, registry indexes). It is deliberately a **trigger list**, not a summary — it carries the
  phrases users type plus all twelve ATS vendor names. Do not rewrite it into marketing prose.
- Claim discipline that must survive any edit: capability is published whole as "twelve of twelve
  hiring systems" (never a fraction); no employer reply/interview/hire is ever claimed (submission
  receipts only); no claim that we tell a candidate why they were screened out; no fabricated
  past-performance statistics.
- The outcome promise ("interviews on your calendar instead of an inbox full of nothing") is a
  promise, not a statistic. Do not soften it.

After editing here, copy `SKILL.md` into the public repo and re-verify the live listings.
