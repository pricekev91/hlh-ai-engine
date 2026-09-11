# TODO

Active items in progress. These are the current focus areas.

## Active

- [ ] Validate GPU PCI IDs for passthrough on updated Proxmox kernels (`226:1`, `226:129`, `511:0` for `gfx1150` — now HIP+Vulkan)
- [ ] Run ai-vm ROCm migration plan on staging environment
- [ ] Confirm final DNS hostnames for AI endpoint (`192.168.1.12:80`)

## This Week

- [ ] Run `./deploy-hlh-ai-engine.sh` to verify LXC 112 creation flow (full cycle, dual HIP+Vulkan, header prints `10.0.0` latest, never pinned)
- [ ] Test `ROCM_VERSION=7.14.1` rollback path — confirm `amdrocm7.14-gfx1150` still works
- [ ] Test model switching after LXC bootstrap (`switch-model.sh` v1.7.0 integration, `90s` `/health` probe)
- [ ] Validate Vulkan (`vulkaninfo --summary`, `RADV_PERFTEST=nogttspill llama-bench -dev Vulkan0` vs `ROCm0`) — HIP+Vulkan no perf hit, `88G` UMA check
- [ ] Validate ROCm `10.0.0` driver (default, never pinned) compatibility with latest `amdgpu` kernel module (`hipconfig`, `rocm-smi`, `10.0.0` 2026-08-26)

## Done (2026-09-11 — v0.9.4 + v0.9.3)

- [x] Dual `HIP+Vulkan` build (`GGML_HIP=ON + GGML_VULKAN=ON`, `gfx1150`-only) — no perf hit, `+12-18M` binary (v0.9.3)
- [x] Unpinned `ROCM_VERSION` never pinned — default now `10.0.0` (was `7.14.1`), `7.14.1` still via `ROCM_VERSION=7.14.1` override, `ROCM_MM` mapping (v0.9.4)
- [x] Fix `DEFAULT_MODEL_URL` `Qwen2.5→Qwen3-Coder-30B` + docs `LXC 101→112` `8080→80` drift
- [x] Deploy script always calls out version (`[0/6]` header + `[6/6]` footer) and forwards `ROCM_VERSION` into LXC — never pinned
