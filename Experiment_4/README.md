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
    <img src="http://yabench.github.io/yabench-one/Experiment_4/csparql/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for C-SPARQL. Precision and recall per window.
</p>

### CQELS

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_4/cqels/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for CQELS. Precision and recall per window.
</p>

## Discussion

In addition to the algorithm implemented by the oracle and demonstrated in other experiments, the oracle implements a new method, called *gracious*, which takes into account known issues of supported report policies by the engines and tries to eliminate them. This possibility facilitates detection of new issues unrelated to potential window delays.

* *Content change:* lower precision/recall may be observed, because of delayed purging of content of the previous window from the engine's active window;
* *Window close:* lower precision/recall may be observed, because of the shift of the engine's active window scope forward on the timeline which can be caused, for instance, by high load.

We run two similar tests for both engines, but one of them in *gracious* mode and the other one in *non-gracious* mode. As it may be seen, in *gracious* mode precision/recall is high, but in normal (*non-gracious*) mode it goes down. Since gracious mode successfully eliminates low precision/recall values, we can prove that the implementations of *window close* and *content change* policies by the engines suffer from the issues explained above and in previous experiments. 