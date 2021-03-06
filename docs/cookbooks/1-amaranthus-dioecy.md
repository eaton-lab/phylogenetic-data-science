

## Workflow diagram

```mermaid
%%{init: {'theme': 'dark', "flowchart" : { "curve" : "basis" } } }%%
graph LR
	0(kinit)
	1(ktrim)
	A(kcount)
	B(kfilter)
	C(kextract)
	D(kassemble)
	0 --> 1 --> A --> B --> C --> D

linkStyle default stroke-width:2px,fill:none,stroke:grey;   	
```

## Study description

Here we re-implement the study by Neves et al. to detect a male linked 
genomic region involved in sex determination in the dioecious plant species 
*Amaranthus palmeri*. This study uses pool-seq to sequence four populations 
composing male and female plants from two geographically distinct populations.

<cite>Cátia José Neves, Maor Matzrafi, Meik Thiele, Anne Lorant, Mohsen B 
	Mesgaran, Markus G Stetter, Male Linked Genomic Region Determines Sex in 
	Dioecious Amaranthus palmeri, Journal of Heredity, Volume 111, Issue 7, 
	October 2020, Pages 606–612, 
	<a href=https://doi.org/10.1093/jhered/esaa047>https://doi.org/10.1093/jhered/esaa047</a></cite>


## Fetch fastq data
If you wish to follow along you can dowload the data from ERA with the
instructions below: 

- ERR4161581 (*California_male_pool*),
- ERR4161582 (*California_female_pool*),
- ERR4161583 (*Kansas_male_pool*),
- ERR4161584 (*Kansas_female_pool*)

??? abstract "Download fastq data using sra-tools"

    Download the latest version of the sratools from [https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit](https://github.com/ncbi/sra-tools/wiki/01.-
    Downloading-SRA-Toolkit) by selecting the compiled binaries that are 
    appropriate for your system (e.g., Linux or MacOSX). (I really do 
    recommend that you use the latest version since this software is updated
    frequently and does not maintain compatibility with older versions.)
    Run the command below to download the fastq data for this study 
    into a new directory. The total file size will be about 140Gb.

    ```bash
    # make a directory to store the raw fastq data files
    mkdir -p ./fastq-data

    # download files to the specified fastq directory
    for run in ERR4161581 ERR4161582 ERR4161583 ERR4161584; do
        fasterq-dump --progress --outdir ./fastq-data --temp . $run;
    done
    ```


## Kmerkit analysis
### Initialize a new project
Start a new project by entering a name and working directory to `init`, 
representing the filename prefix and location where all files will be saved.
The directory will be created if it doesn't yet exist. Multiple input fastq 
files can be entered as arguments, or multiple can be selected using a 
regular expression selector like below. Paired reads are automatically 
detected based on name matching. Sample names are automatically extracted 
from file names. Paired file names should be identical up until some 
delimiter (e.g., `_`), after which the tail is trimmed (`_R1.fastq.gz`). 
You can set the delimiter explicitly.

```bash
kmerkit init --name dioecy --workdir /tmp --delim "_" ./fastq-data/*.gz 
```

This step creates a project JSON file, which will contain fully reproducible 
information about each step in a kmerkit analysis. It will be updated 
upon each kmerkit module that is run. This file can be read directly, 
or, you can view it easily by calling `kmerkit stats`, like below.
??? tip "kmerkit stats output"

	```bash
	kmerkit stats --json /tmp/dioecy.json
	```

	```json
	Project JSON data:
	{
	    "name": "Neves",
	    "workdir": "/pinky/deren/palmeri",
	    "versions": {
	        "kmerkit": "0.0.12",
	        "kmc": "3.1.1",
	        "gemma": "0.9.83",
	        "sklearn": "0.24.1"
	    },
	    "kinit": {
	        "data": {
	            "ERR4161581": [
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161581_1.fastq.gz",
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161581_2.fastq.gz"
	            ],
	            "ERR4161582": [
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161582_1.fastq.gz",
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161582_2.fastq.gz"
	            ],
	            "ERR4161583": [
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161583_1.fastq.gz",
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161583_2.fastq.gz"
	            ],
	            "ERR4161584": [
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161584_1.fastq.gz",
	                "/pinky/DATASTORE/Amaranthus_palmeri_PRJEB38372/ERR4161584_2.fastq.gz"
	            ]
	        },
	        "commands": {}
	    },
	}
	```

### Read trimming (optional)
You *can* perform read trimming on your own before using kmerkit, but we also
provide the option to trim, filter, or subsample your reads within kmerkit
by calling the program `fastp`. Trimmed read files are written to the workdir, 
and subsequent modules (e.g., `count` and `extract`) will 
use the trimmed reads instead of the raw reads (both sets of filepaths can 
be viewed in the project JSON file).

```bash
kmerkit trim -j /tmp/dioecy.json --workers 4
```

Like before we can access the results from the JSON file by calling the
`stats` module. In this case I also provide a module name (trim) to 
select only results for this module. 

??? tip "kmerkit stats output"
	```bash
	kmerkit stats -j /tmp/dioecy.json trim
	```

	```json
	...
	```

### Count kmers
Kmers are counted for each sample using 
[kmc](https://github.com/refresh-bio/KMC) at the specified kmer-size. 
Kmers occurring above or below the specified thresholds will be excluded. 
See the `kmerkit count` page for details on parallelization and memory
consumption for optimizing the speed of this step, which is usually 
the most time consuming. 

```bash
kmerkit count -j /tmp/dioecy.json --kmer-size 35 --min-depth 5 --workers 4 
```

??? tip "kmerkit stats output"

	```bash
	kmerkit stats -j /tmp/dioecy.json count
	```

	```console
	...
	```

### Filter kmers
Apply filters to identify target kmers that are enriched in one group of 
samples versus another. In this case, we aim to identify male-specific kmers,
meaning those that are present in males but not females. This can be done 
by setting a high `min-map` for group 1 (kmers must be present in group 1) and 
setting a low `max-map` for group 0 (kmers cannot be present in group 0). We
must also assign samples to groups 0 or 1. For studies with many samples this
is most easily done by entering a CSV file (see the kfilter docs section). Here
because there are few samples I use the simpler option of entering the sample
names directly using the `-0` and `-1` options to assign to their respective
groups. The min_map and max_map entries each take two ordered values, assigned
to group 0 and 1, respectively.

```bash
kmerkit filter \
	--json /tmp/dioecy.json \
	-1 'ERR4161581' -1 'ERR4161583' \
	-0 'ERR4161582' -0 'ERR4161584' \
	--min_map 0.0 0.5 \
	--max_map 0.0 1.0  
```

??? tip "kmerkit filter results"

	```bash
	kmerkit stats -j /tmp/dioecy.json filter
	```

	```console
	...
	```

### Extract reads 
Now that we've identified a set of target kmers we will extract reads from 
fastq data files that contain these kmers. This is expected to pull out reads
mapping to male-specific regions of the <i>A. palmeri</i> genome. Here you 
can enter new fastq files to extract data from, or enter the names of samples
already in the project database, which will use the (trimmed) fastq data files
referenced in the JSON file. Here I don't enter any sample names, which 
defaults to performing extractions on all 4 samples in the database (we expect
to not recover any reads for the two female pop samples).

```bash
kmerkit extract --json /tmp/dioecy.json --min-kmers-per-read 5
```

??? tip "kmerkit stats output"
	```console
	...
	```


### Assemble contigs 
From the extracted reads created in the last step, we can now assemble contigs
for each sample (or for all samples pooled together) using the `assemble` 
module. Here we use the default assembler, spades. This creates a number of
output files in the workdir, which can be summarized with `stats`. 

```bash
kmerkit assemble --json /tmp/dioecy.json ...
```

The main result of Neves et al. was the identification of an approximately
2Mb assembled contig representing a large contiguous male-specific genomic
region. The summary here shows the ...

??? tip "kmerkit stats output"
	```console
	...
	```

## Reproducibility
In addition to your scripts that can be used to reproduce your analysis, the 
JSON project file contains a full record of the samples, parameters, and the
order of analysis steps that make up your analysis.

??? success "kmerkit project JSON file"
	```console
	...
	```


## TODO: Post-pipeline analysis API
The `kmerkit` Python API can be used to perform post-pipeline analyses 
in a jupyter notebook. Here we create a plot of 

```python
import kmerkit

project = kmerkit.load_json("/tmp/dioecy.json")
...
```

