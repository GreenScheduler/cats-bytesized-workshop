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

## Using MyBinder 

If you cannot install CATS on your local computer then you can run it in the Cloud using MyBinder. This will not be able to use slurm or at but will let you try out some of the other parts. 

Click the image below to launch and then open a terminal when the JupyterHub page opens.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/GreenScheduler/cats-bytesized-workshop/binder)

