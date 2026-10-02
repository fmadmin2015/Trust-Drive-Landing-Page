# Working on Michianalocal

The person asking for changes is usually **PJ**, Steve's business partner. PJ is not a coder. Talk to him in plain English: say what changed on the website, not what changed in the code. Skip jargon, or explain it in a few words when you can't avoid it ("a branch is a separate draft copy of the site").

## The one rule: never change `main` directly

`main` is the live website. Every merge or push to `main` deploys to michianalocal.com within about a minute (`.github/workflows/deploy.yml`). So all work goes through a branch and a pull request, and **PJ decides when it goes live**.

For every new piece of work:

1. **Start fresh from `main`:** `git checkout main && git pull`, then create a new branch with a short descriptive name, like `add-smith-plumbing` or `update-theta-hours`. Don't reuse an old branch for unrelated work.
2. **Make the changes and commit** on that branch, with a clear commit message.
3. **Push the branch and open a pull request** into `main` with `gh pr create`. Write the PR description in plain English, as a short list of what will change on the site.
4. **Tell PJ it's ready and ask him to merge.** Include:
   - a plain-English summary of what will change on the website
   - the pull request link
   - how to put it live: open the link, click the green **Merge pull request** button, then **Confirm merge**
   - that the site updates about a minute after he merges
5. **Don't merge it yourself** unless PJ clearly says so in this conversation (for example, "go ahead and merge it"). Asking you to make a change is not permission to merge it.
6. **After a merge,** check that the deploy finished (`gh run list --workflow deploy.yml --limit 1`, then `gh run watch <id>`). Then load the changed page at `https://michianalocal.com/...` and confirm the change is really there. "Deployment finished" alone doesn't prove the live page changed. Tell PJ the result.

If PJ asks for more changes before merging, add them to the same branch and PR. Once a PR is merged, the next request starts a new branch.

## Things that need Steve, not PJ

Stop and suggest PJ check with Steve before:

- changing anything in `.github/workflows/` (the deploy setup)
- changing anything in Cloudways, GitHub secrets, or repo settings
- deleting pages or renaming page files (that breaks links people and Google already have)

Never put passwords, API keys, or tokens in any file. Everything in this repo is published to the website, including this file.

## How deploys work

- Pushing or merging to `main` makes GitHub Actions ask Cloudways to `git pull` `main` into the site's `public_html/` folder.
- To redeploy without changing anything: `gh workflow run deploy.yml`.
- Don't tell PJ to use the **Pull** button in Cloudways' "Deployment via Git" screen. Its path field can put the site into the wrong folder (`public_html/public_html`).

## Site basics

Plain HTML and CSS, with no build step. See `README.md` for how to add a business or a category. Key points:

- New business pages: copy `business-template.html` to `categories/<category>/<business>.html` and replace every `[BRACKETED]` value, including the canonical link and the two JSON-LD blocks at the top.
- Name, address and phone must match the business's Google Business Profile exactly.
- Reviews box: paste the business's Review-Engine snippet from the Review-Engine sheet. It's a `<div data-review-engine=...>` **plus** a `<script src=".../exec?a=embedjs" async>` line, and both are needed.
- Every page has a `<link rel="canonical">` pointing to its `https://michianalocal.com/...` address, without `www.`.
