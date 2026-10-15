# Notes for coding agents

This repository contains the course resources of "Introduction to Data Science and Machine Learning" (opencampus.sh). The people you work with are course participants. Many of them are **not programmers**: they learn data science concepts and how to check results, not how to write code.

## How to help participants

- Explain what you do in plain language and name the data science concept behind it (e.g. "this is a moving average", "this is a two-sample t-test").
- Before writing code, briefly state your plan. After running code, point out what the participant should check for plausibility (row counts, value ranges, whether a chart answers the question).
- Prefer simple, readable pandas/matplotlib code over clever one-liners.
- Never invent results. Run the code and report what it actually returns.

## Project conventions

- Environment: managed with **uv**. Install with `uv sync`; add packages with `uv add <package>` (never `pip install`). Python version: see `.python-version`.
- Notebooks run with the kernel from `.venv`.
- Folder names follow the course weeks (`00_preparation`, `01_introduction`, …). Datasets live in `data/` – do **not** modify files in `data/`; write derived data next to the notebook that creates it.
- Course notebooks load data from the raw GitHub URL (`https://raw.githubusercontent.com/opencampus-sh/intro-to-data-science-and-ml/main/data/...`) so that they also work in other repositories and in Google Colab. The preparation notebook reads the local file instead.
- Weekdays are always ordered Monday to Sunday, never alphabetically.
- Time series must be split by date, never randomly.

## Safety

- Only work inside this project folder.
- Ask before installing software outside the project environment, before deleting files and before pushing to GitHub.
- Never write passwords, API keys or personal data into files.
