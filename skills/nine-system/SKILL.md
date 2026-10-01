---
name: nine-system
description: Diagnose local Windows machine (RAM/CPU/disk) and Ollama models, and recommend which local nine-* agent to use. Use when the user asks about free RAM, slow local models, Ollama status, missing downloads, or which local model fits the task. Runs on NINECODE via the nine-system MCP (100% local, no API keys).
---

# /nine-system

Health check + router aid for NINECODE's local LLMs (Ryzen 7 5700U, 16GB RAM, CPU-only).

## Tools (nine-system MCP)

1. `sys_status` - RAM total/libre, CPU, disco C, top 5 procesos. Call it BEFORE any `nine-max` (14B) work.
2. `ollama_status` - downloaded models, in-RAM models, missing ones with `ollama pull` hints.
3. `recommend_model` - input `task` (`code_rapido` | `analisis` | `refactor_grande` | `chat`), measures real free RAM unless `free_ram_gb` is given. Returns agent + `ollama/...` model + fallback.

## Workflow

1. User reports slowness or wants a big local task -> call `sys_status` + `ollama_status` in parallel.
2. If `free_ram_gb` < 6 -> tell the user to close Brave/Chrome tabs first (they eat 1GB+). Re-check with `sys_status`.
3. Call `recommend_model` with the task type, then delegate with `@mention`:
   - `nine-code` -> `ollama/qwen2.5-coder:7b` (needs ~6GB free)
   - `nine-reason` -> `ollama/qwen3:8b` (needs ~7GB free)
   - `nine-max` -> `ollama/qwen2.5-coder:14b` (needs ~11GB free)
   - `nine-router` -> `ollama/qwen3:4b` (always available fallback)
4. If a model in `faltantes` is needed -> give the user the exact `ollama pull X` command. Downloads run in the Ollama server, no extra setup.

## Rules

- Never invent RAM numbers: always measure with `sys_status` first.
- Never send a 14B task with < 11GB free: recommend the fallback and say what to close.
- Answer in Spanish, short: numbers + decision + next step.
