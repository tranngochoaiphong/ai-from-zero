# 01. Running AI on Your Own Computer

## Table of Contents

1. [What is an LLM?](#1-what-is-an-llm)
2. [The Two Parts: Software vs. Model](#2-the-two-parts-software-vs-model)
3. [Local LLM Software](#3-local-llm-software)
4. [Open-Source Models (the "content")](#4-open-source-models-the-content)
5. [Getting Started: Install Ollama and Run Your First Model](#5-getting-started-install-ollama-and-run-your-first-model)
6. [How Many Models Can You Install / Run at Once?](#6-how-many-models-can-you-install--run-at-once)
7. [Matching Models to Common Hardware Types](#7-matching-models-to-common-hardware-types)
8. [Running Two Gemma Models at the Same Time](#8-running-two-gemma-models-at-the-same-time)
9. [Quick Reference Tables](#9-quick-reference-tables)

---

## 1. What is an LLM?

**LLM** = *Large Language Model*.

It is the "AI brain" that can read and write text — the same kind of thing behind ChatGPT, Gemini, or Claude. You type a question, it writes an answer.

The key idea to remember from the very start: a working AI is actually **two separate pieces** joined together:

- **The "brain"**: the **model**
- **The app that runs the brain**: the **software**

These two are separate things. That's why you need to understand both.

---

## 2. The Two Parts: Software vs. Model

The easiest analogy is **music software** like Windows Media Player on Windows or Music on macOS:

| Music world | AI world |
|---|---|
| **Music software** (music app, etc.) | **LLM software** (Ollama, LM Studio...) |
| **Song file** (`.mp3`) | **AI model** (Gemma, Llama...) |

The core principle:

> **Software** is like the *music app*. **The model** is like the *song file* it opens.

- One music app can play many different songs.
- Likewise, **one piece of software like Ollama can run many different models** — run Gemma today, switch to Qwen tomorrow, your choice.

You need **both** to do anything. A music app with no songs plays nothing; a song file with no music app will not open.

---

## 3. Local LLM Software

### What does "local" mean?

**Local** = it runs **on your own computer**, without sending anything to the internet.

Unlike ChatGPT (where everything you type goes to a company's server far away), running locally keeps **everything on your machine**. Benefits and trade-offs:

- Private: your data never leaves your computer
- Free: no monthly subscription
- Offline: works with no internet
- Trade-off: speed and intelligence depend on how powerful your machine is

### What does the software actually do?

It handles all the technical work so you don't have to:

- Downloads the model to your machine
- Loads the model into memory (RAM)
- Takes your question and feeds it to the model
- Returns the result to you

### The 4 most common tools

These are the ones a beginner is most likely to meet. Pick one to start; they all run the same open-source models.

| Tool | Interface | Best for |
|---|---|---|
| **Ollama** | Command line | Simple, stable, lightweight; the easiest "just works" option |
| **LM Studio** | Graphical (GUI) | Beginners who prefer clicking over typing; great for browsing and trying models |
| **Jan** | Graphical (GUI) | A clean, open-source desktop app alternative to LM Studio |
| **GPT4All** | Graphical (GUI) | Runs on modest hardware; comes with a Python option too |

> Common workflow: use a GUI tool like *LM Studio* to browse and try models, then use *Ollama* for everyday work once you're comfortable. (More advanced tools like llama.cpp, vLLM, and LocalAI exist for power users, but you don't need them to start.)

---

## 4. Open-Source Models (the "content")

### "Model" — recap

The model is the **"AI brain"** — the part that actually thinks and answers. In the analogy, it is the **song file** the music app opens.

### What does "open-source" mean?

**Open-source** (also called *open-weight*) = the company that made the model **releases it publicly for anyone to download and use for free**, usually for both personal and commercial purposes.

The opposite is a **closed** model like OpenAI's GPT or Anthropic's Claude — you can only use these through their service, and **you cannot download them to your machine**.

> In short: **to run AI locally on your own machine, you must use an open-source model**, because closed models can't be downloaded.

### Notable open-source models

| Model | Made by | Notes |
|---|---|---|
| **Gemma** | Google | Light, efficient, good for weaker machines |
| **Llama** | Meta (Facebook) | Popular, many variants |
| **Qwen** | Alibaba | Strong, good multilingual support |
| **Phi** | Microsoft | Very light, runs on low-end machines |
| **DeepSeek** | DeepSeek | Strong at reasoning and coding |
| **Mistral** | Mistral AI | Solid all-rounder, popular in production |

### A model comes in several "sizes"

You'll see names like `gemma3:1b`, `gemma3:4b`, `qwen3:8b`. The **"B"** means *billion* — the **number of parameters**, i.e. roughly **"how big the brain is"**:

- **Bigger number**: smarter, but needs a **more powerful machine** and runs slower.
- **Smaller number**: a bit "dumber," but **light and fast** on weak machines.

Example: `4b` means the model has 4 billion parameters.

> There's also something called **quantization** (often shown as `Q4`) — a technique that "compresses" a model so it's lighter and can run on ordinary machines. Software like Ollama does this automatically, so you **don't need to worry about it**.

---

## 5. Getting Started: Install Ollama and Run Your First Model

This section is hands-on. By the end you'll have Ollama installed and be chatting with a real model.

### Step 1: Install Ollama

**Windows**
1. Go to https://ollama.com/download
2. Download the Windows installer (`OllamaSetup.exe`) and run it.
3. After it installs, Ollama runs quietly in the background. Open **PowerShell** (or Command Prompt) to type commands.

If you are new to Windows and do not know how to open PowerShell or Command Prompt yet:

1. Press the **Windows** key on your keyboard, or click the **Start** button in the lower-left corner.
2. Type `PowerShell`, then press **Enter** to open PowerShell.
3. If you want to use Command Prompt instead, type `cmd`, then press **Enter**.
4. When the black or blue command window opens, you can type commands like `ollama --version`.

![Open PowerShell or Command Prompt on Windows](../../images/0101.png)

**Mac**
1. Go to https://ollama.com/download
2. Download the macOS version, open the `.zip`, and drag **Ollama** into your Applications folder.
3. Launch it once (it appears in the menu bar). Then open the **Terminal** app to type commands.

Check it installed correctly (same command on both):

```
ollama --version
```

### Step 2: See available open-source models

Ollama keeps a public library of models you can download.

- **Browse online:** visit https://ollama.com/library to see every available model, its sizes, and exact tags (like `gemma3:270m`).
- **See what you already have installed:**

```
ollama list
```

Note: `ollama list` only shows models already on your machine. To discover new models to download, use the online library above.

### Step 3: Install gemma3:270m

This downloads Google's tiny 270-million-parameter Gemma model (about 290 MB):

```
ollama pull gemma3:270m
```

### Step 4: Chat with it

```
ollama run gemma3:270m
```

This opens an interactive chat. Type a message, press Enter, and the model replies. To leave the chat, type:

```
/bye
```

### PowerShell sample (Windows)

The full sequence in Windows PowerShell, start to finish:

```powershell
# Check Ollama is installed
ollama --version

# Download the tiny Gemma model
ollama pull gemma3:270m

# See what is installed on your machine
ollama list

# Start chatting (type /bye to exit)
ollama run gemma3:270m
```

You can also ask a single question without entering chat mode:

```powershell
ollama run gemma3:270m "Explain what an LLM is in one sentence."
```

> Reminder: `gemma3:270m` is very small, so keep questions short and simple. For better answers, install a larger model later (see Section 7) and run it the same way.

---

## 6. How Many Models Can You Install / Run at Once?

This is three different questions that people often mix up. Separating them makes everything clear.

### a) Installing (downloading) — practically unlimited

"Installing" a model just means **saving its files to your hard drive**. The only limit is **disk space**.

Each small model is only a few GB, so on a typical drive you can install **dozens or even hundreds** of models. They just sit on disk and use **no RAM** until you actually run them. (In the music analogy: this is how many *songs you keep stored* — as many as fit.)

### b) Running at the same time (loading into RAM) — limited by memory

To actually *run*, a model must be **loaded into memory** (RAM for CPU, or VRAM for GPU), which is limited.

Technically, software like Ollama **can** load several models at once. By default it allows up to 3 models loaded simultaneously on a CPU machine — **but only on the condition that they fit in available memory**. That condition is the real limit.

So the "3" is just a *ceiling that's allowed*; the **actual limit is your memory**. A powerful machine (lots of RAM/VRAM) can run several at once; a modest one can run only one.

### c) Switching between models — the software handles it automatically

Good news: you **don't manually open and close** models. Ollama manages it for you. If a request needs a new model but there isn't enough memory, Ollama **automatically unloads idle models to make room**, then loads the new one.

So if you call model A, it loads A. If you then call model B and memory can't hold both, it quietly unloads A and loads B. This happens in the background — it just costs a few seconds of reload time. Use the `ollama ps` command to see which models are currently in memory.

---

## 7. Matching Models to Common Hardware Types

The single biggest factor is **memory**: system RAM if you have no graphics card, or **VRAM** (the memory on a dedicated GPU) if you do. A GPU is far faster than a CPU for this, so models that fit in VRAM run much quicker. Always use the default **Q4** quantized version to save memory.

Below are four common machine categories. Find the one closest to yours.

### Type 1: No dedicated GPU (CPU + RAM only)

Office laptops, older desktops, and machines with only integrated graphics. Everything runs on the CPU, which works but is slow, so stay small.

- Sweet spot: **1B to 4B** models, for example `gemma3:1b`, `gemma3:4b`, `llama3.2:3b`, `qwen3:4b`
- Possible but slow: a single **7B to 8B** model, for example `qwen3:8b`
- Avoid: anything larger

### Type 2: Entry or mid-range GPU (about 6 to 8 GB VRAM)

Many gaming laptops and budget desktop cards (for example an RTX 3050/3060 class GPU).

- Comfortable: **7B to 8B** models, for example `qwen3:8b`, `llama3.1:8b`, `phi-4`
- Possible: up to about **12B to 14B** quantized, for example `gemma3:12b`

### Type 3: High-end GPU (about 16 to 24 GB VRAM)

Enthusiast desktop cards (for example an RTX 3090/4090 class GPU).

- Comfortable: **27B to 32B** models, for example `gemma3:27b`, `qwen2.5-coder:32b`
- Possible but slower: a **70B** model at Q4, for example `llama3.3:70b`

### Type 4: Apple Silicon Mac (M-series, unified memory)

On these Macs the CPU and GPU **share the same memory**, so your total RAM is what matters. They are surprisingly capable for their size.

- 16 GB RAM: comfortable with **7B to 14B** models
- 32 GB or more: can handle **27B to 70B** models
- Tip: **Apple MLX** is usually the fastest option on these chips, though Ollama works well too

### General rule of thumb

> Pick the **largest model that fits in your memory with room to spare**. If responses are too slow or the machine struggles, step down one size. If it runs easily, try the next size up.

---

## 8. Running Two Gemma Models at the Same Time

A practical example: installing **and running** both `gemma3:270m` (the tiny nano model from Section 5) and `gemma3:4b` (the 4-billion-parameter model) at once. This works on most machines because the nano model is so small.

### Installing both

Installing just downloads files to disk, and these two are tiny:

- `gemma3:270m`: ~290 MB
- `gemma3:4b`: ~3.3 GB

Download them with:

```
ollama pull gemma3:270m
ollama pull gemma3:4b
```

See everything installed on disk:

```
ollama list
```

### Running / retrieving them

Run a model by name (type `/bye` to exit the chat):

```
ollama run gemma3:270m
```

To use the other one instead:

```
ollama run gemma3:4b
```

### Can both be loaded into memory at once? Usually yes

Memory is the limit for running models simultaneously — but `gemma3:270m` is so small that **both fit comfortably** even on a modest machine. Rough cost: ~300 MB for the nano + ~4 GB for the 4b is under 5 GB total. Ollama allows up to 3 models loaded at once on a CPU machine by default, so it keeps both in memory if you use both.

Check what's currently **loaded in memory** (not just installed on disk):

```
ollama ps
```

This shows each loaded model, its size, and a countdown until it auto-unloads (Ollama frees a model after about 5 minutes of inactivity).

### Why this combo is useful

- Use `gemma3:270m` for quick, simple tasks — lightning fast, but limited in quality.
- Switch to `gemma3:4b` when you need better answers — slower, but noticeably smarter. This is your "real" everyday model.

You can keep two terminal windows open, one per model, and they'll coexist in memory. Or just `run` whichever you need and let Ollama handle loading and unloading automatically.

---

## 9. Quick Reference Tables

### Software vs. Model

| | LLM Software | Open-Source Model |
|---|---|---|
| **What is it?** | The tool that runs the AI | The AI brain itself |
| **Examples** | Ollama, LM Studio, Jan, GPT4All | Gemma, Llama, Qwen, Phi |
| **Analogy** | Music app | Song file |
| **How many to install?** | Just one is enough | Download as many as you like |
| **Decides what?** | How you interact (CLI vs GUI) | How smart the AI is |

### Essential Ollama commands

| Command | What it does |
|---|---|
| `ollama --version` | Confirm Ollama is installed |
| `ollama pull <model>` | Download a model (e.g. `gemma3:270m`) |
| `ollama list` | Show models installed on your machine |
| `ollama run <model>` | Start chatting with a model |
| `ollama ps` | Show which models are loaded in memory |
| `/bye` | Leave the chat |

### Model size by hardware

| Hardware | Comfortable model size |
|---|---|
| No GPU (CPU + RAM) | 1B to 4B |
| Entry/mid GPU (6 to 8 GB VRAM) | 7B to 8B |
| High-end GPU (16 to 24 GB VRAM) | 27B to 32B (up to 70B) |
| Apple Silicon Mac | 7B to 70B depending on RAM |

### One-sentence summary

> **Software** (like Ollama) is like the *music app*; an **open-source model** (like Gemma) is like the *content* it opens. Install the software once, then download as many models as you like to run AI right on your own machine — private, free, and offline. Downloading is unlimited; running several at once is what your memory limits.
