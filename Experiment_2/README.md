# Experiment 2: An aggregate (AVG) query combined with a FILTER

The experiment evaluates the engines' capability to handle aggregate (**AVG**) queries combined with a **FILTER** statement which returns one average temperature value over a given window instead of a set of triples. We note that aggregate queries are a crucial means in stream processing settings to receive data summaries or reveal trends in real-time.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of simulated weather stations (see next section), but the remaining settings are the same:

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

The remaining tests evaluate the scalability of the engines by setting the maximum number of stations. [In case of CQELS the oracle requires a lot more time to check the correctness](TODO) therefore the number of stations is lower.

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_2/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_2/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find out how to visualise the results.

### C-SPARQL

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/csparql/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for C-SPARQL. Precision and recall per window.
</p>

### CQELS

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/cqels/ORACLE_pr.png"/>
    </br>
    Fig 2. The results of the experiment for CQELS. Precision and recall per window.
</p>

## Discussion

### C-SPARQL

The results of the experiment conducted with C-SPARQL show that even a slight *shift* of actual windows &#x1D54E;<sub>a</sub> results in low precision and recall values in case of an aggregate query. The notion of shifted windows is demonstrated in [Experiment 1](https://github.com/YABench/yabench-one/tree/master/Experiment_1). The reason is that an aggregate query typically only returns one value. Hence, if this returned value does not match precisely the expected value, precsion and recall will be zero. Since one missing triple (for instance due to slight delay) already influences the resulting aggregate value, this happens quickly. We did some manual testing with *gracious mode* (explained in section **3.4 Oracle** in the paper) which makes the oracle aware of window border shifts resulting in higher precision and recall values.

Performance results are close to the results of Experiment 1. Memory consumption constantly grows up to similar levels.

### CQELS

As mentioned in Experiment 1, the oracle checks the correctness of the query results outputted by an engine implementing *content change* reporting policy in a different way. It'd be expected to see precision and recall values at either 0% or 100%, but with CQELS the values are averaged over a given window resulting in more granular values.

All windows have low precision and recall values, except the first one. This situation is explained by an issue of CQELS, that is, it forgets to purge content of the previous window from its actual window. Therefore we see precision and recall of 100% for the first window, since there is no previous window whose content would be left in the active window. For the remaining windows we observe 0%, since each of them erroneously includes content of a previous window. This behavior is not considered by the oracle, because of that, precision and recall are so low.

Performance results are very similar to the results of Experiment 1. The memory consumption constantly grows up to the similar levels.
