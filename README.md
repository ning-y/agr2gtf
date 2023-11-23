**agr2gtf** adds gene records to GTF files, overwriting existing gene records.

### Installation

This is a command-line R script with three dependencies: argparse (the R package, not the python module), tidyverse, and rtracklayer.
These can be installed, for example, using conda:

```bash
conda create -n agr2gtf -y
conda activate agr2gtf
conda install -c conda-forge -c bioconda r-argparse r-tidyverse bioconductor-rtracklayer -y
```

### Quickstart

The command-line options are simple,

```bash
$ ./agr2gtf -h
usage: ./agr2gtf [-h] [--keep-attributes KEEP_ATTRIBUTES] input output

Add gene type records to a GTF file, overwriting previous existing gene type
records, inferring gene from gene_id of existing non-gene type records.

positional arguments:
  input                 Input GTF file
  output                Output GTF file

options:
  -h, --help            show this help message and exit
  --keep-attributes KEEP_ATTRIBUTES
                        Comma-delimited list of attributes to keep, in
                        addition to gene_id. The value of an attribute in a
                        newly constructed gene type record is the comma-
                        delimited list of unique values for that attribute for
                        all non-gene type records in the input GTF with that
                        the same gene_id. For example, the default value is
                        "gene_name,gene_type,tag".
```

The output is always an uncompressed GTF.
I haven't checked the behavior with `/dev/stdin` and `/dev/stdout` --- internally it is handled by R, so the behavior should be consistent with whatever R does with those file descriptors.

### Resources

I haven't gotten around to implementing parallel processing on this, so it might take a while.
