# Challenges Running Deep Learning in CPU vs GPU Environments (and How I Solved Them)

## Table of Contents

1. [Overview](#overview)  
2. [Setup & Tools](#setup--tools)  
3. [Issue 1: GPU Performance Tanked](#issue-1-gpu-performance-tanked)  
4. [Issue 2: Devcontainers Take Getting Used To](#issue-2-devcontainers-take-getting-used-to)  
5. [Issue 3: PDF Export Fails (And I Had No Disk Space)](#issue-3-pdf-export-fails-and-i-had-no-disk-space)  


---

## Overview

The goal was to:
- Run a Fastai deep learning model in both CPU and GPU modes
- Benchmark training time across different batch sizes
- Observe GPU usage with `nvtop`
- Export the results into a clean report

Everything worked... eventually.

---

## Setup & Tools

I ran this project inside a VSCode devcontainer running Ubuntu 22.04 with Fastai and Jupyter pre-installed.

To verify GPU availability:

```python
import torch
print("GPU available:", torch.cuda.is_available())
```
## Issue 1: GPU Performance Tanked

At first, my GPU performance was inconsistent. Some runs were fast, others painfully slow — especially at larger batch sizes.

**Cause:** My laptop charger was intermittently disconnecting. When unplugged, the GPU would throttle to conserve power, cutting performance significantly.

### Fix
I replaced the charger. GPU performance immediately improved and became consistent.

**Lesson:** A flaky power connection can silently ruin your benchmarks.

## Issue 2: Devcontainers Take Getting Used To

Devcontainers are great once you're set up, but I initially ran into a few issues:

- Couldn't access local files easily

- File paths were container-specific

- Some outputs like screenshots and PDFs were harder to export

### Fix
I explored the file structure, learned how to work within the container, and adjusted my workflow.

**Lesson:** Containers are powerful, but expect a learning curve when you first use them.


## Issue 3: PDF Export Fails (And I Had No Disk Space)

When I tried exporting the notebook with:
```
jupyter nbconvert --to pdf my_notebook.ipynb
```
I got the error:

``
OSError: xelatex not found on PATH
``

Installing LaTeX (`xelatex`) would fix it, but I didn’t have enough space inside the devcontainer.

### Fix
I exported as HTML instead:

File → Download as → HTML

Opened it in a browser

Printed to PDF via the browser’s "Save as PDF" option

**Lesson:** When LaTeX isn't an option, export as HTML and print to PDF — it works great.
