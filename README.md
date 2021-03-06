## Overview ##
Accel-align is a fast alignment tool implemented in C++ programming language.

## Get started ##

### Docker Container ###
You can now pull a preconfigured docker container to get the binaries:
```
docker run -it rajaappuswamy/accel-align
```

### Pre-requirement ###
If you prefer to do a non-docker install, download and install Intel TBB 
- source: https://github.com/01org/tbb/releases/tag/2019_U5
- libtbb-dev package

### Build index ###
It's mandatory to build the index before alignment. 
Options:
```
-l INT the length of k-mers [32]
-m low memory [use if system memory < 16GB]
```

Example:
```
path-to-accel-align/accindex -m path-to-ref/ref.fna
```
It will generate the index along side the reference genome as `path-to-ref/ref.fna.hash`.

### Align ###
When the alignment is trigged, the index will be loaded in memory automatically.

Options:
```
-t INT number of threads to use[1]
-l INT length of seed [32].
-o name of output file to use
-x alignment-free mapping (base-to-base align by default)
```

#### Pair-end alignment #### 

``` 
path-to-accel-align/accalign options ref.fna read1.fastq read2.fastq
```

Example:
``` 
path-to-accel-align/accalign -l 32 -t 4 -o output-path/out.sam \
path-to-ref/ref.fna input-path/read1.fastq input-path/read2.fastq
``` 

#### Single-end alignment #### 

``` 
path-to-accel-align/accalign options ref.fna read.fastq
```

Example:
``` 
path-to-accel-align/accalign -l 32 -t 4 -o output-path/out.sam \
path-to-ref/ref.fna input-path/read.fastq
``` 

#### Alignment-free mode #### 
Accel-Align does base-to-base alignment by default. However, Accel-Align supports extension-free mapping mode where the position is reported without the CIGAR string.
 `-x` option will enable the extension-free mode.

Example:
``` 
path-to-accel-align/accalign -l 32 -t 4 -x -o output-path/out.sam \
path-to-ref/ref.fna input-path/read.fastq
``` 
  
