# 01. Running AI on a Personal Computer

This lesson covers running an AI model on a personal computer, with no account and no cost.

It is for anyone who can use a terminal but has never run AI locally. After this lesson, Ollama is installed, a real model answers questions on the machine, and the split between the software and the model is clear.

## Table of Contents

1. [What is an LLM?](#1-what-is-an-llm)
2. [The Two Parts: Software vs. Model](#2-the-two-parts-software-vs-model)
3. [Local LLM Software](#3-local-llm-software)
4. [Open Source Models](#4-open-source-models)
5. [Install Ollama and Run a First Model](#5-install-ollama-and-run-a-first-model)
6. [Installing and Running Multiple Models](#6-installing-and-running-multiple-models)
7. [Matching Models to Common Hardware Types](#7-matching-models-to-common-hardware-types)
8. [Running Two Gemma Models at the Same Time](#8-running-two-gemma-models-at-the-same-time)
9. [Common Mistakes](#9-common-mistakes)
10. [Where to Get Help](#10-where-to-get-help)
11. [Quick Reference Tables](#11-quick-reference-tables)

## 1. What is an LLM?

**LLM** stands for *Large Language Model*.

It is the AI brain that reads and writes text. The same kind of system sits behind ChatGPT, Gemini, and Claude. Type a question, it writes an answer.

The key idea to hold from the start: a working AI is actually **two separate pieces** joined together.

* The brain: the **model**
* The app that runs the brain: the **software**, more precisely called an **inference engine**

These two are separate things. That is why both matter.

## 2. The Two Parts: Software vs. Model

The easiest way to understand this is the **music software** analogy, like Windows Media Player on Windows or Music on macOS.

| Music world | AI world |
| --- | --- |
| **Music software** (music app) | **LLM software** (Ollama, LM Studio...) |
| **Song file** (`.mp3`) | **AI model** (Gemma, Llama...) |

The core principle:

> **Software** is like the music app. **The model** is like the song file it opens.

* One music app plays many different songs.
* One piece of software like Ollama runs many different models. Run Gemma today, switch to Qwen tomorrow.

Both are needed to do anything. A music app with no songs plays nothing. A song file with no music app will not open.

## 3. Local LLM Software

### What does "local" mean?

**Local** means the software runs **on the user's own computer**, without sending anything to the internet.

Unlike ChatGPT, where everything typed goes to a company server, running locally keeps **everything on the machine**.

* Private: data never leaves the computer.
* Free: no monthly subscription.
* Offline: works with no internet.
* Trade off: speed and quality depend on how powerful the machine is.

### What does the software do?

It handles all the technical work.

* Downloads the model to the machine.
* Loads the model into memory (RAM).
* Takes the question and feeds it to the model.
* Returns the result.

### The 4 most common tools

Pick one to start. They all run the same open source models.

| Tool | Interface | Best for |
| --- | --- | --- |
| **Ollama** | Command line | Simple, stable, lightweight. The easiest option that just works. |
| **LM Studio** | Graphical (GUI) | Beginners who prefer clicking over typing. Great for browsing and trying models. |
| **Jan** | Graphical (GUI) | A clean, open source desktop app. An alternative to LM Studio. |
| **GPT4All** | Graphical (GUI) | Runs on modest hardware. Comes with a Python option. |

> Common workflow: use a GUI tool like LM Studio to browse and try models, then switch to Ollama for everyday work once it feels familiar. Advanced tools like llama.cpp, vLLM, and LocalAI exist for experienced users. None are needed to start.

## 4. Open Source Models

### What is a model?

The model is the **AI brain**. It is the part that actually thinks and answers. In the analogy, it is the song file the music app opens.

### What does "open source" mean?

**Open source** (also called *open weight*) means the company that made the model **releases it publicly for anyone to download and use for free**, usually for both personal and commercial purposes.

The opposite is a **closed** model like OpenAI's GPT or Anthropic's Claude. Those work only through their service. They cannot be downloaded to a machine.

> Running AI locally requires an open source model. Closed models cannot be downloaded.

### Notable open source models

| Model | Made by | Notes |
| --- | --- | --- |
| **Gemma** | Google | Light, efficient, good for weaker machines |
| **Llama** | Meta (Facebook) | Popular, many variants |
| **Qwen** | Alibaba | Strong, good multilingual support |
| **Phi** | Microsoft | Very light, runs on low end machines |
| **DeepSeek** | DeepSeek | Strong at reasoning and coding |
| **Mistral** | Mistral AI | Solid and balanced, popular in production |

### A model comes in several sizes

Names like `gemma3:1b`, `gemma3:4b`, `qwen3:8b` appear in the library. The **B** stands for *billion*. It is the **number of parameters**, which roughly means **how large the brain is**.

* A higher number means smarter, but it needs a more powerful machine and runs slower.
* A lower number means a bit less capable, but it is light and fast on weaker machines.

Example: `4b` means the model has 4 billion parameters.

> There is also something called **quantization** (often shown as `Q4`). This technique compresses a model so it runs on ordinary machines. Software like Ollama handles quantization automatically, so it needs no manual setup.

## 5. Install Ollama and Run a First Model

Follow these steps. By the end, Ollama is installed and chatting with a real model.

### Step 1: Install Ollama

#### Windows

1. Go to <https://ollama.com/download>
2. Download the Windows installer (`OllamaSetup.exe`) and run it.
3. After installation, Ollama runs quietly in the background. Open **PowerShell** (or Command Prompt) to type commands.

To open PowerShell or Command Prompt:

1. Press the **Windows** key, or click the **Start** button.
2. Type `PowerShell`, then press **Enter** to open PowerShell.
3. To use Command Prompt instead, type `cmd`, then press **Enter**.
4. When the window opens, type commands like `ollama --version`.

![Open PowerShell or Command Prompt on Windows](../../images/0101.png)

#### Mac

1. Go to <https://ollama.com/download>
2. Download the macOS version, open the `.zip`, and drag **Ollama** into the Applications folder.
3. Launch it once (it appears in the menu bar). Then open the **Terminal** app to type commands.

Confirm the install worked (same command on both platforms):

```bash
ollama --version
```

### Step 2: See available open source models

Ollama keeps a public library of models to download.

* Browse online: visit <https://ollama.com/library> to see every available model, its sizes, and exact tags (like `gemma3:270m`).
* See what is already installed:

```bash
ollama list
```

Note: `ollama list` only shows models already on the machine. To find new models to download, use the online library above.

### Step 3: Install gemma3:270m

This downloads Google's tiny 270 million parameter Gemma model (about 290 MB):

```bash
ollama pull gemma3:270m
```

### Step 4: Chat with it

```bash
ollama run gemma3:270m
```

This opens an interactive chat. Type a message, press Enter, and the model replies. To leave the chat, type:

```text
/bye
```

### PowerShell sample (Windows)

The full sequence in Windows PowerShell, from start to finish:

```powershell
# Check Ollama is installed
ollama --version

# Download the tiny Gemma model
ollama pull gemma3:270m

# See what is installed on the machine
ollama list

# Start chatting (type /bye to exit)
ollama run gemma3:270m
```

Ask a single question without entering chat mode:

```powershell
ollama run gemma3:270m "Explain what an LLM is in one sentence."
```

> `gemma3:270m` is very small, so keep questions short and simple. For better answers, install a larger model later (see Section 7) and run it the same way.

## 6. Installing and Running Multiple Models

This is three different questions that people often mix up.

### a) Installing (downloading): practically unlimited

Installing a model means **saving its files to the hard drive**. The only limit is **disk space**.

Each small model is only a few GB. A typical drive holds dozens or even hundreds of models. They sit on disk and use **no RAM** until they actually run. In the music analogy: this is how many songs sit in storage.

### b) Running at the same time: limited by memory

To run a model, it must be **loaded into memory** (RAM for CPU use, or VRAM for GPU use). Memory is limited.

Ollama can load several models at once. By default it allows up to 3 models loaded at the same time on a CPU machine. But this only works if they fit in available memory. That condition is the real limit.

The number 3 is just a ceiling. The **actual limit is available memory**. A powerful machine with lots of RAM or VRAM runs several at once. A modest machine runs only one.

### c) Switching between models: the software handles it automatically

Models do not open and close by hand. Ollama manages that. If a request needs a new model but memory is short, Ollama **automatically unloads idle models to free space**, then loads the new one.

Calling model A loads A. Calling model B when memory cannot hold both quietly unloads A and loads B. This happens in the background and costs a few seconds of reload time. Run `ollama ps` to see which models sit in memory.

## 7. Matching Models to Common Hardware Types

The single biggest factor is **memory**: system RAM when there is no graphics card, or **VRAM** (memory on a dedicated GPU) when there is one. A GPU is far faster than a CPU for running models. Models that fit in VRAM run much quicker. Always use the default **Q4** quantized version to save memory.

Below are four common machine categories. Find the closest match.

### Type 1: No dedicated GPU (CPU and RAM only)

Office laptops, older desktops, and machines with only integrated graphics. Everything runs on the CPU, which works but is slow. Stay with smaller models.

* Sweet spot: **1B to 4B** models, for example `gemma3:1b`, `gemma3:4b`, `llama3.2:3b`, `qwen3:4b`
* Possible but slow: a single **7B to 8B** model, for example `qwen3:8b`
* Avoid: anything larger

### Type 2: Entry or mid range GPU (about 6 to 8 GB VRAM)

Many gaming laptops and budget desktop cards, for example an RTX 3050 or 3060 class GPU.

* Comfortable: **7B to 8B** models, for example `qwen3:8b`, `llama3.1:8b`, `phi-4`
* Possible: up to about **12B to 14B** quantized, for example `gemma3:12b`

### Type 3: High end GPU (about 16 to 24 GB VRAM)

Enthusiast desktop cards, for example an RTX 3090 or 4090 class GPU.

* Comfortable: **27B to 32B** models, for example `gemma3:27b`, `qwen2.5-coder:32b`
* Possible but slower: a **70B** model at Q4, for example `llama3.3:70b`

### Type 4: Apple Silicon Mac (M series, unified memory)

On these Macs the CPU and GPU **share the same memory**. Total RAM is what matters. They are surprisingly capable for their size.

* 16 GB RAM: comfortable with **7B to 14B** models
* 32 GB or more: handles **27B to 70B** models
* Tip: **Apple MLX** is usually the fastest option on these chips, though Ollama works well too

### General rule of thumb

> Pick the **largest model that fits in memory with room to spare**. If responses are too slow or the machine struggles, step down one size. If it runs easily, try the next size up.

## 8. Running Two Gemma Models at the Same Time

A practical example: installing **and running** both `gemma3:270m` (the tiny nano model from Section 5) and `gemma3:4b` (the 4 billion parameter model) at once. This works on most machines because the nano model is very small.

### Installing both

Installing just downloads files to disk. These two are small:

* `gemma3:270m`: about 290 MB
* `gemma3:4b`: about 3.3 GB

Download them with:

```bash
ollama pull gemma3:270m
ollama pull gemma3:4b
```

See everything installed on disk:

```bash
ollama list
```

### Running them

Run a model by name (type `/bye` to exit the chat):

```bash
ollama run gemma3:270m
```

To use the other one:

```bash
ollama run gemma3:4b
```

### Can both be loaded into memory at once?

Usually yes. Memory limits how many models run at the same time, but `gemma3:270m` is so small that **both fit comfortably** even on a modest machine. Rough cost: about 300 MB for the nano model plus about 4 GB for the 4b model, which is under 5 GB total. Ollama allows up to 3 models loaded at once on a CPU machine by default, so it keeps both in memory while both are in use.

Check what is currently **loaded in memory** (not just installed on disk):

```bash
ollama ps
```

This shows each loaded model, its size, and a countdown until it automatically unloads. Ollama frees a model after about 5 minutes of inactivity.

### Why this combination is useful

* Use `gemma3:270m` for quick, simple tasks. It is fast but limited in quality.
* Use `gemma3:4b` when better answers matter. It is slower but noticeably smarter. This is the everyday model.

Keep two terminal windows open, one per model, and they coexist in memory. Or run whichever one is needed and let Ollama handle loading and unloading automatically.

## 9. Common Mistakes

* Running a model larger than available memory. The machine slows to a crawl or the model fails to load. Pick a smaller size, and check `ollama ps` to see what is loaded.
* Leaving off the size tag. `ollama run gemma3` pulls a default that may be large. Always name the exact tag, for example `gemma3:270m`.
* Expecting a tiny model to answer like ChatGPT. `gemma3:270m` is fast but limited. Step up to `gemma3:4b` for better answers.
* Forgetting that a model stays in memory. Ollama keeps a model loaded for about 5 minutes after the last use. Check with `ollama ps`.
* Closing the terminal expecting Ollama to stop. Ollama runs as a background service. The model unloads on its own after inactivity.

## 10. Where to Get Help

* Official download and docs: <https://ollama.com>
* Full model list with sizes and tags: <https://ollama.com/library>
* Source code and issue tracker: <https://github.com/ollama/ollama>
* Run `ollama help` for the full list of commands.

## 11. Quick Reference Tables

### Software vs. Model

| | LLM Software | Open Source Model |
| --- | --- | --- |
| **What is it?** | The tool that runs the AI | The AI brain itself |
| **Examples** | Ollama, LM Studio, Jan, GPT4All | Gemma, Llama, Qwen, Phi |
| **Analogy** | Music app | Song file |
| **How many to install?** | Just one is enough | Download as many as needed |
| **Decides what?** | How to interact (CLI vs GUI) | How capable the AI is |

### Essential Ollama commands

| Command | What it does |
| --- | --- |
| `ollama --version` | Confirm Ollama is installed |
| `ollama pull <model>` | Download a model (e.g. `gemma3:270m`) |
| `ollama list` | Show models installed on the machine |
| `ollama run <model>` | Start chatting with a model |
| `ollama ps` | Show which models are loaded in memory |
| `/bye` | Leave the chat |

### Model size by hardware

| Hardware | Comfortable model size |
| --- | --- |
| No GPU (CPU and RAM) | 1B to 4B |
| Entry and mid range GPU (6 to 8 GB VRAM) | 7B to 8B |
| High end GPU (16 to 24 GB VRAM) | 27B to 32B (up to 70B) |
| Apple Silicon Mac | 7B to 70B depending on RAM |

### Summary

> **Software** (like Ollama) is like the music app. An **open source model** (like Gemma) is like the content it opens. Install the software once, then download as many models as needed. The setup runs on a local machine: private, free, and offline. Downloading is unlimited. Running several at once is limited by memory.
