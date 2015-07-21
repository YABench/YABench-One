# Experiment 3: SELECT query joining graph patterns matching triples received at different times combined with FILTER

The experiment evaluates the engines with a **SELECT** query combined with a **FILTER** statement which joins graph patterns matching triples that were received at different timestamps. It returns a temperature value which is higher than another temperature value measured by the same station in a given window.

## Settings

Three different tests are used to evaluate the engines. The tests are different from each other only by the number of simulated weather stations (see next section), but the remaining settings are the same:

Settings | Value
---------|------
Window size and slide | 5 sec
Interval between the measurements of a single station | 1 sec
Duration of the test | 30 sec

### C-SPARQL & CQELS

Name of test | # of stations (C-SPARQL) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_3/csparql/config.json)) | # of stations (CQELS) ([config.json](https://github.com/YABench/yabench-one/blob/master/Experiment_3/cqels/config.json))
-------------|--------------------------|----------------------
SMALL | 50 | 50
MEDIUM | 200 | 200
BIG | 500 | 500

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_3/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_3/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find how out to visualise the results.

### Precision & Recall
<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_s_pr.png"/>
    </br>
    Fig. 1. Experiment 3 <i>SMALL</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_m_pr.png"/>
    </br>
    Fig. 2. Experiment 3 <i>MEDIUM</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_b_pr.png"/>
    </br>
    Fig. 3. Experiment 3 <i>BIG</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>

### Delay

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_s_d.png"/>
    </br>
    Fig. 4. Experiment 3 <i>SMALL</i> scenario delay for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_m_d.png"/>
    </br>
    Fig. 5. Experiment 3 <i>MEDIUM</i> scenario delay for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_b_d.png"/>
    </br>
    Fig. 6. Experiment 3 <i>BIG</i> scenario delay for CQELS and C-SPARQL.
</p>

### Performance

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_s_p.png"/>
    </br>
    Fig. 7. Experiment 3 <i>SMALL</i> scenario performance results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_s_p.png"/>
    </br>
    Fig. 8. Experiment 3 <i>MEDIUM</i> scenario performance results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_3/e3_s_p.png"/>
    </br>
    Fig. 9. Experiment 3 <i>BIG</i> scenario performance results for CQELS and C-SPARQL.
</p>