## TAOS

This repository contains the simulation code of taos (task assignment and order scheduling) 
related algorithms.

We implement five algorithms, OBTA, NLIP, WF, OCWF, and OCWF-ACC. The first three algorithms 
are First-Come-First-Serve (FIFO) algorithms without adjusting outstanding jobs' orders while the last two algorithms 
are Shortest-Remaining-Time-First (SRTF) algorithms.

### Setup

We use [Alibaba cluster-trace-v2017]([https://github.com/alibaba/clusterdata/blob/master/cluster-trace-v2017/trace_201708.md) 
to drive the simulation. We extract a segment from the file `batch_task.scv` in cluster-trace-v2017 
that contains 250 jobs. These jobs include 113653 task instances in total. We derive job arrivals 
and task durations from the timestamps of the recorded task events. We scale the inter-arrival 
times of the jobs to simulate different levels of system utilization from 50% to 75%. 
The default number of sites is 100.

The default settings are with `taos/env.py`. You may change the settings at your wish 
to test the performance and efficiency of the algorithms.

### Run

You can run ``taos/main.py`` directly to obtain the simulation results in default settings. 
The output should be similar to:
```text
----------------------- Summary -----------------------
There are 113653 tasks, 250 jobs, 100 sites
OBTA progress:: 100%|██████████| 250/250 [00:23<00:00, 10.78it/s, jrt=8997]
[OBTA] computation overhead: 23.200608 secs
OBTA: 587.412
NLIP progress:: 100%|██████████| 250/250 [00:27<00:00,  9.21it/s, jrt=5908]
[NLIP] computation overhead: 27.136066 secs
NLIP: 565.508
WF progress:: 100%|██████████| 250/250 [00:14<00:00, 17.48it/s, jrt=8052]
[WF] computation overhead: 14.305441 secs
WF: 597.192
OCWF progress:: 100%|██████████| 250/250 [15:16<00:00,  3.67s/it, jrt=7842]
[OCWF] computation overhead: 916.499133 secs
OCWF: 314.972
OCWF-ACC progress:: 100%|██████████| 250/250 [08:23<00:00,  2.01s/it, jrt=7842]
[OCWF-ACC] computation overhead: 503.278144 secs
OCWF-ACC: 314.972

Average computation overhead:

OBTA: 0.027999222755432127
NLIP: 0.0643047227859497
WF: 0.0003121204376220703
OCWF: 3.615326265335083
OCWF-ACC: 1.9634334592819214
```
You may use the file ``draw/draw.ipynb`` to obtain the figures of average JRTs, CDF of JRTs, etc.

### Dependencies

See ``requirements.txt``.

The code depends on package `docplex`. You should have a **commercial** or **academic** version 
(NOT the no-cost edition!) of CPLEX optimization studio installed locally (or you have an IBM
Watson Studio Cloud account), and then install the package `docplex` as guided. The programs are 
formulated and solved in `taos/algo/common.py`.
