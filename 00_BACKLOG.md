# BACKLOG

Items for future implementation. These are human-entered ideas not yet reflected
in the codebase.

## GPU / ROCm

- Add GPU memory utilization monitoring script (`rocm-smi` parsing + alerting; `vulkaninfo` + `RADV_PERFTEST=nogttspill` as Vulkan complement)
- Add automatic model eviction when GPU memory is low (consider Vulkan `88G` UMA vs HIP `48G` split)
- Support multi-GPU workloads (future hardware upgrade)
- Track ROCm version compatibility matrix across Proxmox kernel updates (now unpinned `ROCM_VERSION` `10.0.0`; matrix still needed)

## Model Management

- Add model versioning system (pin specific GGUF files per deployment)
- ~~Add model download progress tracking and resume support~~ — `dl.sh` resumable `curl -C -` now in bootstrap `v0.9.3` (`90_DONE`); still needs progress UI
- Add model quality scoring after inference testing (consider per-backend `HIP` vs `Vulkan` scores)

## LXC Lifecycle

- Add LXC snapshot before major model updates
- Add LXC resource quota enforcement (CPU, memory, I/O)
- Add LXC snapshot restore procedure

## Ansible Improvements

- Add ansible-lint to CI workflow
- Split configure-ai-engine-inside-lxc.sh into multiple Ansible roles
- Add idempotency tests for ansible playbook
- Add ansible-galaxy role packaging for reuse

## OpenTofu

- Add tofu variables for GPU PCI IDs (currently hardcoded via cgroup rules)
- Add tofu output for container IP and API endpoint
- Add tofu state locking for multi-operator safety
- Migrate from telmate/proxmox to bpg/proxmox provider (align with hlh-docker)

## Networking

- Add DNS entry for engine API endpoint
- Add HTTPS/TLS termination on nginx reverse proxy
- Add rate limiting configuration for API endpoints
- Add API key authentication for external consumers

## Observability

- Add Prometheus metrics endpoint for inference latency (also consider `rocm-cli` `rocmd` `Observe` TUI + `rocm examine --json` as sidecar; evaluate `rocm dash` vs Prometheus exporter)
- Add structured logging for llama-server
- Add request logging with model name, token count, and backend (`HIP`/`Vulkan`) for per-backend accounting

## Deployment

- Add pre-flight checks for GPU availability before deployment
- Add dry-run / plan mode for deploy script
- Add rollback procedure for failed deployments
- Add CI checks for shell scripts (shellcheck)
