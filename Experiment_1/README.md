# Experiment 1: A simple SELECT combined with a FILTER

The experiment evaluates the engines with a simple **SELECT** query combined with a **FILTER** statement asking for the latest temperature observations above a specified threshold and the sensor which took the measurement.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of weather stations.

The common settings:
 * window size and slide: 5 seconds,
 * interval between the measurements of a single station: 1 second,
 * duration of the test: 30 seconds

### C-SPARQL

Tests and settings ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_1/csparql/config.json)):
 * SMALL - number of stations: 50
 * MEDIUM - number of stations: 1000
 * BIG - number of stations: 10000

### CQELS

Tests and settings ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_1/cqels/config.json)):
 * SMALL - number of stations: 50
 * MEDIUM - number of stations: 150
 * BIG - number of stations: 300

## Results

## Discussion
