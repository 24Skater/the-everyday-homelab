# AI Cluster Plan

Nodes: 3x Dell OptiPlex 7050 Micro — Kaby Lake i5/i7, integrated graphics only (no dGPU), modest RAM. Suggested naming: `AI1`/`AI2`/`AI3` to match the `TC1`/`TC2`/`TC3` convention.

Realistic expectations: this is CPU-only inference on small/quantized models — not fast large-model inference. Great for testing, learning distributed serving, and running lightweight models.

## OS

Bare metal Ubuntu Server 24.04 LTS on each node — no Proxmox/virtualization layer. No dGPU and modest CPU/RAM means virtualization overhead isn't worth it, and staying bare-metal keeps this cluster's purpose distinct from the Proxmox cluster.

## Orchestration

k3s (lightweight Kubernetes) — 1 node as control-plane/server, 2 as agents/workers to start. Built for small edge clusters like this, single-command install.

## Serving pattern

Independent nodes behind a load-balanced Service — **not** one model split across all 3 via RPC. With 1GbE and no GPUs, splitting a model's layers across nodes makes the network the bottleneck per-token (technically works, but slow). Running Ollama as a replicated service, with each node independently serving requests, gets more real throughput and mirrors how production inference clusters are actually built.

## Starting models

Small, CPU-friendly quantized models via Ollama:
- Llama 3.2 3B
- Phi-3.5-mini
- Qwen2.5 7B (Q4)

## Stretch goal (later, optional)

Once the basics work, splitting a larger model across all 3 nodes (llama.cpp RPC backend, or a tool like `exo`) is a fun advanced experiment — expect it to be slow given the network/no-GPU constraints, more educational than practical.

## Next steps

1. Image each node with Ubuntu Server 24.04 LTS
2. Install k3s (server on `AI1`, agents on `AI2`/`AI3`)
3. Deploy Ollama as a replicated service across the cluster
4. Load starting models and test
