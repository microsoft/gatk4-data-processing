# Data pre-processing for variant discovery pipeline on Azure
This repository is an example of running the data pre-processing for variant discovery pipeline, based on [Best Practices Data Pre-processing Pipeline by Broad Institute of MIT and Harvard](https://gatk.broadinstitute.org/hc/en-us/articles/360035535912-Data-pre-processing-for-variant-discovery), on Cromwell on Azure.<br/> 

Learn more about using Azure for your Cromwell WDL workflows on our GitHub repo! - [Cromwell on Azure](https://github.com/microsoft/CromwellOnAzure).<br/>

This repository is a fork from [the original](https://github.com/gatk-workflows/gatk4-data-processing) and has all the required changes to run the WDL workflow on Cromwell on Azure.<br/>

Here, you can find the WDL file and an example inputs JSON file with links to data hosted on a public Azure Storage account. You can use the "datasettestinputs" storage account directly as a relative path, like in the inputs JSON file. 

The `processing-for-variant-discovery-gatk4.b37.trigger.json` and `processing-for-variant-discovery-gatk4.hg38.trigger.json` trigger files are ready to use. You can start the workflow on your instance of Cromwell on Azure, using [these instructions](https://github.com/microsoft/CromwellOnAzure/blob/master/docs/managing-your-workflow.md/#Start-your-workflow).

## gatk4-data-processing

### Purpose :
Workflows for processing high-throughput sequencing data for variant discovery with GATK4 and related tools.

### processing-for-variant-discovery-gatk4 :
The processing-for-variant-discovery-gatk4 WDL pipeline implements data pre-processing according to the GATK Best Practices.  

#### Requirements/expectations:
- Pair-end sequencing data in unmapped BAM (uBAM) format
- One or more read groups, one per uBAM file, all belonging to a single sample (SM)
- Input uBAM files must additionally comply with the following requirements:
  - filenames all have the same suffix (we use ".unmapped.bam")
  - files must pass validation by ValidateSamFile 
  - reads are provided in query-sorted order
  - all reads must have an RG tag
- Reference index files must be in the same directory as source (e.g. reference.fasta.fai in the same directory as reference.fasta)

#### Outputs: 
- A clean BAM file and its index, suitable for variant discovery analyses.

### Software version requirements :
- GATK 4 or later
- BWA 0.7.15-r1140
- Picard 2.16.0-SNAPSHOT
- Samtools 1.3.1 (using htslib 1.3.1)
- Python 2.7
- Cromwell version support 
  - Successfully tested on v37 
  - Does not work on versions < v23 due to output syntax
  
### Important Note :
- The provided JSON is meant to be a ready to use example JSON template of the workflow. It is the user’s responsibility to correctly set the reference and resource input variables using the [GATK Tool and Tutorial Documentations](https://software.broadinstitute.org/gatk/documentation/).
- Please visit the [User Guide](https://software.broadinstitute.org/gatk/documentation/) site for further documentation on our workflows and tools.

### LICENSING :
Copyright Broad Institute, 2019 | BSD-3
This script is released under the WDL open source code license (BSD-3) (full license text at https://github.com/openwdl/wdl/blob/master/LICENSE). Note however that the programs it calls may be subject to different licenses. Users are responsible for checking that they are authorized to run all programs before running this script.
- [GATK](https://software.broadinstitute.org/gatk/download/licensing.php)
- [BWA](http://bio-bwa.sourceforge.net/bwa.shtml#13)
- [Picard](https://broadinstitute.github.io/picard/)
- [Samtools](http://www.htslib.org/terms/)
