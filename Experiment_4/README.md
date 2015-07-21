# Experiment 4: Gracious mode

The experiment uses the same query as [Experiment 3](https://github.com/YABench/yabench-one/tree/master/Experiment_3), but the goal is to demonstrate the *gracious mode* of the oracle (explained also in section **3.4 Oracle** in the paper). In this mode the oracle adjusts the window scope of an expected window &#x1D54E;<sub>e</sub> to match the window scope of an actual window &#x1D54E;<sub>a</sub> allowing to overcome the effect of the shifted window described in [Experiment 1](https://github.com/YABench/yabench-one/tree/master/Experiment_1).

## Settings

In this experiment we use only two tests for each engine with the following settings:

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

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_4/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_4/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find out how to visualise the results.

### C-SPARQL

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_4/e4_cs_gracious.png"/>
    </br>
    Fig 1. Experiment 4 *gracious* precision and recall results for C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_4/e4_cs_non-gracious.png"/>
    </br>
    Fig 2. Experiment 4 *non-gracious* precision and recall results for C-SPARQL.
</p>

### CQELS

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_4/e4_cq_gracious.png"/>
    </br>
    Fig 3. Experiment 4 *gracious* precision and recall results for CQELS.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_4/e4_cq_non-gracious.png"/>
    </br>
    Fig 4. Experiment 4 *non-gracious* precision and recall results for CQELS.
</p>