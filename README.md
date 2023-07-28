## TAOS

This repository contains the simulation code of taos (task assignment and order scheduling) 
related algorithms.

We implement five algorithms, OBTA, NLIP, WF, OCWF, and OWCF-ACC. The first three algorithms 
are FIFO algorithms without adjusting outstanding jobs' orders while the last two algorithms 
are SJF algorithms.

### Setup

We use [Alibaba cluster-trace-v2017]([https://github.com/alibaba/clusterdata/blob/master/cluster-trace-v2017/trace_201708.md) 
to drive the simulation. We extract a segment from the file `batch_task.scv` in cluster-trace-v2017 
that contains 250 jobs. These jobs include 113653 task instances in total. We derive 
task durations from the timestamps of the recorded task events. We scale the inter-arrival 
times of the jobs to simulate different levels of system utilization from 50% to 75%. 
The default number of sites is 100.

The default settings are with `env.py`. You may change the settings at your wish 
to test the performance and efficiency of the algorithms.

### Run

You can run ``main.py`` directly to obtain the simulation results in default settings. 
You may use the file ``draw/draw.ipynb`` to obtain the figures of average JRTs, CDF of JRTs, etc.

### Dependencies

See ``requirements.txt``.

The code depends on package `docplex`. You should have a **commercial** or **academic** version 
(NOT the no-cost edition!) of CPLEX optimization studio installed, and then install the package `docplex` as guided.
