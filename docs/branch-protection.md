# Branch Protection Setup

This guide walks you through protecting `main` and `dev` in the GitHub UI.

## Protect `main`

1. Go to your repo on GitHub.
2. Click **Settings > Branches**.
3. Under **Branch protection rules**, click **Add rule**.
4. Set **Branch name pattern** to `main`.
5. Enable the following settings:

### Required settings

- **Require a pull request before merging**
  - Set **Required approvals** to `1` (or more for larger teams).
- **Require status checks to pass before merging**
  - Check **Require branches to be up to date before merging**.
  - Search for and add the **Lint & Test** status check. This name comes from the CI workflow in [`.github/workflows/ci.yml`](../.github/workflows/ci.yml). The check won't appear in the search until the workflow has run at least once.
- **Require linear history** — keeps the commit graph clean and readable. This blocks merge commits, so leave it off if you promote `dev` to `main` with a merge commit as described in [docs/dev-to-main-flow.md](dev-to-main-flow.md).
- **Require signed commits** — ensures every commit is verified. See [docs/verified-commits.md](verified-commits.md) for setup instructions.
- **Do not allow bypassing the above settings** — applies rules to admins and repo owners too.

6. Click **Create**.

## Protect `dev` (lighter rules)

Protecting `dev` is optional but recommended. Repeat the steps above with these differences:

- **Branch name pattern**: `dev`
- **Require a pull request before merging**: enable, but you can set required approvals to `0` if you're a solo dev.
- **Require status checks to pass**: same as `main` — add the **Lint & Test** check.
- **Require signed commits**: optional on `dev`.
- **Do not allow bypassing**: your call. Some teams allow admin bypass on `dev` for quick iteration.

You can skip **Require linear history** on `dev` if you prefer merge commits for feature branches.

## Rulesets vs. classic branch protection

GitHub now offers **repository rulesets** as a newer alternative to classic branch protection. Rulesets support the same settings described above and add features like organization-level rules and tag protection. Either approach works for this workflow. The steps above use classic branch protection because it's simpler and available on all plan tiers.

## Import the rulesets instead

If your repository can use rulesets, you can skip the manual steps and import the two examples in [`examples/`](../examples/):

| File | Applies to | What it enforces |
|---|---|---|
| [`ruleset-main.json`](../examples/ruleset-main.json) | The default branch | No deletion or force push, signed commits, PR with 1 approval, resolved conversations, merge or squash only, **Lint & Test** passing on an up-to-date branch |
| [`ruleset-dev.json`](../examples/ruleset-dev.json) | `dev` | No deletion or force push, PR with 0 approvals, **Lint & Test** passing on an up-to-date branch |

Neither ruleset has bypass actors, so the rules apply to admins too.

### From the GitHub UI

1. Download the JSON file you want.
2. Go to **Settings > Rules > Rulesets**.
3. Open the **New ruleset** dropdown and click **Import a ruleset**.
4. Select the JSON file, review the rules, and click **Create**.

Repeat for the second file.

### From the command line

With the [GitHub CLI](https://cli.github.com/) signed in as a repository admin:

```bash
gh api --method POST repos/OWNER/REPO/rulesets --input examples/ruleset-main.json
gh api --method POST repos/OWNER/REPO/rulesets --input examples/ruleset-dev.json
```

Replace `OWNER/REPO` with your repository. Check the result:

```bash
gh api repos/OWNER/REPO/rulesets
```

### Adjust before importing

- **Approvals**: change `required_approving_review_count` in `ruleset-main.json` if your team needs more than one reviewer. Solo developers can't approve their own PRs, so set it to `0`.
- **Signed commits**: remove the `required_signatures` rule if you don't sign commits.
- **Linear history**: add `{ "type": "required_linear_history" }` to `rules` and drop `"merge"` from `allowed_merge_methods` if you squash `dev` into `main` instead of using a merge commit.
- **Status check name**: the `context` must match the job `name` in your CI workflow. It's `Lint & Test` in [`ci.yml`](../.github/workflows/ci.yml).

## Verify it works

After setting up protection:

1. Try pushing directly to `main`:

   ```bash
   git checkout main
   git commit --allow-empty -m "test direct push"
   git push
   ```

   This should be rejected.

2. Open a PR to `main` without CI passing. The merge button should be disabled until the **Lint & Test** check goes green.

3. Check that the PR requires the correct number of approvals before merging.

If all three are blocked as expected, your protection is working.
