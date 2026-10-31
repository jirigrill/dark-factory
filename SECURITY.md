# Security policy

## Scope

This repository holds design documentation for an autonomous software factory. Security reports are in scope when they concern:

- a flaw in the design that could let an agent escape its guardrails, reach secrets, or change its own permissions
- a supply-chain, prompt-injection or workflow-injection weakness in the described pipeline
- a misconfiguration of this repository (permissions, branch protection, secret scanning, Actions policy)

## Reporting a vulnerability

Use GitHub's private vulnerability reporting: open the **Security** tab and choose **Report a vulnerability**. Do not open a public issue, and do not include exploit details in a pull request or discussion.

Please include the affected section of the spec (or repository setting), the impact, and a suggested fix if you have one.

## What to expect

- Acknowledgement within 7 days.
- A fix or a documented decision within 30 days for confirmed design issues.
- Credit in the repository once the issue is resolved, if you want it.

## Secrets and credentials

This repository should never contain credentials, tokens, private keys or production data. If you find one, report it privately and do not copy it elsewhere. Any exposed credential is treated as compromised and rotated.

## Supported versions

There are no releases yet. The design draft on `main` is the only supported version.
