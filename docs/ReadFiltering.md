# Read Filtering Workflow

The `read_filtering` workflow uses 
`fastq` and `trimmomatic` to assess
the quality of sequencer reads and 
filter out low-quality reads.

The user has control over the names 
and URLs of sequence data that is 
downloaded, as well as parameters like
the quality threshold.


## Quick Start

To list available workflows (only one):

```
$ taco ls
```

To get rules defined by the workflow:

```
$ taco ls read_filtering
```

To run the workflow using the provided
workflow config and parameter files,

```
$ taco read_filtering \
    --config-yaml=workflow-config/config_step1.yaml \
    --params-yaml=workflow-params/config_step1.yaml
```

By default, this will generate output files in the `data/` directory.
To change the output directory, use the `--prefix` flag:

```
$ taco --prefix=my_data read_filtering \
    --config-yaml=workflow-config/config_step1.yaml \
    --params-yaml=workflow-params/config_step1.yaml
```

If the directory does not exist, it will be created.

Continue reading for more details about how to determine
what rules a workflow defines, how to set parameters
for the read filtering workflow, and the various 
target files that are useful for the workflow config
file.

