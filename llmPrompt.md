Saved Continuation Prompt – Cross-Repo Task Orchestrator + Claude Workflow

I’m building a GitHub-based tasks workflow that can coordinate work across multiple repos using Claude Code.

Goal

Create a new repo tcm-orchestration that hosts “task chain” Issues.

When an Issue is created/edited, an orchestrator workflow parses a YAML block in the Issue body (tasks list).

For each task, it triggers a per-repo bootstrap-pr.yml workflow (via workflow_dispatch) to:

create a branch

make an empty commit

open a PR

add PR body metadata (TCM-ISSUE: owner/repo#num, TCM-TASK: id)

post a Claude comment depending on claude.mode:

safe: auto post the real @claude ...

unsafe: post a prepared comment (does NOT trigger) and require label claude:run

manual: no comment

When PRs merge/close, callback workflows should update the orchestration Issue:

tick off the completed task

unlock dependent tasks and create the next PRs automatically

Repos

Rails: app/server

React monorepo: app/monorepo

Scraper API: tcm-scraper

Scraper web: tcm-scraper-web
Each repo will include the same bootstrap-pr.yml.

Current state / blocker

I pushed bootstrap-pr.yml but GitHub reports “Invalid workflow file … YAML syntax error on line 96”.

Likely culprit is the if: expression for posting Claude comment. We need to fix the workflow to validate.

Next steps: finalize bootstrap-pr.yml so it validates; replicate it to all repos; then implement tcm-orchestration orchestrate workflow (issue parser + dispatcher) using ORCH_TOKEN (fine-grained PAT stored as repo secret).

What I want from you

Provide minimal, correct workflow YAML (GitHub Actions-valid) and step-by-step fixes.

Keep it pragmatic: small, deterministic, no extra features until base flow works.