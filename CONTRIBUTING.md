# Contributing to HEC-Commander

Thank you for your interest in contributing to HEC-Commander. This project is an open-source suite of Jupyter Notebooks and tools for AI-assisted automation of HEC-RAS, HEC-HMS, and related water resources engineering workflows. It is maintained by [CLB Engineering Corporation](https://clbengineering.com/) and licensed under the MIT License.

---

## Our Philosophy: Don't Ask Me, Ask a GPT!

HEC-Commander was built with LLM assistance from the very beginning. We welcome contributions prepared the same way. Use whatever agent works for you -- Claude Code, Codex, Aider, Cursor, Gemini, GitHub Copilot, or anything else. The tool does not matter; the quality of the result does.

When an LLM agent reads the project rules, understands the conventions, and self-reviews its own output before you submit a PR, the maintainer's review burden drops significantly. That means faster merges for you and a healthier project for everyone.

Learn more about the philosophy behind this approach: [LLM Forward Engineering](https://clbengineering.com/llm-forward)

---

## Quick Start

1. **Fork** the repository on GitHub: [gpt-cmdr/HEC-Commander](https://github.com/gpt-cmdr/HEC-Commander)
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/<your-username>/HEC-Commander.git
   cd HEC-Commander
   ```
3. **Create a branch** for your contribution:
   ```bash
   git checkout -b feat/my-contribution
   ```
4. **Launch your preferred LLM agent** and point it at the repo. Have it read `CONTRIBUTING.md`, `CLAUDE.md`/`AGENTS.md`, and any relevant notebook READMEs before writing code.
5. **Make your changes**, self-review with the checklist below, and open a PR.

---

## The Self-Review Contract

We operate on a simple contract:

> If your agent reads the project rules and self-reviews its output against the checklist below, your PR will be straightforward to review and fast to merge.

PRs that clearly followed the checklist get prioritized. PRs that ignore it may be sent back with a friendly "please re-run the checklist."

---

## LLM Self-Review Checklist

Before opening a PR, have your agent (or yourself) verify:

### Notebook Quality

- [ ] First cell is a **Markdown cell with an H1 title** (`# Descriptive Title`)
- [ ] Notebook includes clear explanations between code cells (not just code dumps)
- [ ] All code cells execute without errors (Kernel > Restart & Run All)
- [ ] No hardcoded absolute paths -- use relative paths or parameterized variables
- [ ] Outputs are saved in the committed notebook (readers should see results)
- [ ] File size is reasonable (under 5 MB; large outputs should be images, not raw data)

### Code Quality

- [ ] Functions have **Google-style docstrings** with Args, Returns, and Raises sections
- [ ] Uses `logging` module for status messages, not bare `print()` statements (minor print usage in notebooks is acceptable for demonstration purposes)
- [ ] Error handling is present for file I/O, network calls, and external tool invocations
- [ ] No secrets, credentials, or internal file paths committed
- [ ] Dependencies are documented (either in the notebook or in `requirements.txt`)

### HEC-RAS / HEC-HMS Notebooks

- [ ] Uses example projects or clearly documents how to obtain test data
- [ ] No hardcoded paths to `C:\Users\...` or similar machine-specific locations
- [ ] HEC-RAS/HMS version requirements are stated
- [ ] Notebook explains the engineering workflow, not just the code

### General

- [ ] Changes are scoped -- one logical change per PR
- [ ] Commit messages follow conventional format (see below)
- [ ] No unrelated formatting changes mixed in with functional changes

---

## What We Accept

We welcome contributions in these areas:

- **Notebooks**: New automation workflows, analysis tools, or tutorials for HEC-RAS, HEC-HMS, DSS, or related tools
- **Improvements to existing notebooks**: Bug fixes, clarity improvements, updated dependencies
- **Tools and utilities**: Python scripts, helper functions, or CLI tools that support H&H workflows
- **Documentation**: README improvements, blog posts, setup guides, workflow explanations
- **Bug fixes**: Corrections to existing code, broken links, outdated instructions
- **Example data**: Small, shareable example datasets that make notebooks reproducible

---

## What We Don't Accept

- **New dependencies without justification**: If your contribution requires a new package, explain why in the PR description. Avoid heavy or obscure dependencies when a standard library solution exists.
- **Breaking changes without discussion**: If your change alters the behavior of an existing notebook or tool, open an issue first to discuss the approach.
- **Proprietary or sensitive data**: No project-specific data, client information, or files that cannot be freely redistributed.
- **Low-effort submissions**: Notebooks that are just raw LLM output without review, testing, or explanation do not meet the bar. The LLM is a tool -- you are the engineer.

---

## Commit Messages

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
feat(RAS-Commander): Add parallel execution notebook for 2D models

docs(Blog): Add post on AORC precipitation workflows

fix(HMS-Commander): Correct Jython path resolution on Windows 11

chore: Update requirements.txt with current dependency versions
```

**Prefixes**: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`

**Scope**: Use the relevant folder name (`RAS-Commander`, `HMS-Commander`, `DSS-Commander`, `Blog`, `ChatGPT Examples`) or omit for repo-wide changes.

### LLM Attribution

If an LLM agent wrote or substantially contributed to your changes, add a co-author line to your commit message:

```
feat(RAS-Commander): Add breach analysis automation notebook

Co-Authored-By: Claude <noreply@anthropic.com>
```

Use the appropriate attribution for the tool you used. This is not required, but it is appreciated for transparency.

---

## Community Standards

### Safety-Critical Domain

HEC-Commander tools are used in **flood modeling, dam safety, and floodplain management** -- domains where errors can affect public safety. Contributions should reflect that seriousness:

- Validate results against known benchmarks when possible
- Document limitations and assumptions clearly
- Prefer conservative defaults over aggressive optimizations
- Include visual verification steps (plots, maps) so engineers can sanity-check results

### Professional Conduct

- Be respectful and constructive in issues, PRs, and discussions
- Assume good faith -- contributors have varying levels of experience with both engineering and coding
- When reviewing others' work, explain the "why" behind requested changes
- Credit prior work and contributors appropriately

### LLM Forward Philosophy

This project follows the [LLM Forward](https://clbengineering.com/llm-forward) approach to engineering:

1. **Professional responsibility first** -- Public safety, ethics, and professional licensure remain paramount
2. **LLMs forward, not first** -- Technology accelerates engineering insight without replacing professional judgment
3. **Multi-level verifiability** -- HEC-RAS GUI review + visual outputs + code audit trails
4. **Human-in-the-loop** -- Licensed professionals in responsible charge at all times

---

## Project Structure

```
HEC-Commander/
├── RAS-Commander/       # HEC-RAS automation notebooks and tools
├── HMS-Commander/       # HEC-HMS automation notebooks and tools
├── DSS-Commander/       # DSS plotting and calibration statistics
├── Blog/                # Technical blog posts
├── ChatGPT Examples/    # GPT assistant examples and conversations
├── misc/                # Logos, presentations, supporting files
├── CLAUDE.md            # Agent guidance for this repository
├── AGENTS.md            # Agent guidance (same content)
└── CONTRIBUTING.md      # This file
```

Place new notebooks in the appropriate subfolder. If your contribution doesn't fit an existing folder, propose a location in your PR description.

---

## Getting Help

- **Issues**: Open an issue on [GitHub](https://github.com/gpt-cmdr/HEC-Commander/issues) for bugs, questions, or feature requests
- **Discussions**: Use GitHub Discussions for open-ended questions or ideas
- **LLM Agents**: Point your agent at the repo and ask it -- that is literally the point of this project
- **Related projects**:
  - [ras-commander](https://github.com/gpt-cmdr/ras-commander) -- Python library for HEC-RAS automation
  - [hms-commander](https://github.com/gpt-cmdr/hms-commander) -- Python library for HEC-HMS automation

---

*Maintained by [CLB Engineering Corporation](https://clbengineering.com/). Licensed under MIT.*
