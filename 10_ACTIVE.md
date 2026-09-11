# TODO

Active items in progress. These are the current focus areas.

## Active

- [ ] Validate GPU PCI IDs for passthrough on updated Proxmox kernels (`226:1`, `226:129`, `511:0` for `gfx1150` — now HIP+Vulkan)
- [ ] Run ai-vm ROCm migration plan on staging environment
- [ ] Confirm final DNS hostnames for AI endpoint (`192.168.1.12:80`)

## This Week

- [ ] Run `ROCM_VERSION=7.14.1 ./deploy-hlh-ai-engine.sh` to verify LXC 112 creation flow (full cycle, dual HIP+Vulkan, header prints version)
- [ ] Test `ROCM_VERSION=10.0.0` path on staging (unpinned major) — confirm `amdrocm10.0-gfx1150` exists
- [ ] Test model switching after LXC bootstrap (`switch-model.sh` v1.7.0 integration, `90s` `/health` probe)
- [ ] Validate Vulkan (`vulkaninfo --summary`, `RADV_PERFTEST=nogttspill llama-bench -dev Vulkan0` vs `ROCm0`) — HIP+Vulkan no perf hit, `88G` UMA check
- [ ] Validate ROCm `7.14.1` driver (default unpinned) compatibility with latest `amdgpu` kernel module (`hipconfig`, `rocm-smi`)

## Done (2026-09-11 — v0.9.3)

- [x] Dual `HIP+Vulkan` build (`GGML_HIP=ON + GGML_VULKAN=ON`, `gfx1150`-only) — no perf hit, `+12-18M` binary
- [x] Unpinned `ROCM_VERSION` (`7.14.1` default, `10.0.0` override via env) with `ROCM_MM` package mapping
- [x] Fix `DEFAULT_MODEL_URL` `Qwen2.5→Qwen3-Coder-30B` + docs `LXC 101→112` `8080→80` drift
- [x] Deploy script calls out version (`[0/6]` header + `[6/6]` footer) and forwards `ROCM_VERSION` into LXC
