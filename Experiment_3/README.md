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

### C-SPARQL

As it's shown on the charts, the precision and recall values decrease under high load. Under low load precision and recall values are higher than 75%, but the other charts the last windows are already have 0% precision and recall. This situation is explained in the same way it was explained in Experiment 1: the reason is the delay of the actual window.

Performance results are close to the results of Experiment 1. The memory consumption constantly grows up to the similar levels.

### CQELS

In this experiment it's also observed how the issue with purging the content of the previous window affects precision and recall values. Precision and recall values of all windows, except the first one, are near 50%, because roughly half of the results go from the content of the previous window and the other half from the content of the current window.

Performance results are close to the results of Experiment 1. The memory consumption constantly grows up to the similar levels.
