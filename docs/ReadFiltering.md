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

## Workflow Rules

Output of `taco ls read_filtering`: 

```text
pull_biocontainers

    Pull the required versions of containers from quay.io.

download_reads

    Fetch user-requested files from OSF
    containing reads that will be used
    in the read filtering process.

    Note that this should define wildcard-based
    rules, rather than downloading all files
    at once, to keep things flexible and fast.

download_read_adapter

    Download FASTA read adapaters.
    This downloads adpaters for
    the TruSeq2-PE sequencer by default.

pre_trimming_quality_assessment

    Perform a pre-trimming quality check
    of the reads from the sequencer.

post_trimming_quality_assessment

    Perform a post-trimming quality check
    of the reads from the sequencer.

quality_trimming

    Trim reads from the sequencer by dropping low-quality reads.

interleave_reads

    Interleave paired-end reads using khmer.
    The trim quality comes from the filename.
```

## Workflow Parameters

Default parameter dictionary defined in `read_filtering.settings`:

```text
{
    "short_description": "Read Filtering Walkthrough 1 - Fetching Reads - Parameters",
    "read_filtering" : {
        "read_files" : {
            "SRR606249_1.fq.gz" :           "files.osf.io/v1/resources/dm938/providers/osfstorage/59f0f9156c613b026430dbc7",
            "SRR606249_2.fq.gz" :           "files.osf.io/v1/resources/dm938/providers/osfstorage/59f0fc7fb83f69026076be47",
            "SRR606249_subset10_1.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f10134b83f69026377611b",
            "SRR606249_subset10_2.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f101f26c613b026330e53a",
            "SRR606249_subset25_1.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f1039a594d900263120c38",
            "SRR606249_subset25_2.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f104ed594d90026411f486",
            "SRR606249_subset50_1.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f1082d6c613b026430e5cf",
            "SRR606249_subset50_2.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f10ac6594d900262123e77"
        },
        "read_patterns" : {
            "pre_trimming_pattern"  : "{sample}_{direction}.fq.gz"
        }
    }
}
```

