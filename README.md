# Peddle — Data Release

Companion data for the M.Sc. thesis *"A Domain-Specialized Agentic LLM for Marketing
Campaign Generation"* and the code at https://github.com/oduwairi/peddle-research.

This package contains the **derived training data** and a **de-identified sample** of
the scored corpus. The full 55,000-ad AdFlex corpus is **not** included — see the
[Data Availability Statement](https://github.com/oduwairi/peddle-research/blob/main/DATA.md).

## Contents

```
sft_dataset/
  train.jsonl        4,081 chat-format SFT pairs  (instruction-backtranslation)
  validation.jsonl     226
  test.jsonl           228
sample/
  scored_sample_deidentified.jsonl   300 scored ads (de-identified)
```

### `sft_dataset/` — fine-tuning data

Each line: `{"messages": [{role, content}...], "metadata": {example_id, ad_id, platform}}`.
`messages` is a standard `system`/`user`/`assistant` chat triple — the `user` turn is the
reverse-engineered brief, the `assistant` turn is the real high-performing ad. This is
the exact set used to QLoRA-fine-tune Qwen3-8B. Source AdFlex IDs are hashed.

### `sample/scored_sample_deidentified.jsonl` — scoring/tiering illustration

300 ads, 100 per tier (high/medium/low), balanced across the five platforms. Each line
carries ad copy, engagement counts, the composite score, its three signal components
(survivability / engagement volume / engagement velocity), and the tier label —
identifying and targeting fields removed. Lets reviewers inspect the input schema and
verify the scoring code without the full corpus.

## Provenance & terms

Underlying ad data was collected via the commercial AdFlex API (https://adflex.io).
Redistribution of the full corpus is restricted by AdFlex's terms; this de-identified
derived subset is released for academic reproducibility only. Public validation
datasets used elsewhere in the thesis (Upworthy, IRA, Meta/Google/TikTok ad libraries)
are available from their original sources.

Contact: oduwairi@gmail.com
