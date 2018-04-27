# Read Filtering Workflow Parameters

The default parameter dictionary is defined 
in `read_filtering.settings`. We include a few
notes on each portion of this file.

```text
from snakemake.utils import update_config

if(not config['clean']):
    ...
```

Note that if the `--clean` flag is specified, 
this default configuration is not set.
This can be useful for troubleshooting 
or ensuring all input parameters have been
specified.

```text
    # Note: don't include http:// or https://
    config_default = {
```

The structure of the default config dictionary
is covered on the [Workflows](https://dahak-metagenomics.github.io/dahak-taco/Workflows/)
page of the taco documentation.
It consists of top-level keys named
for the workflow, or for the general 
"common" keys used by most or all rules
(e.g., biocontainers). 

We described the parameter dictionary structure as:

```text
{
    '<workflow-name>' : {
        '<rule-name>' : {
            '<param-name>' : <param-value>,
            '<param-list>' : [<value1>, ...],
            ...
        }
    }
}
```

We see this structure below with two top-level
keys, "biocontainers" and "read_filtering".

```
        "biocontainers" : {
            "trimmomatic" : {
                "use_local" : False,
                "quayurl" : "quay.io/biocontainers/trimmomatic",
                "version" : "0.36--5"
            },
            "fastqc" : {
                "use_local" : False,
                "quayurl" : "quay.io/biocontainers/fastqc",
                "version" : "0.11.7--pl5.22.0_2"
            },
            "khmer" : {
                "use_local" : False,
                "quayurl" : "quay.io/biocontainers/khmer",
                "version" : "2.1.2--py35_0"
            }
        },
```

The biocontainers key stores all information about 
container images for different programs used in this 
workflow. This information is shared across all rules
so it is grouped under a common top-level key.

The other top-level key is the key named for the workflow.

```
        "read_filtering" : {
    
            # Note: read files (below) must match pre-trimming-pattern below.
            # The workflow actually builds the rules to download 
            # the read files by using the pre_trimming_pattern.
            "read_patterns" : {
                "pre_trimming_pattern"  : "{sample}_{direction}_reads.fq.gz",
                "post_trimming_pattern" : "{sample}_{direction}_trim{qual}.fq.gz",
            },
    
            # read_files must be defined by user 
            "read_files" : {
                "SRR606249_1_reads.fq.gz" :           "files.osf.io/v1/resources/dm938/providers/osfstorage/59f0f9156c613b026430dbc7",
                "SRR606249_2_reads.fq.gz" :           "files.osf.io/v1/resources/dm938/providers/osfstorage/59f0fc7fb83f69026076be47",
                "SRR606249_subset10_1_reads.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f10134b83f69026377611b",
                "SRR606249_subset10_2_reads.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f101f26c613b026330e53a",
                "SRR606249_subset25_1_reads.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f1039a594d900263120c38",
                "SRR606249_subset25_2_reads.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f104ed594d90026411f486",
                "SRR606249_subset50_1_reads.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f1082d6c613b026430e5cf",
                "SRR606249_subset50_2_reads.fq.gz" :  "files.osf.io/v1/resources/dm938/providers/osfstorage/59f10ac6594d900262123e77"
            },
    
            "quality_assessment" : {
                # optional, modifiers for the .fq.gz --> .zip --> results workflow
                "fastqc_suffix": "fastqc",
            },
    
            "quality_trimming" : {
                "trim_suffix" : "se"
            },
            "interleaving" : {
                "interleave_suffix" : "pe"
            },
            "adapter_file" : {
                "name" : "TruSeq2-PE.fa",
                "url"  : "http://dib-training.ucdavis.edu.s3.amazonaws.com/mRNAseq-semi-2015-03-04/TruSeq2-PE.fa"
            }
        }
    }
```

There are keys corresponding to each rule or application.
This information is used to control the behavior of the 
rules. For some simple examples of how to use these
parameters to construct rules, see the [taco-simple](https://github.com/dahak-metagenomcis/taco-simple)
workflow repository.

