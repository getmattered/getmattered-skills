# AI Applyd Skills

Open skills for AI agents, published by [AI Applyd](https://aiapplyd.com).

A skill is a folder with a `SKILL.md` — a set of instructions an agent loads when a task matches its
description. These are written to be useful on their own, in any agent that reads the format. No
account, no key, nothing to install.

## Skills

| skill | use it when |
|---|---|
| [`apply-to-jobs`](skills/apply-to-jobs) | Tailoring a resume to a posting, checking whether an ATS can parse it, writing a cover letter that doesn't read like AI slop, answering screening questions, submitting on a company's own careers page, and following up. |

## Using a skill

**Fastest — any agent** (Claude Code, Codex, Cursor, Copilot, Zed, Amp and more):

```bash
npx skills add whateverneveranywhere/aiapplyd-skills
```

**Claude Code** — or clone into your skills directory:

```bash
git clone https://github.com/whateverneveranywhere/aiapplyd-skills.git
cp -r aiapplyd-skills/skills/apply-to-jobs ~/.claude/skills/
```

**Anything else** — `SKILL.md` is plain Markdown with YAML frontmatter. Paste it into your system
prompt, or point your agent's loader at the folder.

## What these are, and are not

They encode a **method**, not a product. `apply-to-jobs` will make an application meaningfully
stronger whether or not you ever use AI Applyd — that is the point of publishing it.

Where a claim would need evidence we cannot show you, the skill says so plainly rather than asserting
it. If you find a line that overstates something, open an issue; we would rather fix it than defend
it.

## Contributing

Issues and PRs welcome. For a new skill, keep the same shape: one folder, one `SKILL.md` with `name`
and `description` frontmatter, and a description written so an agent can tell from it alone whether
the skill applies.

## Licence

MIT — see [LICENSE](LICENSE). Use them, fork them, ship them in your own tools.
