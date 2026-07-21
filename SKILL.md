---
name: grepguard-skill
description: Run AI coding agents in GrepGuard's isolated cloud sandboxes and inspect their session logs. Use when a user asks to run, repeat, troubleshoot, or audit an agent task with the GrepGuard CLI, create or use GrepGuard namespaces and pods, or retrieve logs from a GrepGuard agent session.
---

# GrepGuard

## Overview

Use GrepGuard to execute agent work inside a disposable cloud sandbox. Treat the CLI as the source of truth for available commands and flags: this skill documents the stable workflow, not an exhaustive CLI reference.

## Install and sign in

Check whether the CLI is available with `grepguard --help`. If it is missing, install it only when the user has authorized installation:

```bash
npm install -g grepguard
```

Check whether the user is logged in:

```bash
grepguard auth status
```

If they are not logged in, authenticate interactively. Never ask for, print, store, or place an API key in a command, file, prompt, or log.

```bash
grepguard auth login
```

## Create a namespace

Use the namespace supplied by the user. If none is supplied, ask for one before creating it. Create a namespace only with clear authorization:

```bash
grepguard create namespace <namespace>
```

Wait for the namespace to become `Active` before using it. This may take a few seconds and sometimes up to one minute:

```bash
grepguard get ns
```

## Create a pod

Use the named pod. If the user asks for a fresh sandbox, create a clearly named disposable pod in the active namespace:

```bash
grepguard create pod <pod> --namespace <namespace>
```

## Configure Codex

When using Codex, set `CODEX_API_KEY` for the pod. If Codex needs to push to GitHub as the Sandbar Agent, also set `GIT_PAT`. Set each variable in a separate command:

```bash
grepguard env <sandbox> CODEX_API_KEY --namespace <namespace>
grepguard env <sandbox> GIT_PAT --namespace <namespace>
```

`grepguard env` securely prompts for each value, so it does not appear in shell history. Never include a secret value in a command, file, prompt, or log. You can use `-n <namespace>` instead of `--namespace <namespace>`.

## Run a task

Confirm the task, agent, pod, and namespace before running. Only use `codex` or `opencode` as the agent. Keep prompts focused and include the expected result:

```bash
grepguard run <pod> --agent <agent> --prompt "<task>" --namespace <namespace>
```

Logs can take some time to become available as agent is running in the sandbox. Check the completed run and summarize the result:

```bash
grepguard logs <pod> --agent <agent> --namespace <namespace>
```

## Delete resources

Delete a pod only with the user's authorization:

```bash
grepguard delete pod <sandbox> --namespace <namespace>
```

You can use `-n <namespace>` instead of `--namespace <namespace>`.

Delete a namespace only with the user's authorization:

```bash
grepguard delete ns <id_of_ns>
```

Check with `grepguard get ns` and wait for deletion to finish before reporting success. This may take a few seconds and sometimes up to one minute.

## Examples

Run a contained debugging task:

```bash
grepguard run auth-fix --agent codex --prompt "Investigate issue #4, implement a minimal fix, and report the changed files and tests run." --namespace acme-web
```

Review its record:

```bash
grepguard logs auth-fix --agent codex --namespace acme-web
```
