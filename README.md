# mlflow-claude-tracer

A lightweight starter project for testing Claude Code tracing with MLflow.

## Overview

This repository demonstrates how to connect Claude Code sessions with MLflow tracking so you can inspect runs, traces, and related metadata from a local MLflow backend.

## Features

- Configures Claude via [.claude/settings.json](.claude/settings.json) with MLflow environment variables.
- Registers a stop hook so Claude can trigger MLflow's Claude autologging workflow when a session ends.
- Uses a local MLflow tracking backend backed by the SQLite database in this repository.
- Writes MLflow artifacts and metadata to [mlartifacts](mlartifacts) and [mlflow.db](mlflow.db).

## Project structure

- [main.py](main.py): a simple example entrypoint.
- [pyproject.toml](pyproject.toml): Python project configuration and dependency definition.
- [.claude/settings.json](.claude/settings.json): Claude settings that enable MLflow tracing and hook registration.
- [mlartifacts](mlartifacts): directory where MLflow artifacts are stored.
- [mlflow.db](mlflow.db): local SQLite tracking database used by MLflow.

## How it works

1. The project enables MLflow tracing through Claude's settings file.
2. When Claude is launched from the repository root, the configured hook triggers MLflow's Claude autologging workflow.
3. MLflow records session metadata and stores it in the configured tracking backend.
4. You can inspect the results in the MLflow UI or by reading the local tracking files.

## Prerequisites

Make sure the following tools are installed and available on your system:

- [uv](https://docs.astral.sh/uv/) for managing the Python environment and dependencies
- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) for running Claude from the terminal

You can verify they are installed with:

```bash
uv --version
claude --version
```

## Quick start

Install dependencies:

```bash
uv sync
```

Run the sample script:

```bash
uv run python main.py
```

To inspect the MLflow tracking data locally, start the UI:

```bash
uv run mlflow ui --host 127.0.0.1 --port 5000
```

Then open http://127.0.0.1:5000 in your browser.

## Reference

Official MLflow documentation for Claude Code tracing:

- https://mlflow.org/docs/latest/genai/tracing/integrations/listing/claude_code/
