---
title: Setup
---


## Installing CATS

Optionally create a new virtual environment:

```bash
python -m venv cats-env
source cats-env/bin/activate
```

Install CATS using pip. 

```bash
python -m pip install climate-aware-task-scheduler
```

### Installing a scheduler

To fully use CATS you will need a scheduler such as `at` or `slurm`. Without one CATS will simply tell you what time the job should be started at. Most Linux and Mac systems will already have `at` installed. Slurm is typically only available on HPC clusters. Windows does not come with a scheduler that CATS can use, so Windows users will either need to manually start a job or use WSL where `at` can be installed. 

