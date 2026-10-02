# Working on the Trust Drive landing page

The person asking for changes is usually **PJ**, Steve's business partner. PJ is not a coder. Talk to him in plain English: say what changed on the website, not what changed in the code. Skip jargon, or explain it in a few words when you can't avoid it ("a branch is a separate draft copy of the site").

## The one rule: never change `main` directly

`main` is the live site. Every merge or push to `main` can go live on the real Trust Drive website, so all work goes through a branch and a pull request, and **PJ decides when it goes live**.

For every new piece of work:

1. **Start fresh from `main`:** `git checkout main && git pull`, then create a new branch with a short descriptive name, like `update-pricing-copy` or `fix-get-started-cta`. Don't reuse an old branch for unrelated work.
2. **Make the changes and commit** on that branch, with a clear commit message.
3. **Push the branch and open a pull request** into `main`. Write the PR description in plain English, as a short list of what will change on the site.
4. **Tell PJ it's ready and ask him to merge.** Include:
   - a plain-English summary of what will change on the website
   - the pull request link
   - how to put it live: open the link, click the green **Merge pull request** button, then **Confirm merge**
5. **Don't merge it yourself** unless PJ clearly says so in this conversation (for example, "go ahead and merge it"). Asking you to make a change is not permission to merge it.
6. **After a merge,** confirm the deploy actually went out and load the live site to check the change is really there before telling PJ it's done. "Deployment finished" alone doesn't prove the live page changed.

If PJ asks for more changes before merging, add them to the same branch and PR. Once a PR is merged, the next request starts a new branch.

## Things that need Steve, not PJ

Stop and suggest PJ check with Steve before:

- changing how this site deploys — there's no deploy workflow file in this repo, so confirm with Steve how a push to `main` actually reaches the live site before assuming
- changing anything in Cloudways, GitHub secrets, or repo settings
- deleting pages or renaming page files (that breaks links people and Google already have)

Never put passwords, API keys, or tokens in any file. Everything in this repo may end up published to the website, including this file.

## Site basics

Plain HTML, no build step. Two pages:

- `index.html` — the main landing page
- `get-started.html` — the get-started page

Keep any business name, address, and phone number on these pages character-for-character identical to the real Trust Drive details — mismatches hurt local ranking.
