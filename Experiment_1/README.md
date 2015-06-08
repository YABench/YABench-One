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
MEDIUM | 1000 | 150
BIG | 10000 | 300

The SMALL test is the same for both engines allowing us to compare their results directly. The remaining tests evaluate the scalability of the engines by setting the maximum number of stations. [In case of CQELS the oracle requires a lot more time to check the correctness](TODO) therefore the number of stations is lower.

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_1/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_1/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find out how to visualise the results.

### C-SPARQL
<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/csparql/ORACLE_pr.png"/>
    </br>
    Fig 1. The results of the experiment for C-SPARQL. Precision and recall per window.
</p>

### CQELS

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_1/cqels/ORACLE_pr.png"/>
    </br>
    Fig 2. The results of the experiment for CQELS. Precision and recall per window.
</p>

## Discussion

### C-SPARQL

The results of the experiment conducted with C-SPARQL show that the precision and recall per window degrades under high loads, i.e., with 10 000 stations it drops dramatically. It is expected that with 50 stations (SMALL) each window contains 1 750 triples and with 10 000 stations (BIG) this number grows up to 350 098 triples. The reason why precision and recall decrease is essentially given by the fact that higher loads lead to bigger delays in query result delivery.

Delay for low load ranges from a minimum of 41ms to a maximum of 112ms. The maximum is reached at the very beginning representing the so called warm-up phase of an engine. After this phase the delay times even out. The same appears to happen for the high load scenario, however, at a much different scale. The delay times range from 793ms to 2 807ms, hence, the average is 20-25 times higher the low load scenario.

<p align="center">
  <img src="http://yabench.github.io/yabench-one/Experiment_1/winshift.png"/>
  </br>
  <span>Fig 3. Lower precision and recall due to delay of actual window.</span>
</p>

This delay, consecutively, allows to draw the conclusion that the actual windows are shifted, therefore, deviating from the ideal windows computed by the oracle as shown in Figure 3. Given a query which asks for all statements occurring on stream &#x1D54A;, a delay between start and end timestamps of the expected window computed by the oracle &#x1D54E;<sub>e</sub> and the actual window &#x1D54E;<sub>a</sub> by the engine, can be observed. This is also the reason for lower precision and recall values. &#x1D54E;<sub>e</sub> contains only one (*s<sub>2</sub>*) of three relevant statements (blue filling), hence, recall *r* = 1/3. Out of the two selected statements of &#x1D54E;<sub>e</sub> ({*s<sub>1</sub>*, *s<sub>2</sub>*}) only the latter one is relevant, hence, precision *p* = 1/2. In other words, whereas the scope of an ideal window is [*t<sub>s</sub>*, *t<sub>e</sub>*), the scope of shifted windows adds a delay to the start and end timestamps and is denoted as [*t<sub>s</sub>* + *d<sub>s</sub>*, *t<sub>e</sub>* + *d<sub>e</sub>*). It is worth to note that *d<sub>s</sub>* and *d<sub>e</sub>* can be different due to timing issues of engines. This explains different declines in precision and recall.

Moreover, we can also see variations between actual and expected result size in triples, the first coming from the engine, the latter being calculated by the oracle.

Performance results of both low and high load experiments highlight memory consumption. It can be observed that in the low load scenario, memory consumption quickly rises to 99MB and slowly rises to 150MB, however, then appears to flatten out. In the high load scenario memory consumption rises continuously for about 20 seconds and then starts to even out at a level of about 895MB.

### CQELS

The results of the experiment conducted with CQELS show the precision and recall per window under low, medium, and high loads staying at the same level, i.e., 100%. It is different from the results obtained for C-SPARQL where we can observe that these metrics degrade under high load. This can be explained by the different reporting policies [1] implemented by the engines and the way the oracle handles this difference. CQELS implements the *content change* policy meaning that reporting is done only when the content of the active window changes. C-SPARQL implements the *window close* policy meaning that reporting is done only when the active window closes.

In case of *window close* policy the oracle cannot know which triples are in the *window content*. Therefore, it has to rely on computed window borders determined based on window size and window slide. This introduces a mismatch between the actual and expected window borders. Whereas, in case of *content change* policy the oracle knows that *(a)* each graph of triples with the same timestamp may trigger at least one query result and *(b)* query results are ordered in the same way as the triples in the input stream &#x1D54A;. These two facts prohibit mismatches between actual and expected windows leading to higher precision and recall values.

Performance results of all tests highlight memory consumption. CPU usage and number of spawned threads stay at the same level. In all tests memory consumption continuously rises up to a certain level which is different for each test, however, the number of triples in each window stays the same. In the SMALL setting memory consumption rises up to 265MB, MEDIUM - up to 400MB, BIG - up to 560MB.

## References

1. Botan, I., Derakhshan, R., Dindar, N., Haas, L.M., Miller, R.J., Tatbul, N.: SECRET: A model for analysis of the execution semantics of stream processing systems. PVLDB 3(1), 232–243 (2010)
