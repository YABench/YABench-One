# Experiment 4: Gracious mode

The experiment uses the same query from [Experiment 3](https://github.com/YABench/yabench-one/tree/master/Experiment_3), but the goal is to demonstrate the *gracious mode* of the oracle. In this mode the oracle adjusts the window scope of expected window &#x1D54E;<sub>e</sub> to match the window scope of actual window &#x1D54E;<sub>a</sub> which allows to overcome the effect of the shifted window described in [Experiment 1](https://github.com/YABench/yabench-one/tree/master/Experiment_1).

## Settings

In this experiment we use only two tests for each engine with the following common settings:

Settings | Value
---------|------
Window size and slide | 5 sec
Interval between the measurements of a single station | 1 sec
Duration of the test | 20 sec
# of stations | 1

### Tests

Name of test | Gracious mode
-------------|--------------------------
gracious | true
non-gracious | false

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_4/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_4/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find how to visualise the results.

### C-SPARQL

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_4/csparql/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for C-SPARQL. Precision and recall per window
</p>

### CQELS

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_4/cqels/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for CQELS. Precision and recall per window
</p>

## Discussion
