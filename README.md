# Day 13 — Docker Security & Optimization

## Objective
Compare an intentionally unsafe Docker image with a safer image, scan both using Trivy, and apply runtime security restrictions.

## Project files
- Dockerfile.bad — intentionally unsafe baseline image
- Dockerfile.good — improved multi-stage image
- app.py — Flask demo application
- requirements.txt — pinned Flask dependency
- .dockerignore — excludes unnecessary and sensitive local files
- reports/before.json — baseline Trivy report
- reports/after.json — improved image Trivy report
- reports/comparison.md — before/after comparison

## Security improvements
- Replaced python:latest with python:3.12-slim.
- Used a multi-stage build.
- Installed Python dependencies without pip cache.
- Configured a non-root application user.
- Removed the hardcoded API_TOKEN from the improved image.
- Applied CPU, memory and PID limits at runtime.
- Enabled a read-only root filesystem.
- Mounted /tmp as tmpfs.
- Dropped Linux capabilities.
- Enabled no-new-privileges.

## Validation
- Verified the improved image runs as user app (UID 10001).
- Verified runtime security settings using docker inspect.
- Checked runtime resource usage with docker stats.
- Scanned both images with Trivy.

## Scan results
See reports/comparison.md for the recorded image sizes and vulnerability counts.

The improved image still reports 44 HIGH vulnerability entries. This lab does not claim that the image is vulnerability-free; further remediation is needed.

## Important security note
The training token is fake and must not be committed. Do not push the intentionally vulnerable image to a public registry.
