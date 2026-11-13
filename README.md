# GetMattered skills

The workflow skills of the [GetMattered MCP server](https://github.com/getmattered/getmattered-mcp), version 1.19.1. Each folder holds one `SKILL.md`: the steps an assistant follows with the GetMattered tools for one part of a job search.

This repository is rewritten by every release of getmattered-mcp, so it always matches the live server. Please open issues and pull requests on [getmattered/getmattered-mcp](https://github.com/getmattered/getmattered-mcp) instead.

## Skills

| skill | what it does |
|---|---|
| [`apply-to-a-job`](skills/apply-to-a-job/SKILL.md) | Send a real job application with GetMattered. |
| [`build-resume-document`](skills/build-resume-document/SKILL.md) | Get the PDF of the user's resume on file, share it when asked, or create a private editable draft in the GetMattered resume builder. |
| [`find-matching-jobs`](skills/find-matching-jobs/SKILL.md) | Find jobs that fit the user with GetMattered, save or skip them, and change what it looks for. |
| [`follow-up-on-applications`](skills/follow-up-on-applications/SKILL.md) | Follow up with employers on applications that have gone quiet, using GetMattered. |
| [`handle-recruiter-replies`](skills/handle-recruiter-replies/SKILL.md) | Read the emails employers sent about the user's applications, explain what each employer wants, and send the user's reply with GetMattered once they approve the exact text. |
| [`manage-saved-searches`](skills/manage-saved-searches/SKILL.md) | Save the user's current GetMattered job preferences as a named search and turn email alerts for its new matches on or off. |
| [`prepare-for-interview`](skills/prepare-for-interview/SKILL.md) | Prepare for a specific job interview with GetMattered and practice answers grounded in the user's experience. |
| [`review-and-send`](skills/review-and-send/SKILL.md) | Review the applications GetMattered prepared, change them, and send the ones the user approves. |
| [`setup-job-search`](skills/setup-job-search/SKILL.md) | Set up a GetMattered account for job matching with the user's resume and job preferences. |
| [`tailor-for-a-job`](skills/tailor-for-a-job/SKILL.md) | Score and tailor the user's resume to one job posting with GetMattered. |
| [`track-applications`](skills/track-applications/SKILL.md) | Check where the user's job applications stand with GetMattered, which employers confirmed them, and how many applications and credits the user has left. |
| [`translate-resume`](skills/translate-resume/SKILL.md) | Translate a saved GetMattered resume-builder document into another language. |
| [`using-getmattered`](skills/using-getmattered/SKILL.md) | Map of the GetMattered tools. |
| [`write-cover-letter`](skills/write-cover-letter/SKILL.md) | Write or revise a cover letter for one job with GetMattered. |

## Using them

The skills call the GetMattered tools, so connect the server first: see [getmattered-mcp](https://github.com/getmattered/getmattered-mcp#readme). Its plugin already carries these skills. To add only the skills to an assistant that reads `SKILL.md` folders:

```bash
npx skills add getmattered/getmattered-skills
```

## Licence

MIT, see [LICENSE](LICENSE).
