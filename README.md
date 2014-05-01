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
*SVsim* can be downloaded from the *releases* tab, or can be manually downloaded from the command line as follows:

~~~~~~~~~~~~~~~~~~
git clone git://github.com/GregoryFaust/SVsim.git
cp SVsim/SVsim /usr/local/bin/
~~~~~~~~~~~~~~~~~~

##Usage
*SVsim* requires input of a reference genome as an indexed fasta file (for example using **samtools faidx**).
The Structural Variants to create are specified in an input file using a simple declarative language described below.  Output includes a [fasta](http://en.wikipedia.org/wiki/FASTA_format) file in which the created SVs are embedded, a [bedpe](http://bedtools.readthedocs.org/en/latest/content/general-usage.html) file that specify the breakpoint coordinates in the input genome, and a *event* file that gives additional information about the SV events that were created.



