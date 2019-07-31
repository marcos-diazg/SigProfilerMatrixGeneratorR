[![Docs](https://img.shields.io/badge/docs-latest-blue.svg)](https://osf.io/s93d5/wiki/home/) [![License](https://img.shields.io/badge/License-BSD\%202--Clause-orange.svg)](https://opensource.org/licenses/BSD-2-Clause) [![Build Status](https://travis-ci.com/AlexandrovLab/SigProfilerMatrixGenerator.svg?branch=master)](https://travis-ci.com/AlexandrovLab/SigProfilerMatrixGenerator)

# SigProfilerMatrixGeneratorR
An R wrapper for running the SigProfilerMatrixGenerator (https://osf.io/s93d5/wiki/home/) framework.
**INTRODUCTION**


**PREREQUISITES**
devtools 
```
install.packages("devtools")
```

**QUICK START GUIDE**

This section will guide you through the minimum steps required to create mutational matrices:
1. First, install the python package using pip. The R wrapper still requires the python package:
```
                          pip install SigProfilerMatrixGenerator
```
2. Install SigProfilerMatrixGeneratorR using devtools:
```
install_github("AlexandrovLab/SigProfilerMatrixGeneratorR")
```
3. Load the package in an R session and install your desired reference genome as follows (available reference genomes are: GRCh37, GRCh38, mm9, and mm10):
```
$ R
>> library("SigProfilerMatrixGeneratorR")
>> install('GRCh37', rsync=False, bash=True)
```
    This will install the human 37 assembly as a reference genome.

4. Place your vcf files in your desired output folder. It is recommended that you name this folder based on your project's name
5. From within an R session, you can now generate the matrices as follows:
```
$ R
>> library("SigProfilerMatrixGeneratorR")
>> matrices <- SigProfilerMatrixGeneratorR("BRCA", "GRCh37", "/Users/ebergstr/Desktop/BRCA/", plot=T, exome=False, bed_file=None, chrom_based=False, tsb_stat=False, seqInfo=False, cushion=100)
```
  The layout of the required parameters are as follows:
  
      SigProfilerMatrixGeneratorFunc(project, reference_genome, path_to_input_files)
      
  where project, reference_genome, and path_to_input_files must be strings (surrounded by quotation marks, ex: "test"). Optional parameters include:
      
      exome=False:       [boolean] Downsamples mutational matrices to the exome regions of the genome
      bed_file=None      [string path to bed_file] Downsamples mutational matrices to custom regions of the genome. Requires the full path to the BED file. 
      chrom_based=False  [boolean] Outputs chromosome-based matrices
      plot=False         [boolean] Integrates with SigProfilerPlotting to output all available visualizations for each matrix. 
      tsb_stat=False     [boolean] Outputs the results of a transcriptional strand bias test for the respective matrices. 
      seqInfo=False      [boolean] Ouputs original mutations into a text file that contains the SigProfilerMatrixGenerator classificaiton for each mutation. 
      cushion=100	[integer] Adds an Xbp cushion to the exome/bed_file ranges for downsampling the mutations.
  


**INPUT FILE FORMAT**

This tool currently supports maf, vcf, simple text file, and ICGC formats. The user must provide variant data adhering to one of these four formats. If the user’s files are in vcf format, each sample must be saved as a separate files. 


**Output File Structure**

The output structure is divided into three folders: input, output, and logs. The input folder contains copies of the user-provided input files. The outputfolder contains
a DBS, SBS, ID, and TSB folder (there will also be a plots folder if this parameter is chosen). The matrices are saved into the appropriate folders. The logs folder contains the error and log files for the submitted job.


**SUPPORTED GENOMES**

This tool currently supports the following genomes:

GRCh38.p12 [GRCh38] (Genome Reference Consortium Human Reference 37), INSDC
Assembly GCA_000001405.27, Dec 2013. Released July 2014. Last updated January 2018. This genome was downloaded from ENSEMBL database version 93.38.

GRCh37.p13 [GRCh37] (Genome Reference Consortium Human Reference 37), INSDC
Assembly GCA_000001405.14, Feb 2009. Released April 2011. Last updated September 2013. This genome was downloaded from ENSEMBL database version 93.37. 

GRCm38.p6 [mm10] (Genome Reference Consortium Mouse Reference 38), INDSDC
Assembly GCA_000001635.8, Jan 2012. Released July 2012. Last updated March 2018. This genome was downloaded from ENSEMBL database version 93.38. 

GRCm37 [mm9] (Release 67, NCBIM37), INDSDC Assembly GCA_000001635.18.
Released Jan 2011. Last updated March 2012. This genome was downloaded from ENSEMBL database version release 67.

rn6 (Rnor_6.0) INSDC Assembly GCA_000001895.4, Jul 2014. Released Jun 2015. Last updated Jan 2017. 
This genome was downloaded from ENSEMBL database version 96.6.

**LOG FILES**

All errors and progress checkpoints are saved into *sigProfilerMatrixGenerator_[project]_[genome].err* and *sigProfilerMatrixGenerator_[project]_[genome].out*, respectively. 
For all errors, please email the error and progress log files to the primary contact under CONTACT INFORMATION.

**CITATION**

E.N. Bergstrom, M.N. Huang, U. Mahto, M. Barnes, M.R. Stratton, S.G. Rozen, and L.B. Alexandrov (2019) SigProfilerMatrixGenerator: a tool for visualizing and exploring patterns of small mutational events. https://www.biorxiv.org/content/10.1101/653097v1


**COPYRIGHT**

Copyright (c) 2019, Erik Bergstrom [Alexandrov Lab] All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE. 

**CONTACT INFORMATION**

Please address any queries or bug reports to Erik Bergstrom at ebergstr@eng.ucsd.edu
