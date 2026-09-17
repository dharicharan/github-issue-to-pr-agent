# Autonomous GitHub Issue-to-PR Pipeline

An asynchronous agent service engineered in Python that converts labeled GitHub issues into verified, review-ready Pull Requests with automated test verification and strict budget ceilings.

## Features
- **HMAC Verified Webhooks**: Type-safe webhook receiver verifying `X-Hub-Signature-256` payloads.
- **Budget Ledger & Safety Gates**: Enforces daily dollar and PR rate limits per repository to prevent runaway agent loops.
- **Automated Sandbox Lifecycle**: Dispatches issue requirements into isolated scratch branches without write permissions to `main`.
- **Pre-PR Verification**: Runs automated test suites and coverage delta checks prior to dispatching pull requests.

## Architecture

```
GitHub Issue / PR Comment
          |
          v
+-----------------------------------------------------------+
|                  GitHub App Webhook Ingest                |
|  - HMAC Signature Verification (`X-Hub-Signature-256`)   |
|  - Rate & Budget Gatekeeper (Daily Dollar/PR Ceilings)    |
+-----------------------------+-----------------------------+
                              |
                              v
                +----------------------------+
                |    Isolated Cloud Sandbox  |
                |  - Dynamic Runtime Infer   |
                |  - Git Worktree Isolation  |
                +--------------+-------------+
                               |
                               v
                +----------------------------+
                |     SWE Agent Fix Loop     |
                |  - Diagnosis & Code Patch  |
                +--------------+-------------+
                               |
                               v
                +----------------------------+
                |     Verification Gate      |
                |  - CI Test Suite Check     |
                |  - Coverage Delta Delta >=0|
                +--------------+-------------+
                               |
                               v
                  Review-Ready Pull Request
```

## Quickstart

```bash
python main.py
```
