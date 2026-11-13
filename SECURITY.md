# Security Policy

## Supported versions

This repository is a template, so there are no releases. Only the current `main` branch is supported. Fixes land on `main` and are not backported.

## What counts as a security issue

The template has no application code, but its workflows and guidance can still be wrong in ways that matter. Report it privately if you find, for example:

- A workflow in `.github/workflows/` that could leak secrets, run untrusted code with write permissions, or be abused through a pull request from a fork.
- Documentation or example configuration that would leave a repo less protected than it claims, such as a ruleset that doesn't block what the docs say it blocks.

Typos, unclear wording and feature ideas are not security issues. Open a normal issue for those.

## How to report

Use GitHub's private vulnerability reporting:

1. Go to the **Security** tab of this repository.
2. Click **Report a vulnerability**.
3. Describe the problem, the affected file, and how to reproduce it.

Please don't open a public issue or pull request for a security problem until it has been fixed.

## What happens next

You should get a reply within 7 days. Once the problem is confirmed, the fix goes into `main` and you're credited in the advisory unless you'd rather not be.

## If you use this template

Your copy of this file describes this project's process, not yours. Update it before you publish your own repository, and turn on private vulnerability reporting in the **Security** section of your repository settings so the **Report a vulnerability** button exists.
