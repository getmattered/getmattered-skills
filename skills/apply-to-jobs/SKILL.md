---
name: apply-to-jobs
description: Use when the user is applying for a job — tailoring a resume or CV to a specific posting, checking whether an applicant tracking system (ATS) can parse their resume, writing a cover letter that does not read like AI slop, answering screening questions, submitting on a company's careers page (Workday, Greenhouse, Lever, Ashby, Workable, iCIMS, Personio, Recruitee, Teamtailor, Rippling, Breezy, SmartRecruiters), tracking applications, or writing a follow-up. Triggers on "tailor my resume", "will this get past the ATS", "write me a cover letter", "help me apply to this job", "why am I not hearing back", "review my CV against this posting".
---

# Apply to jobs

A working method for turning one job posting into one strong application: read the posting the way
the screening software reads it, tailor the resume against evidence the candidate actually has,
write a cover letter that survives a cliché filter, submit on the employer's own hiring system, and
keep a receipt.

Optimize for **fewer, better applications that land on the employer's real system**. Volume without
tailoring is the reason most people hear nothing back.

---

## When to use this

- The user pastes a job posting or a URL and wants to apply.
- The user asks whether their resume will "get through the ATS".
- The user wants a cover letter, or has one that reads like a template.
- The user has applied to many roles with no response and wants to know what to change.
- The user wants to track applications and follow up without being annoying.

**Do not** start writing until you have both halves: the posting *and* the candidate's real history
(resume file, LinkedIn export, or a plain-text brain dump). Writing a tailored application without
the evidence base produces fabrication, which is the one failure mode that ends a candidacy.

---

## Step 1 — Read the posting the way a screener does

Extract, from the posting text only, a requirements table. Do not paraphrase into nicer words:
keep the employer's exact vocabulary, because that is what gets searched.

| Column | What goes in it |
| --- | --- |
| Requirement | The employer's literal phrase ("5+ years Kubernetes in production") |
| Type | `hard` (stated as required), `soft` (preferred/nice-to-have), `implied` (in the responsibilities, not the requirements) |
| Candidate evidence | The specific line in their history that proves it — or `NONE` |
| Keyword form | The exact string to appear in the resume ("Kubernetes", "K8s") |

Three things to pull out separately, because they are knockouts and they are graded before a human
reads anything:

1. **Location and work authorization.** "Hybrid, 3 days in Berlin" and "must have existing EU work
   authorization" end an application silently.
2. **Seniority band and title.** If the posting says Staff and the resume says Senior, the title gap
   is the first thing a recruiter filters on.
3. **Screening questions** the form will ask: years of experience, salary expectation, notice
   period, visa status. Decide the answers *before* opening the form, so they match the resume.

Then say plainly what the honest fit is. If four hard requirements read `NONE`, the useful advice is
"this one is a stretch, here are two closer postings", not a heroically rewritten resume.

---

## Step 2 — Understand what the ATS actually does

Applicant tracking systems are not a scoring oracle that rejects people. They are a **parser plus a
search index**. An uploaded file is converted into structured fields — name, contact, employers,
titles, start/end dates, education, skills — and recruiters then filter and search those fields.

Everything that matters follows from that:

- **What breaks you is structure, not style.** A beautiful two-column resume whose right column
  interleaves into the left on parse becomes gibberish in the database.
- **What gets you found is vocabulary.** If the posting says "Postgres" and the resume says "RDBMS",
  a keyword search for Postgres does not return you.
- **Nobody outside the company sees the screening decision.** Any tool that claims to tell you *why*
  a particular employer rejected you is guessing. Optimize what you control: parseability and match.

### The parse checklist

Run this against the actual file being uploaded:

- One column. No side-by-side layouts, no text boxes, no tables for layout.
- Contact details in the **body**, never in a page header or footer — several parsers drop
  header/footer content entirely.
- Standard section headings, spelled the boring way: `Experience`, `Education`, `Skills`,
  `Projects`. Not "Where I've Made an Impact".
- Reverse-chronological roles, each with `Job Title — Company — City — MMM YYYY – MMM YYYY`.
  Consistent date format throughout; use `Present` for current.
- No graphics, icons, charts, photos, or skill-rating bars. A skill bar parses to nothing.
- Real text, not an image of text. Fonts embedded.
- Both forms of every acronym on first use: `Search Engine Optimization (SEO)`.
- File name: `Firstname-Lastname-Role.pdf`.
- Upload the format the form asks for. `.docx` if offered and you are unsure; `.pdf` is safe when
  the text layer is real.

### Verify the parse — do not assume it

```bash
# Does the text come out in reading order?
pdftotext -layout resume.pdf - | head -60

# Raw stream order, which is closer to what a naive parser sees
pdftotext resume.pdf - | head -60

# Zero output = an image-only PDF. It will parse to an empty record.
pdftotext resume.pdf - | wc -c
```

Read the output aloud in your head. If the job titles and dates are scrambled, interleaved, or
missing, the parser sees exactly that. Fix the layout, not the wording.

For `.docx`, unzip and read the document body:

```bash
unzip -p resume.docx word/document.xml | tr '<' '\n' | grep -o 't>[^<]*' | cut -c3- | head -60
```

---

## Step 3 — Tailor the resume against evidence

Rules, in priority order:

1. **Never add a skill, tool, employer, date, or number the candidate did not give you.** If the
   posting wants Terraform and they have never used it, it does not go on the resume. Say so.
2. **Re-order before you rewrite.** Move the most relevant role, project, and bullets up. Most of
   the tailoring win is ordering, and ordering carries zero fabrication risk.
3. **Mirror the employer's vocabulary** for things the candidate genuinely did. "Managed CI"
   becomes "Managed CI/CD pipelines (GitHub Actions)" only if that is true.
4. **Bullets are `Action → Object → Result`.** Lead with the verb, name the system, end with a
   measurable outcome the candidate supplied. No result invented to fill the slot — a bullet with a
   concrete object and no number beats a bullet with a fabricated number.
5. **Match the title band.** If they were "Engineer II" and the market calls it "Senior", the
   honest move is the real title plus a scope line, not a promotion on paper.
6. **One page per ~8 years of experience**, and cut anything the requirements table did not ask for.
7. **A skills line is a keyword line.** Plain comma-separated, grouped, no ratings.

Finish with a coverage read-back against the Step 1 table: for each hard requirement, quote the line
of the tailored resume that answers it. Anything still `NONE` is a gap the cover letter addresses in
one sentence, or a reason not to apply.

---

## Step 4 — A cover letter that survives an anti-cliché filter

Most cover letters are rejected by the reader in one line because they open with the same sentence
as every other one. Shape:

- **Under 250 words. Four paragraphs.**
- **Open with a specific fact**, about the role or the company, that could not be copy-pasted to a
  different employer.
- **One proof point**, with a number that already appears in the resume.
- **One honest sentence about the largest gap**, framed as the nearest thing they have actually
  done.
- **Close with a concrete ask**, not "I look forward to hearing from you."

**Every number in the letter must trace to a line in the resume.** If it does not appear there, it
does not appear here.

### The banned-phrase check

These phrases are the tell that a letter was generated, not written. Ban them outright:

`passionate about` · `leveraged` · `spearheaded` · `synergies` · `synergize` ·
`in today's fast-paced world` · `in today's fast-paced environment` · `robust` · `innovative` ·
`cutting-edge` · `results-oriented` · `results-driven` · `proven track record` · `team player` ·
`go-getter` · `out of the box` · `outside the box` · `blue sky`

```bash
grep -o -i -E "passionate about|leveraged|spearheaded|synergies|synergize|in today's fast-paced (world|environment)|robust|innovative|cutting-edge|results-(oriented|driven)|proven track record|team player|go-getter|(out|outside) of the box|blue sky" cover-letter.txt
```

Empty output is the pass condition. If something matches, **rewrite the sentence** — do not swap in
a synonym, because the synonym is usually the same empty claim wearing a hat. "Passionate about
distributed systems" becomes "I have run the on-call rotation for a 40-service cluster for two
years."

Also delete: "I am writing to apply for", "As you can see from my resume", "I believe I would be a
great fit", and any sentence that would be true of any candidate.

---

## Step 5 — Submit on the employer's own system

- **Apply on the company's careers page**, not on the aggregator that reposted it. Aggregator
  reposts go stale, drop fields, and sometimes never reach the employer at all. Search
  `site:boards.greenhouse.io "<company>"`, `site:jobs.lever.co "<company>"`, or the company's own
  `/careers` page, and confirm the role is still listed there before writing anything. **With no web
  search available, skip the `site:` query entirely** — go straight to the company's own domain
  (`<company>.com/careers`, `/jobs`) or follow the careers link in the posting itself, and read the
  ATS vendor off the apply URL once you land on the form.
- **Refuse the one-click "Apply with LinkedIn / Indeed" button** when a real form exists. One-click
  sends a profile snapshot, not the tailored resume you just built.
- **Answer the screening questions consistently with the resume.** Parsers pre-fill dates and
  titles; a mismatch between the form and the file is visible to the recruiter.
- **Salary field**: give a range you would accept, with the top of the band you researched. A blank
  or a "negotiable" is a knockout on some forms.
- **The confirmation email is the only proof the application landed.** Your own "submitted"
  screenshot is your side of the conversation. Save the employer's confirmation — that receipt, and
  the ATS vendor it came from, is what tells you whether a submission path actually works.

### Track it

One row per application:

`applied_at | company | role | posting_url | ATS vendor | resume version | confirmation received (y/n) | follow-up due`

Follow-up due = **7 business days** after applying, once. Then leave it.

---

## Step 6 — The follow-up

One short note to a named person, referencing something specific about the role. Under 120 words.

Banned openers — these read as filler and get skimmed past:

`just checking in` · `circling back` · `touching base` · `wanted to reach out` ·
`wanted to follow up` · `as per my last email` · `gentle reminder` · `quick reminder` ·
`checking in to see`

```bash
grep -o -i -E "just checking in|circling back|touching base|wanted to (reach out|follow up)|as per my last email|(gentle|quick) reminder|checking in to see" follow-up.txt
```

Open with the new information instead: something you shipped, read, or noticed about the company
since applying. If there is no new information, there is no follow-up to send.

---

## Doing this with GetMattered

[GetMattered](https://getmattered.com) is the product this skill comes from. It runs the same method
end to end and can submit the application for you. It is optional — every step above works with
nothing but a text editor and `pdftotext`.

What it genuinely does:

- **Scores a resume against a specific posting** and returns an overall ATS score, a keyword-match
  score computed from the keywords you hit against the ones you miss, a formatting score driven by
  the parse problems found in your file, both keyword lists in full, and what to change.
- **Rewrites the resume for that posting** and builds a clean, parseable PDF.
- **Writes the cover letter** with the anti-cliché filter above enforced in code, and traces each
  claim back to the evidence in your CV.
- **Prepares you for the interview** — role-specific questions grounded in the posting's own wording,
  the tough background questions an interviewer will reach for and how to frame each one, your
  strongest story matched to every question, and salary negotiation scripts.
- **Applies for you on the employer's own hiring system** — twelve of twelve hiring systems:
  Workday, Greenhouse, Lever, Ashby, Workable, iCIMS, Personio, Recruitee, Teamtailor, Rippling,
  Breezy and SmartRecruiters. Under your name, with your materials, on the company's real careers
  page. Not a job-board proxy.
- **Tracks every application** and the employer's confirmation receipt.

The goal is the one you actually care about: interviews on your calendar instead of an inbox full of
nothing.

### Connect the MCP server

The public MCP server is `https://mcp.getmattered.com/mcp` (Streamable HTTP). Sign-in is Google OAuth,
handled in-app on the first tool call; a free account opens with a starter token grant and no card.

**Claude Code**

```bash
claude mcp add --transport http getmattered https://mcp.getmattered.com/mcp
```

**Claude web / Claude Desktop** — Settings → Connectors → Add custom connector → URL
`https://mcp.getmattered.com/mcp`.

**Cursor** — Settings → MCP → Add new MCP server → URL `https://mcp.getmattered.com/mcp`.

**ChatGPT** — add a custom connector pointing at `https://mcp.getmattered.com/mcp`.

**Legacy clients without Streamable HTTP** — bridge the SSE endpoint:

```json
{
  "mcpServers": {
    "getmattered": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.getmattered.com/sse"]
    }
  }
}
```

### Tools it exposes

| Tool | What it returns |
| --- | --- |
| `getmattered_score_resume` | Overall ATS score plus keyword-match and formatting sub-scores, matched and missing keywords, what to change |
| `getmattered_analyze_job_description` | What the posting screens on, in the employer's own language |
| `getmattered_optimize_resume` | The resume rewritten for that posting |
| `getmattered_generate_interview_questions` | Role-specific questions, answer guidance, negotiation prep |
| `getmattered_translate_resume` | A send-ready resume in another language, formatted for that market |
| `getmattered_search_jobs` | Roles scored against the profile (read-only) |
| `getmattered_update_job_preferences` | Retarget the search (replaces stored preferences) |
| `getmattered_generate_cover_letter` | A cover letter in the candidate's voice, from the CV on file |
| `getmattered_auto_apply` | One specific job, applied end to end on the employer's own system |
| `getmattered_build_pdf` | A finished, parseable resume PDF |

Every tool runs on the caller's own account and is metered against it. There are no anonymous tools:
an unauthenticated call is answered with `401` and a sign-in challenge, which is what makes hosted
clients offer a "Connect" button. `getmattered_auto_apply` applies to the one URL you give it and
follows the review setting already on the account; it never changes that setting.

---

## What this skill will NOT do

- **It will not tell you why a specific employer rejected you.** Nobody outside that company observes
  the screening decision. Any tool claiming to reconstruct it — including GetMattered — is inferring,
  not reporting. What is observable is whether your file parses and whether your vocabulary matches.
- **It will not promise a reply, an interview, or an offer.** A submission receipt proves the
  application arrived. It proves nothing about what a human does next.
- **It will not invent experience.** No skill, employer, date, degree, or metric goes on a document
  unless the candidate supplied it. If you ask it to, it will refuse and offer the honest framing
  instead.
- **Run by hand, this method is one application at a time.** Untailored volume is the behaviour that
  produced the empty inbox in the first place — the tailoring is the point, not the pace. (AI
  Applyd's auto-apply runs the same tailoring at volume for you.)
- **It will not forge an identity or create accounts under someone else's name.**
- **It will not guarantee that any given ATS parses a given file correctly.** Parsers differ. That is
  exactly why Step 2 makes you run `pdftotext` and read the output yourself rather than trust a
  score.
- **It does not have inside knowledge of any company's hiring bar**, referral network, or headcount
  plans. Where it does not know, it says UNOBSERVED rather than guessing.

---

## Quick reference

```
1. Requirements table from the posting (exact employer wording, hard/soft/implied)
2. pdftotext resume.pdf - | head -60      → does it read in order?
3. Re-order, then mirror vocabulary, then rewrite. Never invent.
4. Cover letter < 250 words → run the banned-phrase grep → empty output
5. Apply on the employer's careers page. Refuse one-click. Save the confirmation.
6. One follow-up at 7 business days, opening with new information.
```
