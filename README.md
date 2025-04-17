# AppWorld to T-Bench

A simple tool to translate AppWorld tasks into T-Bench format.

## Installation

```bash
uv pip install appworld
uv run appworld install
uv run appworld download data
```

## Run

```bash
python appworld-to-t-bench.py {appworld_task_id} {t_bench_task_id} --t-bench-directory .
# Task will be generated in ./tasks/{t_bench_task_id}
```
