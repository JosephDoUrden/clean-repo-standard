# clean-repo-standard

**A GitHub repo template for shipping to production safely.**

> Move fast — but don't break prod.

## What this is

A ready-to-use repository template with branch protection rules, a CI workflow, a PR template, and documentation. It gives small teams a production-safe workflow in under 30 minutes — no paid tools, no complex setup.

## Who this is for

- Solo developers who want guardrails without overhead
- Small teams (2-10 people) setting up a new repo
- Anyone tired of pushing directly to `main` and hoping for the best

## What's included

| File | Purpose |
|------|---------|
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | PR template with summary, risk level, testing, and rollback sections |
| [`.github/workflows/ci.yml`](.github/workflows/ci.yml) | Minimal CI workflow that runs on PRs to `dev` and `main` |
| [`.github/workflows/stale.yml`](.github/workflows/stale.yml) | Marks issues and PRs stale after 60 days without activity and closes them 14 days later |
| [`.github/dependabot.yml`](.github/dependabot.yml) | Weekly Dependabot updates for the pinned GitHub Actions |
| [`.github/CODEOWNERS`](.github/CODEOWNERS) | Requests review from the owner on every PR. Replace `@JosephDoUrden` with your own user or team |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) | Bug report and feature request templates |
| [`docs/branch-protection.md`](docs/branch-protection.md) | Step-by-step guide to protecting `main` and `dev` in GitHub |
| [`docs/verified-commits.md`](docs/verified-commits.md) | How to set up SSH or GPG commit signing |
| [`docs/dev-to-main-flow.md`](docs/dev-to-main-flow.md) | The branching workflow, merge strategies, and hotfix process |
| [`examples/ruleset-main.json`](examples/ruleset-main.json) | Ruleset for `main`, ready to import |
| [`examples/ruleset-dev.json`](examples/ruleset-dev.json) | Ruleset for `dev`, ready to import |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | How to open issues and pull requests, plus the docs writing style |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Contributor Covenant 2.1 |
| [`SECURITY.md`](SECURITY.md) | How to report a vulnerability privately |

## Quick start

1. **Use this template.** Click "Use this template" on GitHub to create your repo.

2. **Set up branch protection.** Import the rulesets (see below) or follow [docs/branch-protection.md](docs/branch-protection.md) to protect `main` and `dev` by hand.

3. **Configure commit signing.** Follow [docs/verified-commits.md](docs/verified-commits.md) to sign your commits with SSH or GPG.

4. **Customize CI.** Open [`.github/workflows/ci.yml`](.github/workflows/ci.yml) and replace the placeholder `echo` commands with your actual lint and test commands.

5. **Start shipping.** Read [docs/dev-to-main-flow.md](docs/dev-to-main-flow.md) for the day-to-day workflow, then open your first PR.

## Import the rulesets

The [`examples/`](examples/) folder holds ruleset exports for `main` and `dev`. Import them in **Settings > Rules > Rulesets > New ruleset > Import a ruleset**, or from the command line:

```bash
gh api --method POST repos/OWNER/REPO/rulesets --input examples/ruleset-main.json
gh api --method POST repos/OWNER/REPO/rulesets --input examples/ruleset-dev.json
```

[docs/branch-protection.md](docs/branch-protection.md#import-the-rulesets-instead) explains what each file enforces and what to change first.

## Philosophy

Safety should be the default, not an afterthought. This template makes "the right way" the easy way: all changes go through a pull request, CI runs automatically, and `main` always reflects what's in production. It's strict enough to prevent mistakes but light enough that it doesn't slow you down.

## FAQ

**Isn't this overkill for a solo developer?**

No. Branch protection isn't about code review — it's about making deploys intentional. A PR gives you a moment to read your own diff, confirm CI passes, and merge deliberately instead of pushing on impulse.

**Can I skip the `dev` branch?**

You can, but it's not recommended. The `dev` branch lets you batch features and test them together before promoting to production. If you skip it, you lose that staging layer. See [docs/dev-to-main-flow.md](docs/dev-to-main-flow.md) for the full rationale.

**What if I don't want signed commits?**

Commit signing is recommended but not required. If you skip it, just don't enable "Require signed commits" in your branch protection rules. Everything else still works.

## Contributing

Contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request, and report security problems through [SECURITY.md](SECURITY.md).

If you use this template, update the contact details in `CODE_OF_CONDUCT.md` and `SECURITY.md` for your own project.

## License

[MIT](LICENSE)
