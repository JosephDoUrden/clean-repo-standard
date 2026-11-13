# Contributing

Thanks for helping. This repo is a template made of docs and GitHub configuration, so most contributions are edits to Markdown, YAML or JSON. There's nothing to build or install.

By taking part you agree to follow the [Code of Conduct](CODE_OF_CONDUCT.md). Security problems go through [SECURITY.md](SECURITY.md), not public issues.

## Issues

Open an issue before starting anything larger than a small fix, so we can agree on the approach first.

- **Bug or mistake**: say which file is wrong, what it says, and what it should say. Link to the GitHub docs page if the mistake is about GitHub behaviour.
- **Idea**: describe the problem it solves for a small team, not just the file you'd add. The template stays small on purpose.

## Pull requests

1. Fork the repo and create a branch from `main`:

   ```bash
   git checkout -b fix/short-description
   ```

   Use `feature/` for new content and `fix/` for corrections.

2. Make your change. Keep one topic per pull request.

3. Sign your commits if you can. See [docs/verified-commits.md](docs/verified-commits.md).

4. Push and open a pull request against `main`. Fill in the [PR template](.github/pull_request_template.md) and link the issue it closes.

The **Lint & Test** check has to pass and all review conversations have to be resolved before a pull request can merge. Pull requests are squash merged.

## Writing style

The docs follow a few rules. Please match them:

- Write in the second person ("you"). Contractions are fine.
- Keep sentences and paragraphs short.
- Give the exact command or setting rather than linking to an external guide.
- Use fenced code blocks with a language tag, such as `bash`, `yaml` or `json`.
- No emoji, no marketing language.
- Assume the reader is a working developer. Skip the basics.

## Workflow and config changes

- Pin third-party actions to a full commit SHA and put the version in a comment, for example `uses: actions/checkout@<sha> # v7.0.1`.
- Give every workflow the smallest `permissions:` block it needs.
