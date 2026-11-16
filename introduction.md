---
title: "Using CATS"
teaching: 5 # teaching time in minutes
exercises: 15 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you use CATS to run computational jobs when grid carbon intensity is lowest?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- How to run CATS jobs with the at scheduler.
- How to run CATS jobs with the slurm scheduler.
::::::::::::::::::::::::::::::::::::::::::::::::

## Running CATS without a scheduler

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Run CATS without a scheduler

CATS has one required argument, `-d` or `--duration` for the duration of the job in minutes. This is usually a best estimate, but it should be the upper end of what is likely. 

By default CATS uses the UK Carbon Intensity provider to get grid carbon intensity. This needs to know your approximate location to work out which of the UK's (or more precisely Britain's, as Northern Ireland is part of the Irish grid) 14 grid regions you are located in. Obviously this needs to be somewhere in the UK for there to be any valid UK Carbon Intensity data. We'll show an example of looking up locations outside the UK later on. With no location specified CATS will try to work out your location from your internet IP address. 

```bash
cats -d 180 
```

:::::::::::::::::::::::: solution 

## Output
 
```output
WARNING:root:Use of config.yaml is deprecated. We suggest renaming to 'cats_config.yml'

WARNING:root:location not provided. Estimating location from IP address: SA68.

The.____ ..... __ .... ________ . ______...
.. /  __)...../  \....(__    __).)  ____)....
..|  /......./    \......|  |...(  (___........
..| |limate./  ()  \ware.|  |ask.\___  \cheduler
..|  \__...|   __   |....|  |....____)  )....
...\    )..|  (..)  |....|  |...(      (..


Best job start time                       = 2026-11-17 08:49:43
Carbon intensity if job started now       = 212.86 gCO2eq/kWh
Carbon intensity at optimal time          = 105.80 gCO2eq/kWh
```

:::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 2: specify your location to CATS

CATS can be given a location by using the first part of a UK postcode, for example L1 for Liverpool, SW1A for London (Westminster), OX1 for Oxford, M1 for Manchester, EH1 for Edinburgh or IV1 for Inverness. This is specified with the `-l` or `--location` option. 

Try specifying a location for your job using the first part of a UK postcode. Try comparing different regions using the postcodes listed above. On a windy day Edinburgh or Manchester will often have lower carbon intensity since those regions have a lot of wind turbines. On sunnier days Oxford or London can be lower as there is more solar power in the South of England. You can check the current carbon intensity on the website [https://carbonintensity.org.uk](https://carbonintensity.org.uk). 


:::::::::::::::::::::::: solution 

```bash
cats -d 180 -l SW1A
```

```bash
cats -d 180 -l OX1
```
```bash
cats -d 180 -l L1
```

```bash
cats -d 180 -l M1
```


```bash
cats -d 180 -l EH1
```

cats -d 180 
:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 3: Running CATS with the at scheduler

The `at` scheduler dates back to early versions of a Unix and is used to run a given command at a certain time. It features some basic job queueing capabilities where multiple jobs can be waiting to run at different times. CATS can invoke `at` automatically by using setting the `-s` or `--scheduler` option to "at" and the `-c` option to specify the command to run. 

```bash
cats -d 180 -l L1 -s at -c "echo hello world"
```
This should finish the output with the job's number and scheduled start time. 

```output
job 1 at Tue Nov 17 22:50:00 2026
```
We can also check the queue with the `atq` command:

```bash
atq
```

```output
1	Tue Nov 17 22:50:00 2026 a colin
```

If we decide we don't want to run the job then we can use the `atrm` command to remove it from the queue.

```bash
atrm 1
```
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 4: Running CATS with the Slurm scheduler

The Slurm scheduler is a popular open source scheduler used on many HPC systems including several UK national facility systems such as Isambard, Archer, Bede, Baskerville, Dawn and JASMIN. CATS can invoke Slurm by using setting the `-s` or `--scheduler` option to "slurm" and the `-c` option to specify the command to run. 

```bash
cats -d 180 -l L1 -s slurm -c "echo hello world"
```
This should finish the output with the job's number and scheduled start time. 

```output
```

We can also check the queue with the `squeue` command:

```bash
squeue
```

```output
```

If we decide we don't want to run the job then we can use the `scancel` command to remove it from the queue.

```bash
scancel 12345
```
::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 5: Using a CATS configuration file

Instead of specifying arguments on the command line, CATS can also read these from a configuration file. This is useful if you are repeatedly running CATS.

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints 

- The `--duration` or `-d` options to CATS specify the job duration.
- The `--location` or `-l` options to CATS specify the location where the job is running. This is used to identify the grid region it is running in. By default this uses the UK Carbon Intensity data provider.


::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
