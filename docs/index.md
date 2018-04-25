# taco-read-filtering

This repository implements a read filtering workflow for 
[dahak-taco](https://github.com/dahak-metagenomics/dahak-taco).



# Quick Start

## List Available Actions

```
taco ls             # List available workflows

taco ls workflow1   # List rules in workflow 1

taco ls workflow2   # List rules in workflow 2
```

## Run Workflow

Include the `-n` flag to do a dry run first.

taco requires the `--config-json` and `--params-json` 
flags to point to the configuration and parameter
JSON/YAML files.

```
taco -n workflow1 \
    --config-json=workflow-config/config_step1.json \
    --params-json=workflow-params/params_step1.json

taco -n workflow2 \
    --config-json=workflow-config/config_step2.json \
    --params-json=workflow-params/params_step2.json

...etc...

taco -n workflow6 \
    --config-json=workflow-config/config_step6.json \
    --params-json=workflow-params/params_step6.json
```

To run the workflow:

```
taco -n workflow1 \
    --config-json=workflow-config/config_step1.json \
    --params-json=workflow-params/params_step1.json

taco -n workflow2 \
    --config-json=workflow-config/config_step2.json \
    --params-json=workflow-params/params_step2.json

...etc...

taco -n workflow6 \
    --config-json=workflow-config/config_step6.json \
    --params-json=workflow-params/params_step6.json
```



# Details

## `rules/` Directory

The rules directory contains one folder per workflow.

Each workflow folder must include a `Snakefile`.
It is recommended to structure Snakefiles so that 
they import individual rule files. Individual rule
files then use workflow parameters from the parameters
file the user passed in.

## `workflow-config` Directory

The config files define the target files or rules for Snakemake to run.

## `workflow-params` Directory

The parameter files define values for the workflow parameters 
used to define the Snakemake rules.



# Links

[dahak-taco documentation](https://dahak-metagenomics.github.io/dahak-taco/)

[dahak-taco github repo](https://github.com/dahak-metagenomics/dahak-taco)

[taco-simple github repo](https://github.com/dahak-metagenomics/taco-simple)


