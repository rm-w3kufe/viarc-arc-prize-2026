# ViArc VSM — ARC Prize 2026 solutions

Team **rm -w3kufe** · tracks **ARC-AGI-2** and **ARC-AGI-3** · all solution code [CC0-1.0](LICENSE).

## ARC-AGI-2 (`agi2/`)

Symbolic engine + certified LLM (Qwen2.5-3B-Instruct, staged offline as a
competition dataset — evaluation runs with internet disabled).

- Deterministic dynamics/program enumeration with leave-one-out (LOO)
  certification against train pairs.
- LLM proposals must pass V1 self-consistency (majority of K=4 samples) and
  V2 LOO understanding before they may compete; uncertified guesses never
  outrank verified symbolic programs.
- Only the keys of the competition's `sample_submission.json` are solved;
  the judged file is schema-exact (`attempt_1`/`attempt_2` per entry).

Reproduce: `python3 agi2/build_notebook.py --out kaggle_notebook.ipynb`
then push as a Kaggle notebook (`agi2/kaggle/push.sh`) and run on GPU.

## ARC-AGI-3 (`agi3/`)

VSM homeostat + CNN proposer + certified Qwen brain, as a single-file agent
(`agi3/agent/viarc3_agent.py`, spliced into the kernel notebook as
`my_agent.py`) embedded in the official ARC-AGI-3-Agents
notebook pattern (gateway rerun plays the games; the agent is the code).

- Action selection degrades silently: CNN tier → LLM brain → deterministic
  homeostat (the harness never crashes).
- Deterministic seeds from `game_id` only (no wall-clock entropy).
- Local dev loop: the `arc3-lab` Makefile (`play-local`, `notebook`,
  `submit`); test suites under `agi3/tests/`.

## Licensing & attribution

- Solution code in this repository: **CC0-1.0** (see LICENSE).
- Qwen model weights (Apache-2.0) are used via a Kaggle staged dataset and
  are **not bundled** here; the upstream license ships with that dataset.
- The ARC-AGI-3 CNN tier is adapted from the official Kaggle sample
  "ARC3 Sample Submission – Stochastic Goose" (DriesSmit / Tufa Labs);
  attribution is preserved in the module headers.
- Third-party Python packages (torch, transformers, pandas, arc-agi, …)
  keep their own licenses and are not vendored.
