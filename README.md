# Gingoa

An AI code guardrail and validation framework that constrains and checks AI coding agents through logic and code, not through prompts.

## Why

An AI coding agent reads your data, writes your code and tells you the result is fine. Instructions in a prompt can ask it to be careful; they cannot make it so, and they cannot prove that it was. Gingoa puts the checks where the agent cannot talk its way past them:

- **Enforced by the harness.** Each check runs as a hook or a local program around the agent, so the verdict does not depend on the model's own account of what it did.
- **Measured, not asserted.** A check produces evidence you can read, such as a score, a list of surviving bugs, or the exact values that were withheld.
- **Local.** Checks run on your machine and send nothing anywhere.
- **Honest about limits.** These are guardrails against mistakes and overreach by a cooperating agent. They are not a sandbox against an agent that sets out to defeat them; each component documents what it does not cover.

## Components

Each component is its own repository, released and versioned on its own. Gingoa links them; it does not copy their code.

| Component | What it controls | How | Repository |
|---|---|---|---|
| **deid-guard** | What personal data reaches the model | Data files are read through a profile card, then a de-identified copy; every row the model reads is scrubbed against known values and detectors; unmasking a column needs the user's approval in a local dialog. Korean and English. | [godic97/deid-guard](https://github.com/godic97/deid-guard) |
| **mutation-gate** | Whether the agent's tests actually catch bugs | When the agent writes or runs tests, it mutation-tests the code under test (StrykerJS for JS/TS, mutmut for Python), adds assertions until the surviving mutants die, and reports the score. An optional end-of-turn report covers the lines the agent changed. | [godic97/mutation-gate](https://github.com/godic97/mutation-gate) |

## Install

Both components are Claude Code plugins. Install the ones you need from inside Claude Code:

```
/plugin install deid-guard --marketplace godic97/deid-guard
/plugin install mutation-gate --marketplace godic97/mutation-gate
```

Each repository's README lists its requirements, configuration and limits.

## License

MIT. See [LICENSE](LICENSE). Each component carries its own license in its repository.
