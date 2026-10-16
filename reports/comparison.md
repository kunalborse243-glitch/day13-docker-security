# Day 13 — Docker Security Comparison

| Metric | Before (my-app:bad) | After (my-app:v2) |
|---|---:|---:|
| Image disk usage | 1.76 GB | 185 MB |
| HIGH vulnerability entries | 401 | 44 |
| CRITICAL vulnerability entries | 16 | 0 |
| Base image | python:latest | python:3.12-slim |
| Runtime user | Root by default | app (non-root) |
| API token embedded in image ENV | Yes | No |
| Read-only root filesystem | No | Yes, at runtime |
| CPU limit | Not configured | 0.5 CPU |
| Memory limit | Not configured | 256 MiB |
| PID limit | Not configured | 100 |
| Linux capabilities | Default set | All dropped |
| no-new-privileges | Not configured | Enabled at runtime |

## Results

- HIGH findings reduced from 401 to 44 (approximately 89.0% fewer).
- CRITICAL findings reduced from 16 to 0.
- Image disk usage reduced from 1.76 GB to 185 MB.
- The safer image runs as a non-root user.
- Runtime hardening restrictions were confirmed using docker inspect.
- Trivy still reports 44 HIGH findings. Further remediation and rescanning are needed before claiming the image is vulnerability-free.

## Notes

Trivy counts vulnerability entries, which may include repeated CVEs across packages.
The before/after comparison uses the saved reports generated during this lab.
Image size uses Docker's displayed disk usage values.
