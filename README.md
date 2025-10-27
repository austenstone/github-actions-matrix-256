# GitHub Actions Matrix 512 🚀

This repository demonstrates how to bypass GitHub Actions' 256 matrix job limit using reusable workflows to create **512 total matrix jobs**!

## How it works

GitHub Actions has a documented limit of 256 matrix jobs per workflow run. However, this limit applies *per workflow*, not per workflow run. By using reusable workflows, we can multiply the number of jobs:

- **Parent workflow** (`parent.yml`): Creates 2 matrix jobs
- **Child workflow** (`child.yml`): Each parent job calls this with a matrix of 256 jobs
- **Total**: 2 × 256 = **512 jobs** 🎉

## The Setup

```
parent.yml (2 matrix jobs)
    ↓
child.yml (256 matrix jobs each)
    ↓
512 total jobs across both workflows
```

## Running the workflow

1. Go to the Actions tab in your GitHub repository
2. Select "Manual trigger" workflow
3. Click "Run workflow"
4. Watch as GitHub creates 512 concurrent jobs! 😮

## Theory vs Practice

In theory, you could nest workflows up to 4 levels deep:
- 256^4 = **4,294,967,296 jobs** per workflow run! 🤯

In practice, GitHub's UI starts timing out after ~600 jobs, and too many jobs might get your Actions disabled (ask me how I know 😅).

## Files

- `parent.yml`: The main workflow that creates the initial matrix
- `child.yml`: The reusable workflow called by each parent matrix job
- This README explaining the madness

## Why?

Because we can! 🔥 This explores an interesting behavior where GitHub's 256-job limit is per-workflow, not per-workflow-run, allowing creative workarounds with reusable workflows.

---

*Warning: Use responsibly! Don't blame me if GitHub disables your Actions account* 😉