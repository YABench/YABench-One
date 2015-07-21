# Experiment 1: SELECT combined with a FILTER

The experiment evaluates the engines with a **SELECT** query combined with a **FILTER** statement asking for the latest temperature observations above a specified threshold and the sensor which took the measurement.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of simulated weather stations (see next section), but the remaining settings are the same:

Settings | Value
---------|------
Window size and slide | 5 sec
Interval between the measurements of a single station | 1 sec
Duration of the test | 30 sec

### C-SPARQL & CQELS

Name of test | # of stations (C-SPARQL) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_1/csparql/config.json)) | # of stations (CQELS) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_1/cqels/config.json))
-------------|--------------------------|----------------------
SMALL | 50 | 50
MEDIUM | 1000 | 1000
BIG | 10000 | 10000

The BIG test for CQELS is not published yet, since the oracle did not finish within a reasonable amount of time. We are currently investigating towards running the oracle on a cluster. Results will be updated once we have them.

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_1/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_1/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find out how to visualise the results.

### Precision & Recall
<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_s_pr.png" width="80%"/>
    </br>
    Fig. 1. Experiment 1 <i>SMALL</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_m_pr.png" width="80%"/>
    </br>
    Fig. 2. Experiment 1 <i>MEDIUM</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_b_pr.png" width="80%"/>
    </br>
    Fig. 3. Experiment 1 <i>BIG</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>

### Delay

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_s_d.png" width="80%"/>
    </br>
    Fig. 4. Experiment 1 <i>SMALL</i> scenario delay for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_m_d.png" width="80%"/>
    </br>
    Fig. 5. Experiment 1 <i>MEDIUM</i> scenario delay for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_b_d.png" width="80%"/>
    </br>
    Fig. 6. Experiment 1 <i>BIG</i> scenario delay for CQELS and C-SPARQL.
</p>

### Performance

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_s_p.png" width="80%"/>
    </br>
    Fig. 7. Experiment 1 <i>SMALL</i> scenario performance results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_s_p.png" width="80%"/>
    </br>
    Fig. 8. Experiment 1 <i>MEDIUM</i> scenario performance results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/e1_s_p.png" width="80%"/>
    </br>
    Fig. 9. Experiment 1 <i>BIG</i> scenario performance results for CQELS and C-SPARQL.
</p>