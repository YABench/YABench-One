# Experiment 2: An aggregate (AVG) query combined with a FILTER

The experiment evaluates the engines with an aggregate (**AVG**) query combined with a **FILTER** statement returning one average temperature value over a given window instead of a set of triples. We note that aggregate queries are a crucial means in stream processing settings to receive data summaries or reveal trends.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of weather stations (see next section), but the other settings are the same:

Settings | Value
---------|------
Window size and slide | 5 sec
Interval between the measurements of a single station | 1 sec
Duration of the test | 30 sec

### C-SPARQL & CQELS

Name of test | # of stations (C-SPARQL) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_2/csparql/config.json)) | # of stations (CQELS) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_2/cqels/config.json))
-------------|--------------------------|----------------------
SMALL | 50 | 50
MEDIUM | 1000 | 150
BIG | 10000 | 300

The SMALL test is the same for both engine that allows us to compare their results. By at the rest of tests we evaluate the scalability of the engines, so we set the maximum number of stations which the oracle can compute the correctness with. [In case of CQELS the oracle requires a lot more time to check the correctness](TODO) therefore the number is significantly lower.

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_2/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_2/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find how to visualise the results.

### C-SPARQL

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/csparql/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for C-SPARQL. Precision and recall per window
</p>

### CQELS

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/cqels/ORACLE_pr.png"/>
    </br>
    Fig 2. The results of the experiment for CQELS. Precision and recall per window
</p>

## Discussion

### C-SPARQL

The results of the experiment conducted with C-SPARQL show that even a slight *shift* of actual window &#x1D54E;<sub>a</sub> may result in low precision and recall values in case of an aggregate query. The notion of shifted window is demonstrated in [Experiment 1](https://github.com/YABench/yabench-one/tree/master/Experiment_1).

Performance results are close to the results of Experiment 1. The memory consumption constantly grows up to the similar levels.

### CQELS

As mentioned in Experiment 1, the oracle checks the correctness of the query results outputted by an engine implementing *content change* reporting policy in a different way. It'd be expected to see precision and recall values whether 0 or 100%, but with CQELS the values are average precision and recall in a given window, therefore they are not only 0 or 100%.

All windows have low precision and recall values, except the first one. This situation is explained by the issue of CQELS when the purging of content of the previous window from the engine's actual window is delayed. Therefore we see 100% p/r for the first window, since there is no previous window whose content would be in the active window, and 0% for the others, since each of them include content of a previous window. This behavior is not considered by the oracle, because of that, precision and recall are so low.

Performance results are very similar to the results of Experiment 1. The memory consumption constantly grows up to the similar levels.
