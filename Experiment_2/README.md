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
SMALL | 1 | 1
MEDIUM | 1000 | 1000
BIG | 10000 | 10000

Since the MEDIUM scenario yields 0% for precision and recall for both engines (see discussion in the paper) we omit to show results for the BIG scenario here. Additionally, due to drastically increasing delays when running the query of Experiment 2 for CQELS, corresponding delay-plots are omitted. Consequently, the next section shows precision and recall plots for SMALL load, and performances plots for SMALL/MEDIUM/BIG load.

## Results

The results are published online: [C-SPARQL](https://github.com/YABench/yabench-one/tree/master/Experiment_2/csparql/results) and [CQELS](https://github.com/YABench/yabench-one/tree/master/Experiment_2/cqels/results). Take a look at [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page to find out how to visualise the results.

### Precision & Recall
<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/e2_s_pr.png"/>
    </br>
    Fig. 1. Experiment 2 <i>SMALL</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/e2_m_pr.png"/>
    </br>
    Fig. 2. Experiment 2 <i>MEDIUM</i> scenario precision and recall results for CQELS and C-SPARQL.
</p>


### Performance

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/e2_s_p.png"/>
    </br>
    Fig. 3. Experiment 2 <i>SMALL</i> scenario performance results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/e2_s_p.png"/>
    </br>
    Fig. 4. Experiment 2 <i>MEDIUM</i> scenario performance results for CQELS and C-SPARQL.
</p>

<p align="center">
    <img src="http://yabench.github.io/yabench-one/Experiment_2/e2_s_p.png"/>
    </br>
    Fig. 5. Experiment 2 <i>BIG</i> scenario performance results for CQELS and C-SPARQL.
</p>
