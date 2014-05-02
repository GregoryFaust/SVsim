SVsim
=====

Written by Greg Faust (gf4ea@virginia.edu)  
[Ira Hall Lab, University of Virginia](http://faculty.virginia.edu/irahall/)

**Current version:** 0.1.1

SVsim is written in Python 2.6+, and requires [pysam](https://code.google.com/p/pysam/).  It has been tested on both Linux and OSX. It has not been tested with Python versions 3.0 or higher.

##Summary
A Structural Variant (SV) is any genomic insertion, deletion, duplication, inversion or translocation of 50 bases or more in length.

*SVsim* is a tool to simulate Structural Variant calls in order to generate sythetic benchmark data useful to test/evaluate SV calling pipelines.  For example, it has been used to generate test datasets for both [YAHA](http://faculty.virginia.edu/irahall/yaha/) and [LUMPY](https://github.com/arq5x/lumpy-sv).

##Installation
*SVsim* is a self contained Python source file and requires no special installation beyond **python** and **pysam**.
However, we strongy suggest that you have [bedtools](https://github.com/arq5x/bedtools2) and [samtools](http://samtools.sourceforge.net/) installed.
In addition, it is common to use [wgsim](https://github.com/lh3/wgsim) to simulate sequencing reads from the **fasta** file that *SVsim* produces.

*SVsim* can be downloaded from the *releases* tab, or can be manually downloaded from the command line as follows:

~~~~~~~~~~~~~~~~~~
git clone git://github.com/GregoryFaust/SVsim.git
cp SVsim/SVsim /usr/local/bin/
~~~~~~~~~~~~~~~~~~

##Usage
*SVsim* requires input of a reference genome as an indexed fasta file (for example using **samtools faidx**).
The Structural Variants to create are specified in an input file using a simple declarative language described below.  Output includes a [fasta](http://en.wikipedia.org/wiki/FASTA_format) file in which the created SVs are embedded, a [bedpe](http://bedtools.readthedocs.org/en/latest/content/general-usage.html) file that specify the breakpoint coordinates in the input genome, and a *event* file that gives additional information about the SV events that were created.

Here is the call format:
```
SVsim -i commands.sim -r genome.fasta -o output.file.root [options]
```
which will output the following files:
```
output.file.root.bedpe
output.file.root.event
output.file.root.fasta
```

---
**Terminology:**  
In what follows, we will use the following terms:
* Source Region:   The genomic region from which an inserted DNA sequence is taken.
* Target Location: The genomic point at which an SV is created.  It falls between two bases.
* Original Offset: Location coordinates relative to the original genome.
* Mutated Offset:  Location coordinates relative to the mutated genome.

---
**Major Modes:**  
SVsim operates in two major modes that largely control what is output in the **fasta** file, but there are also mode specific options that further control how SVs are simulated.
The default mode is called *contig* mode.
In this mode, the **fasta** file will contain only small regions of the genome surrounding the target location or breakpoints of the SVs.
The other major moade is called *Whole Genome Mode (WGM)*.
In this mode, the entire mutated genome is output to the **fasta** file.
In *contig* mode, each simulated SV will be independent of each other, while in *WGM* the simulated SVs will not be independent if they fall near each other in the mutated genome.
The **-W** option specifies that *WGM* will be used.








