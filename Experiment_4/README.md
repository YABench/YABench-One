# Experiment 4: Gracious mode

The experiment evaluates the engines with a **SELECT** query combined with a **FILTER** statement which joins graph patterns matching triples that were received at different timestamps. It returns a temperature value which is higher by specified threshold than another temperature value measured by the same station in a given window.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of weather stations (see next section), but the other settings are the same:

Settings | Value
---------|------
Window size and slide | 5 sec
Interval between the measurements of a single station | 1 sec
Duration of the test | 30 sec

### C-SPARQL & CQELS

Name of test | # of stations (C-SPARQL) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_4/csparql/config.json)) | # of stations (CQELS) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_4/cqels/config.json))
-------------|--------------------------|----------------------
SMALL | 50 | 50
MEDIUM | 1000 | 150
BIG | 2500 | 300

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_4/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_4/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find how to visualise the results.

## Discussion
