# YABench-One

A benchmark testing SELECT, aggregate, and join query capabilities of C-SPARQL and CQELS engines.

## Preparing

First, you need to clone this repository and download the [latest release](https://github.com/YABench/yabench/releases/latest) of the YABench framework.

Make sure that you have installed all prerequisites and dependencies which are listed on the [Installing](https://github.com/YABench/yabench/wiki#installing) wiki page.

Now you're ready to run the tests!

## Running

Example command to execute a test:
```
./yabench-runner/runner.py <test folder> -Dexec.oracle=<path to Oracle's .jar> -Dexec.generator=<path to Generator's .jar> -Dexec.engine=<path to Engine's jar>
```

For example, if you've unpacked the release archive to the cloned repository folder, you should have the following folder structure:
```
-- .
-- Experiment_1/
-- Experiment_2/
...
-- Experiment_4/
...
-- yabench-<version>/
```

If you want to run Experiment #1 with CQELS engine, you need to execute the following command:
```
./yabench-<version>/yabench-runner/runner.py Experiment_1/cqels -Dexec.oracle=yabench-<version>/yabench-oracle.jar -Dexec.engine=yabench-<version>/yabench-cqels.jar
-Dexec.engine=yabench-<version>/yabench-generator.jar
```

The results can be found in the `Experiment_1/cqels/results` folder. They can be visualized with the `yabench-reports` web application, see [Visualisation of the results](https://github.com/YABench/yabench/wiki#visualisation-the-results) wiki page.
