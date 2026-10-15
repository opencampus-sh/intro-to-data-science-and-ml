# Introduction to Data Science and Machine Learning – Course Resources

Example notebooks, datasets and the Python environment for the course **Introduction to Data Science and Machine Learning** at [opencampus.sh](https://edu.opencampus.sh).

- **Course handbook** (weekly tasks, videos, requirements): [GitBook](https://opencampus.gitbook.io/opencampus-machine-learning-program/courses/einfuehrung)
- **Enrolment, course room link and project submission:** [edu.opencampus.sh](https://edu.opencampus.sh)
- **Team project:** in week 3 every team creates its own repository from the [project template](https://github.com/opencampus-sh/repo-template-intro-to-data-science-and-ml). This repository here contains only the course resources.

## Setup

You need your own laptop with VS Code (or Cursor), Git, [uv](https://docs.astral.sh/uv/getting-started/installation/) and a coding agent installed – see the [Preparation page](https://opencampus.gitbook.io/opencampus-machine-learning-program/courses/einfuehrung/vorbereitung) in the course handbook.

### 1. Get the repository onto your laptop

Choose one of these options:

- **With VS Code:** open VS Code, click *Clone Git Repository…* on the welcome page (or press `Ctrl+Shift+P` / `Cmd+Shift+P` and type *Git: Clone*), paste `https://github.com/opencampus-sh/intro-to-data-science-and-ml` and choose a folder. Open the cloned folder when VS Code asks.
- **With your coding agent:** open an empty folder in VS Code, start the agent and ask: *"Clone https://github.com/opencampus-sh/intro-to-data-science-and-ml into this folder and open it."*
- **With the terminal:** `git clone https://github.com/opencampus-sh/intro-to-data-science-and-ml`

### 2. Let the agent set up the environment

Open the folder in VS Code, start your coding agent and paste this prompt:

```text
Please set up this course repository on my computer:
1. Check that uv is installed (`uv --version`). If it is missing, tell me how to install it on my operating system and wait until I have done it.
2. Run `uv sync` to install the right Python version and all packages into the .venv folder of this project.
3. Check that the VS Code extensions "Python" and "Jupyter" are installed; if not, tell me how to install them.
4. Open 00_preparation/pedestrians_kiel_holstenstrasse.ipynb, select the Python interpreter from .venv as the kernel and run all cells.
5. If anything fails, explain the problem in simple words and fix it. Do not change anything outside this project folder and ask me before installing software.
```

Without an agent: run `uv sync` in the project folder, open the notebook, select the kernel from `.venv` and click *Run All*.

### Fallback: GitHub Codespaces

If you cannot install software on your laptop, click *Code → Codespaces → Create codespace on main* on GitHub. The configuration in `.devcontainer/` sets up the same environment in your browser.

## Contents

| Folder | Course week | Content |
| --- | --- | --- |
| `00_preparation/` | Preparation | Pedestrians in Kiel's Holstenstraße – first notebook to test your setup |
| `01_introduction/` | 1 | Comparing the temperatures of July and May (t-test) |
| `02_visualization/` | 2 | Example plots with matplotlib and seaborn |
| `05_time_series/` | 5 | Time series of pedestrian counts |
| `06_linear_regression/` | 6 | Linear regression (OLS) and interaction effects |
| `07_overfitting/` | 7 | Overfitting and feature selection |
| `08_neural_networks/` | 8 | Data preparation and training of neural networks (TensorFlow/Keras) |
| `09_missing_values/` | 9 | Imputation of missing values and evaluation of the imputation |
| `data/` | – | All datasets, see [data/README.md](data/README.md) |
| `archive/` | – | Material from the former R version of the course |

## Using the data in your own repository

Notebooks can load the data directly from GitHub, so it works in any repository, for example:

```python
import pandas as pd

BASE_URL = "https://raw.githubusercontent.com/opencampus-sh/intro-to-data-science-and-ml/main/data/bakery/"
sales = pd.read_csv(BASE_URL + "umsatzdaten_gekuerzt.csv")
weather = pd.read_csv(BASE_URL + "wetter.csv")
kiel_week = pd.read_csv(BASE_URL + "kiwo.csv")
```
