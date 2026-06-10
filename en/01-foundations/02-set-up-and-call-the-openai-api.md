# 02. Set Up the Tools and Call the OpenAI API

This lesson sets up a coding environment and makes a first call to the OpenAI API from a notebook.

It is for anyone who finished lesson 01 and can use a terminal, but has never written code that talks to an AI service. After this lesson, Git, Cursor, and uv are installed, an OpenAI API key works, and a notebook prints a real answer from a model in the cloud.

## Table of Contents

1. [Local Model vs API: The Difference](#1-local-model-vs-api-the-difference)
2. [Tools Installed in This Lesson](#2-tools-installed-in-this-lesson)
3. [Install Git and GitHub Desktop](#3-install-git-and-github-desktop)
4. [Install Cursor](#4-install-cursor)
5. [Install uv](#5-install-uv)
6. [Get an OpenAI API Key](#6-get-an-openai-api-key)
7. [Create a Project and Set Up the Environment](#7-create-a-project-and-set-up-the-environment)
8. [Add the API Key in a .env File](#8-add-the-api-key-in-a-env-file)
9. [Install the Cursor Extensions](#9-install-the-cursor-extensions)
10. [What is an .ipynb File?](#10-what-is-an-ipynb-file)
11. [Select the Kernel](#11-select-the-kernel)
12. [Make the First OpenAI API Call](#12-make-the-first-openai-api-call)
13. [Example: Ask About the World Cup 2026](#13-example-ask-about-the-world-cup-2026)
14. [Common Mistakes](#14-common-mistakes)
15. [Where to Get Help](#15-where-to-get-help)
16. [Quick Reference](#16-quick-reference)

## 1. Local Model vs API: The Difference

Lesson 01 ran a model on the local machine with Ollama. The model lived on disk and answered with no internet.

This lesson does the opposite. It calls a model that runs on OpenAI's servers. The code sends a question over the internet and gets an answer back.

| | Local model (lesson 01) | API (this lesson) |
| --- | --- | --- |
| Where the model runs | On the machine | On OpenAI servers |
| Internet needed | No | Yes |
| Cost | Free | Pay per use |
| Model quality | Limited by the hardware | Large, powerful models |
| Privacy | Data stays on the machine | Data sent to OpenAI |

Both approaches matter. Local is private and free. The API gives access to stronger models without strong hardware.

> The API charges money per request. The amounts are tiny for learning, often a fraction of a cent per call. A billing setup is still required. See section 6.

## 2. Tools Installed in This Lesson

Install these once. They form a standard setup for any Python AI project later.

| Tool | What it is | Why it is needed |
| --- | --- | --- |
| **Git** | Version control software | Tracks changes to code over time |
| **GitHub** | A website that hosts Git projects | Stores and shares code online |
| **GitHub Desktop** | An app with buttons for Git | Uses Git without typing commands |
| **Cursor** | A code editor with AI built in | Writes and runs the code |
| **uv** | A Python package manager | Installs Python and libraries fast |

> Cursor is a code editor based on VS Code, with an AI assistant added. Anything that works in VS Code works in Cursor.

## 3. Install Git and GitHub Desktop

### What is Git?

**Git** is software that records the history of a project. It saves snapshots of the code so any version can be recovered later. It runs on the local machine.

### What is GitHub?

**GitHub** is a website that stores Git projects online. It is the place where code lives in the cloud, so it can be backed up and shared. A free account is enough.

### What is GitHub Desktop?

**GitHub Desktop** is an app that does Git actions with buttons instead of typed commands. It is the friendly way to save work to GitHub. It also installs Git automatically.

### Steps

1. Create a free GitHub account at <https://github.com>
2. Download GitHub Desktop from <https://desktop.github.com>
3. Install it and sign in with the GitHub account.
4. Installing GitHub Desktop also installs Git, so no separate Git install is needed.

Confirm Git is installed. Open a terminal and run:

```bash
git --version
```

A version number means Git is ready.

## 4. Install Cursor

**Cursor** is the code editor used for the rest of this guide. It looks and works like VS Code, with an AI assistant on the side.

1. Download Cursor from <https://cursor.com>
2. Install it and open it once.
3. Sign in when asked. The free tier is enough to start.

> Anyone who already uses VS Code can use it instead. The extensions and steps are identical. Cursor is the default here because of the built in AI help.

## 5. Install uv

**uv** is a tool that installs Python and manages project libraries. It is fast and handles the tricky parts automatically. It creates an isolated space per project so libraries never clash.

### Windows

Open PowerShell and run:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### Mac

Open the Terminal app and run:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Close the terminal, open a new one, then confirm it works:

```bash
uv --version
```

> uv installs Python too, so a separate Python install is not required. uv downloads the right version when the project needs it.

## 6. Get an OpenAI API Key

An **API key** is a secret password that proves who is calling the API. The code sends it with every request so OpenAI knows which account to bill.

1. Create an account at <https://platform.openai.com>
2. Add a small amount of credit under **Billing**. A few dollars covers a lot of learning.
3. Go to <https://platform.openai.com/api-keys>
4. Click **Create new secret key**, give it a name, and copy the key.
5. Save the key somewhere safe right away. The website shows it only once.

> Treat the key like a password. Never paste it into a public place. Never commit it to GitHub. Section 8 shows the safe way to store it.

## 7. Create a Project and Set Up the Environment

A **project** is a folder that holds the code, its libraries, and its settings. uv creates and manages this folder.

Open a terminal and run these commands one by one:

```bash
uv init world-cup-api
cd world-cup-api
uv add openai python-dotenv ipykernel
```

What each command does:

* `uv init world-cup-api` creates a new project folder named `world-cup-api`.
* `cd world-cup-api` moves into that folder.
* `uv add ...` installs three libraries into the project:
  * **openai**: the official library for calling the OpenAI API.
  * **python-dotenv**: reads secrets from a `.env` file.
  * **ipykernel**: lets notebooks run inside this project.

uv creates a hidden folder named `.venv` inside the project. This is the **virtual environment**, an isolated space that holds the project's libraries. It keeps this project separate from every other one.

Now open the project folder in Cursor:

1. In Cursor, choose **File**, then **Open Folder**.
2. Pick the `world-cup-api` folder.

## 8. Add the API Key in a .env File

A **`.env` file** is a plain text file that stores secrets, like the API key. Code reads from it, but the file itself never goes online.

1. In Cursor, create a new file in the project folder named exactly `.env`
2. Add this single line, pasting the real key after the equals sign:

```text
OPENAI_API_KEY=sk-paste-your-real-key-here
```

3. Save the file.

Keep the key out of GitHub. The `.env` file must never be uploaded.

* `uv init` already created a `.gitignore` file, which lists files Git should ignore.
* Open `.gitignore` and confirm a line with `.env` is present. If it is missing, add it on its own line:

```text
.env
```

> The reason: anyone who gets the key can spend money on the account. The `.gitignore` entry tells Git to skip the `.env` file, so the secret stays on the machine.

## 9. Install the Cursor Extensions

An **extension** adds a feature to Cursor. Two are needed to run notebooks and Python.

1. In Cursor, click the **Extensions** icon in the left bar. It looks like four squares.
2. Search for and install each of these, both published by Microsoft:
   * **Python** (Microsoft): runs and understands Python code.
   * **Jupyter** (Microsoft): runs notebook files.
3. Reload Cursor if it asks.

## 10. What is an .ipynb File?

An **`.ipynb` file** is a Jupyter notebook. It is a document that mixes runnable code with text and results, all in one place.

### How it works

A notebook is a stack of **cells**. Each cell is one of two types:

* **Code cell**: holds code. Run it and the result appears right below.
* **Markdown cell**: holds notes, written in Markdown, the same format as a `.md` file.

Run cells one at a time. The output, whether text, a number, or an error, stays attached under each cell. This makes a notebook ideal for learning. Change one cell, run it, and see the effect at once.

### Does it work on GitHub?

Yes. GitHub renders `.ipynb` files as a readable page. It shows the code, the notes, and the saved outputs together. So a notebook pushed to GitHub looks like a finished report, not raw code.

### Notebook vs Markdown

| | `.md` (Markdown) | `.ipynb` (Notebook) |
| --- | --- | --- |
| Holds text | Yes | Yes |
| Holds runnable code | No, code is shown but not run | Yes, code runs in place |
| Shows results | No | Yes, saved under each cell |
| Best for | Writing and docs | Experiments and learning |
| Under the hood | Plain text | A JSON file |

> A `.md` file is for writing that people read. An `.ipynb` file is for code that runs while writing notes around it. This lesson uses a notebook so each API call runs and shows its answer on the spot.

## 11. Select the Kernel

A **kernel** is the engine that runs the code in a notebook. The notebook must use the project's kernel so it can find the installed libraries.

1. In Cursor, create a new file named `main.ipynb` in the project folder.
2. Open it. A button labeled **Select Kernel** appears at the top right.
3. Click it, then choose **Python Environments**.
4. Pick the one that points to `.venv`, usually shown as **.venv (Python)**.

> The `.venv` kernel is the project's own environment from section 7. It is the only one with `openai` installed. Picking any other kernel leads to a "module not found" error.

## 12. Make the First OpenAI API Call

The notebook is ready. Time to send a question to the model.

In the first code cell, paste this and run it:

```python
from dotenv import load_dotenv
from openai import OpenAI

# Read the key from the .env file into the environment
load_dotenv()

# Create the client. It finds OPENAI_API_KEY automatically.
client = OpenAI()

# Send a question to the model
response = client.responses.create(
    model="gpt-4o-mini",
    input="Say hello in one short sentence."
)

# Print the model's answer
print(response.output_text)
```

What each part does:

* `load_dotenv()` loads the secret from the `.env` file.
* `OpenAI()` creates the **client**, the object that talks to the API. It reads the key on its own.
* `client.responses.create(...)` sends the request. `model` picks which AI to use. `input` is the question.
* `response.output_text` is the answer text. `print` shows it.

Run the cell. After a short wait, a greeting from the model appears below the cell.

> `gpt-4o-mini` is a small, cheap, fast model. It is a good default for learning. To use a stronger model later, change the `model` value. See <https://platform.openai.com/docs/models> for the current list.

## 13. Example: Ask About the World Cup 2026

A real question shows the API doing useful work. The 2026 FIFA World Cup is a good test because it is a recent event with a new format.

Add a new cell, paste this, and run it:

```python
response = client.responses.create(
    model="gpt-4o-mini",
    input=(
        "The 2026 FIFA World Cup is hosted by the United States, Canada, and Mexico. "
        "Answer in three short bullets: "
        "how many teams play in 2026, "
        "how many teams played in 2022, "
        "and what is new about the 2026 format."
    )
)

print(response.output_text)
```

The model replies with the facts: 48 teams in 2026, up from 32 in 2022, the largest World Cup so far.

Try changing the question. Ask about a favorite team, the host cities, or the match schedule. Each run sends a fresh request and prints a fresh answer.

> The model knows general facts from its training, but not live results. For scores happening right now, the model alone is not enough. Later lessons add live data to fix this.

## 14. Common Mistakes

* Forgetting to add billing credit. The API returns a quota error. Add a few dollars under Billing at <https://platform.openai.com>.
* Picking the wrong kernel. A "module not found" error for `openai` means the notebook is not on the `.venv` kernel. Reselect it in the top right.
* Naming the secret file wrong. It must be exactly `.env`, with the dot and nothing before it. A file named `env.txt` will not load.
* Committing the `.env` file. Check that `.gitignore` lists `.env` before pushing to GitHub. A leaked key can cost real money.
* Running cells out of order. The first cell creates the `client`. Run it before any cell that uses `client`, or the notebook reports `client` is not defined.
* Pasting the key with extra spaces or quotes. The line is `OPENAI_API_KEY=sk-...` with no spaces and no quotes around the key.

## 15. Where to Get Help

* OpenAI API docs: <https://platform.openai.com/docs>
* Model list and prices: <https://platform.openai.com/docs/models>
* uv docs: <https://docs.astral.sh/uv>
* Cursor docs: <https://docs.cursor.com>
* GitHub Desktop docs: <https://docs.github.com/en/desktop>

## 16. Quick Reference

### Setup commands

| Command | What it does |
| --- | --- |
| `git --version` | Confirm Git is installed |
| `uv --version` | Confirm uv is installed |
| `uv init <name>` | Create a new project folder |
| `uv add <library>` | Install a library into the project |
| `uv add openai python-dotenv ipykernel` | Install the libraries this lesson needs |

### The full notebook

```python
from dotenv import load_dotenv
from openai import OpenAI

load_dotenv()
client = OpenAI()

response = client.responses.create(
    model="gpt-4o-mini",
    input="Say hello in one short sentence."
)

print(response.output_text)
```

### Summary

> Install Git, Cursor, and uv once. Create a project with uv, store the key in a `.env` file, and keep that file out of GitHub. Open an `.ipynb` notebook, select the `.venv` kernel, and run a cell. The code sends a question to OpenAI and prints the answer. Unlike the local model in lesson 01, this runs in the cloud, costs a little money, and gives access to far stronger models.
