# Experiment 3: A SELECT query joining graph patterns matching triples received at different time combined with FILTER

The experiment evaluates the engines with a **SELECT** query combined with a **FILTER** statement which joins graph patterns matching triples that were received at different timestamps. It returns a temperature value which is higher by specified threshold than another temperature value measured by the same station in a given window.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of weather stations (see next section), but the other settings are the same:

Settings | Value
---------|------
Window size and slide | 5 sec
Interval between the measurements of a single station | 1 sec
Duration of the test | 30 sec

### C-SPARQL & CQELS

Name of test | # of stations (C-SPARQL) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_3/csparql/config.json)) | # of stations (CQELS) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_3/cqels/config.json))
-------------|--------------------------|----------------------
SMALL | 50 | 50
MEDIUM | 1000 | 150
BIG | 2500 | 300

The SMALL test is the same for both engine that allows us to compare their results. By at the rest of tests we evaluate the scalability of the engines, so we set the maximum number of stations which the oracle can compute the correctness with. [In case of CQELS the oracle requires a lot more time to check the correctness](TODO) therefore the number is significantly lower.

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_3/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_3/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find how to visualise the results.

### C-SPARQL

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/csparql/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for C-SPARQL. Precision and recall per window
</p>

### CQELS

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/cqels/ORACLE_pr.png"/>
    </br>
    Fig 2. The results of the experiment for CQELS. Precision and recall per window
</p>

## Discussion
