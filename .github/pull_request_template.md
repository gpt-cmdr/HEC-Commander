## Summary

<!-- Brief description of what this PR does and why. -->

## Type of Change

- [ ] New notebook or tool
- [ ] Improvement to existing notebook or tool
- [ ] Bug fix
- [ ] Documentation update
- [ ] Dependency or configuration change
- [ ] Other (describe below)

## LLM Self-Review Checklist

<!-- If you used an LLM agent, confirm it reviewed against these criteria. -->

### Notebook Quality

- [ ] First cell is Markdown with H1 title
- [ ] Clear explanations between code cells
- [ ] All cells execute without errors (Kernel > Restart & Run All)
- [ ] No hardcoded absolute paths
- [ ] Outputs saved in committed notebook
- [ ] N/A (not a notebook change)

### Code Quality

- [ ] Google-style docstrings on functions
- [ ] Uses `logging` instead of bare `print()` where appropriate
- [ ] Error handling for file I/O and external calls
- [ ] No secrets or machine-specific paths committed
- [ ] Dependencies documented

### HEC-RAS / HEC-HMS Specifics

- [ ] Uses example projects or documents how to obtain test data
- [ ] HEC-RAS/HMS version requirements stated
- [ ] Engineering workflow explained, not just code
- [ ] N/A (not an H&H notebook)

## Test Plan

<!-- How did you verify this works? -->

- [ ] Ran notebook end-to-end (Kernel > Restart & Run All)
- [ ] Tested with HEC-RAS/HMS version: ___
- [ ] Verified on OS: ___
- [ ] Other: ___

## LLM Attribution

<!-- Optional but appreciated. Which tool helped? -->

- [ ] This PR was prepared with LLM agent assistance
- Agent used: <!-- e.g., Claude Code, Codex, Cursor, Copilot, etc. -->

---

*See [CONTRIBUTING.md](../CONTRIBUTING.md) for full guidelines.*
