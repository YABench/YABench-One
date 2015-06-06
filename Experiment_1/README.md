# Experiment 1: A simple SELECT combined with a FILTER

The experiment evaluates the engines with a simple **SELECT** query combined with a **FILTER** statement asking for the latest temperature observations above a specified threshold and the sensor which took the measurement.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of weather stations (see next section), but the other settings are the same:

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

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_1/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_1/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find how to visualise the results.

## Discussion

The results conducted with C-SPARQL show that the precision and recall per window degrades under high loads, i.e. with 10 000 stations it drops drastically. It's expected that with 50 stations (SMALL) each window contains 1 750 triples and with 10 000 stations (BIG) this number grows up to 350 098 triples. The reason why precision and recall decrease, is essentially given by the fact that higher loads leads to bigger delays in query result delivery.

Delay for low load ranges from a minimum of 41ms to a maximum of 112ms. The maximum is reached at the very beginning representing the so called warm-up phase of an engine. After this phase the delay times even out. The same appears to happen for the high load scenario, however, at a much different scale. The delay times range from 793ms to 2 807ms, hence, the average is 20-25 times higher the low load scenario.

![Lower precision and recall due to delay of actual window](http://yabench.github.io/yabench-one/Experiment_1/winshift.png "Lower precision and recall due to delay of actual window &#x1D54E;<sub>a</sub>")

This delay, consecutively, allows to draw the conclusion that the actual windows are shifted, therefore, deviating from the ideal windows computed by the oracle as shown in figure above. Given a query which asks for all statements occurring on stream &#x1D54A;, a delay between start and end timestamps of the expected window computed by the oracle &#x1D54E;<sub>e</sub> and the actual window &#x1D54E;<sub>a</sub> by the engine, can be observed. This is also the reason for lower precision and recall values. &#x1D54E;<sub>e</sub> contains only one (*s<sub>2</sub>*) of three relevant statements (blue filling), hence, recall *r* = 1/3. Out of the two selected statements of &#x1D54E;<sub>e</sub> ({*s<sub>1</sub>*, *s<sub>2</sub>*}) only the latter one is relevant, hence, precision *p* = 1/2. In other words, whereas the scope of an ideal window is [*t<sub>s</sub>*, *t<sub>e</sub>*), the scope of shifted windows adds a delay to the start and end timestamps and is denoted as [*t<sub>s</sub>* + *d<sub>s</sub>*, *t<sub>e</sub>* + *d<sub>e</sub>*). It is worth to note that *d<sub>s</sub>* and *d<sub>e</sub>* can be different due to timing issues of engines. This explains different declines in precision and recall.

Moreover, we can also see variations between actual and expected result size in triples, the first coming from the engine, the latter being calculated by the oracle.

Performance results of both low and high load experiments highlight memory consumption. It can be observed that in the low load scenario, memory consumption quickly rises to 99MB and slowly rises to 150MB, however, than appears to flatten out. In the high load scenario memory consumption rises continuously for about 20 seconds and then starts to even out at a level of about 895MB.
