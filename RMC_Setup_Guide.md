# RMC Formation — Setup Guide
**Training LLMs at Scale + Research with Agents**

> Covers accounts and tools on your laptop. The cluster's Python/conda environment is set up separately in Session 1.

---

## At a Glance

| # | What | For | When |
|---|------|-----|------|
| 1 | Weights & Biases account | Experiment tracking | Day 1 |
| 2 | Hugging Face account + write token | Models, datasets, Hub | Day 1 |
| 3 | GitHub account | Cloning exercises, version control | Both days |
| 4 | Anthropic API key (free credit) | Claude Code agent | Day 2 |
| 5 | OpenAI / ChatGPT account | Codex agent | Day 2 |
| 6 | VS Code + extensions | Editor / remote dev | Both days |
| 7 | Node.js 18+, Git, agent CLIs | Running the agents | Day 2 |

---

## 1. Weights & Biases

- Sign up (free): https://wandb.ai
- Copy your API key: https://wandb.ai/authorize
- Paste it on the cluster during Session 1

**Key saved?** ☐

---

## 2. Hugging Face

- Sign up (free): https://huggingface.co/join
- Create a **Write** token: https://huggingface.co/settings/tokens
- ⚠️ Save it immediately — shown only once

**Token saved?** ☐

---

## 3. GitHub

- Sign up (free) if needed: https://github.com/signup

**Account ready?** ☐

---

## 4. Anthropic API Key (Claude Code)

1. Sign up: https://console.anthropic.com
2. Create a key under **API Keys**
3. Do **not** add a payment method — free trial credit covers Day 2 usage
4. Copy the key (`sk-ant-...`) and keep it private

**Key saved?** ☐

---

## 5. OpenAI / ChatGPT (Codex)

- Codex uses a free ChatGPT account — no API key or payment required
- Sign up if needed: https://chatgpt.com

**Account ready?** ☐

> ⚠️ Never commit keys to git or share them. Set them as environment variables on Day 2.

---

## 6. VS Code

Install: https://code.visualstudio.com

Add these extensions on **both your laptop and the cluster** (Remote-SSH doesn't sync them):

**Mandatory**
- Remote - SSH (+ Remote Explorer)
- Python (extension pack)
- Jupyter

**Nice to have**
- GitLens, Black Formatter, Flake8, autoDocstring, Python Indent, Python Type Hint, Code Spell Checker, Rainbow CSV

> Cursor (https://cursor.com) works too — same extensions and Remote-SSH flow. Demo will be in VS Code.

**Extensions installed?** ☐ laptop  ☐ cluster

---

## 7. Node.js, Git, and Agent CLIs

Install Node.js 18+: https://nodejs.org (or use `nvm`)  
Install Git: https://git-scm.com

Then install the CLIs:

```bash
npm install -g @anthropic-ai/claude-code@latest   # Claude Code
npm install -g @openai/codex                       # Codex
```

> ⚠️ Don't use `sudo` with npm. If you hit permission errors, install Node via `nvm`.

Sign-in for both CLIs happens together on Day 2.

**Installed?** ☐

---

## Pre-Day-1 Smoke Check

Run each command — should print a version with no error:

```bash
node --version    # v18+
git --version
code --version
claude --version
codex --version
```

**And have these ready to paste:**

- [ ] W&B API key
- [ ] HF write token
- [ ] Anthropic API key

---

*That's it — see you Day 1.*
