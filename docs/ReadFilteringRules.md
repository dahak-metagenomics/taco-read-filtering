# Workflow Rules

The taco workflow defines a number of rules. For a brief description
of each, use the `taco ls` command and pass the name of the 
`read_filtering` workflow:

```
$ taco ls read_filtering
```

**Fetch Data Rules:**

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
```

**Quality Assessment Rules:**

```
pre_trimming_quality_assessment

    Perform a pre-trimming quality check
    of the reads from the sequencer.

post_trimming_quality_assessment

    Perform a post-trimming quality check
    of the reads from the sequencer.
```

**Filter/Trim:**

```
quality_trimming

    Trim reads from the sequencer by dropping low-quality reads.
```

**Interleave:**

```
interleave_reads

    Interleave paired-end reads using khmer.
    The trim quality comes from the filename.
```

