# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`clean-repo-standard` is a **GitHub repository template** (not a software library or application) that defines secure branch protection and workflow standards for small teams (1-10 people). It is framework-agnostic and contains configuration files, documentation, and example configs rather than application code.

## Repository Purpose

Provides battle-tested patterns for:
- Branch protection rules (`main` fully protected, no direct pushes)
- PR-based workflow: `feature/*` or `fix/*` → `dev` → `main` → production
- Verified/signed commits
- CI enforcement on PRs
- Standardized PR templates

## Repository Structure

```
.github/
  pull_request_template.md   — PR template (summary, risk, testing, rollback)
  workflows/
    ci.yml                   — CI workflow: runs on PRs to dev and main
docs/
  branch-protection.md       — GitHub UI walkthrough for protecting main and dev
  dev-to-main-flow.md        — Branching workflow, merge strategies, hotfix process
  verified-commits.md        — SSH and GPG commit signing setup
CLAUDE.md                    — Guidance for Claude Code (this file)
LICENSE                      — MIT license
README.md                    — Project overview, quick start, FAQ
```

## Writing Style

- Second person ("you"), contractions are fine
- Short sentences, short paragraphs
- No corporate jargon, no emoji
- Provide exact commands rather than linking to external guides
- GitHub Flavored Markdown with `#` headers and fenced code blocks with language tags
- Target audience: developers who are practical, not beginners — skip the basics

## Architecture Notes

This is a **template repo**, not a codebase with build/test/lint commands. Contributions are documentation and GitHub configuration files (YAML workflows, markdown templates, JSON branch protection configs). There is no application source code, package manager, or build system.

## Branching Model

- `main` — production-ready, protected, merge via PR only
- `dev` — integration branch, all feature work merges here first
- `feature/*`, `fix/*` — short-lived branches off `dev`

## Git Attribution

- Never include `Co-Authored-By` lines referencing Claude, Anthropic, or any AI tool in commit messages.
- Commits must appear as if written solely by the repository owner.
- Do not add AI-related metadata, tags, or footers to any commit, PR, or issue.
