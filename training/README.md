# Interphyre — RL Training Code

This folder contains the physics environment, the GRPO training
framework (`verl` / `verl_tool`), the evolving skill-bank pipeline (`SKILL-RL`), the
training/eval launch scripts, and the preprocessed datasets needed to reproduce runs.

The goal of the project is to train an LLM agent (Qwen 2.5 3B Instruct) to solve
[Interphyre](#) physics puzzles via tool use and GRPO, with an optional skill bank that is
distilled from agent trajectories by a larger teacher model and injected into the agent's
system prompt.

## Directory layout

| Path | Description |
|------|-------------|
| `interphyre/` | Box2D physics simulation engine — 25 puzzle levels, object/render/validation modules. |
| `verl/` | Vendored [verl](https://github.com/volcengine/verl) RL training library (editable install). |
| `verl_tool/` | Tool-augmented training framework on top of verl — agent loop, servers, trainer, hooks, workers. |
| `SKILL-RL/` | Evolving skill-bank pipeline: distillation, evolution loops, skill banks, trajectory analysis. |
| `data/` | Preprocessed parquet datasets per training variant (e.g. `interphyre_dte_s1_50`, `interphyre_tbp_evolving_continuous`). |
| `examples/data_preprocess/interphyre_data.py` | Builds the parquet datasets from Interphyre levels. |
| `examples/train/interphyre/` | SLURM + shell launch scripts for the GRPO training runs and the 7B teacher (vLLM). |
| `examples/eval/` | SLURM eval scripts and `interphyre_eval.py`. |
| `verl_tool.egg-info/` | Build metadata for the `verl_tool` package. |
| `requirements.txt` | Frozen Python dependencies (Python 3.10). |
| `.env.example` | Template for API keys / service endpoints (copy to `.env`, fill in). |
| `LICENSE`, `.gitignore` | Carried over from the source project. |

## Training variants

The three variants (all train Qwen 2.5 3B Instruct via GRPO) are described in detail in
[`SKILL-RL/README.md`](SKILL-RL/README.md):

| Variant | Skill bank | Launch script |
|---------|-----------|---------------|
| Non-skilled | None | `examples/train/interphyre/slurm_train_3b_a100_1gpu_dte_bsz1.sh` |
| Skilled (static) | Fixed at data-gen time | `examples/train/interphyre/slurm_train_3b_a100_1gpu_dte_bsz1_skilled.sh` |
| Evolving-skilled | Grows each round via a 7B teacher | `examples/train/interphyre/slurm_evolving_grpo_dte.sh` |

## Environment setup

The code targets **Python 3.10** with a CUDA 12 GPU stack (torch 2.8, vLLM 0.11, flash-attn,
ray). `verl` and `verl_tool` are vendored in this folder and installed editable.

```bash
# create a Python 3.10 environment (conda example)
conda create -n interphyre python=3.10 -y
conda activate interphyre

# install pinned dependencies
pip install -r requirements.txt

# install the vendored training framework (editable)
pip install -e ./verl
pip install -e ./verl_tool

# configure secrets/services
cp .env.example .env   # then fill in API keys / endpoints
```

> **Note:** `requirements.txt` is a full `pip freeze` of the working environment and pins
> CUDA-specific wheels. Adjust the `nvidia-*`, `torch`, `vllm`, and `flash-attn` versions to
> match your CUDA driver if needed.

## Reproducing a run

1. Build the dataset (if not already present in `data/`):
   ```bash
   python examples/data_preprocess/interphyre_data.py
   ```
2. Launch a training run, e.g.:
   ```bash
   sbatch examples/train/interphyre/slurm_train_3b_a100_1gpu_dte_bsz1.sh
   ```
3. Evaluate a checkpoint:
   ```bash
   sbatch examples/eval/slurm_eval_dte_run24.sh
   ```

See `SKILL-RL/README.md` for the evolving skill-bank pipeline and teacher setup.
