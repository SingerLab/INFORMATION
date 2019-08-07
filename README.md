# INFORMATION

Please start adding useful information on resources for Singer Lab Data Analysis

- Project task management tools at : https://github.com/orgs/SingerLab/projects/1

- Singer Work on JUNO:
    
    working directory ->```/work/singer```
    
    Genomes annotations and resources: ```juno:/work/singer/genomes/```
    
        Genome indices, gene, miRNA, repetitive element, and variant annotations are available for the human and mouse genome. Additional genome indices are available for other species.  The directory also contains sequences and indices for TCGA decoy genome, TCGA virus sequences, NCBI human virus sequences, and all NCBI viral sequences.  Lastly, we have sequences and indices common contamination artifacts e.g. adapters and PhiX, to perform an extensive sequencing QC.
    
    
    User specific directories -> ```juno:/work/singer/gularter/``` ```juno:/work/singer/soccin/```
    

- Singer Lab Genomic Data Archive on LUNA at:

    InvC/Singer -> ```luna:/ifs/assets/socci/Data/Singer/```

- Singer Lab work directories and databases
    SingerS -> ```juno:/work/singer/```

    CRDB -> ```luna:/home/socci/Work/Users/SingerS/CRDB.LIMS/dumps```

        - latest version: 2018.02.12
            - FullDataExport_CRDB_180212__MinimalInfo.csv
            - FullDataExport_CRDB_180212__MinimalInfo.rda

The critical columns in the CRDB file are:

|column| description|
|------|------------|
|BIO_ID|SampleID|
|MOLD_HISTOLOGY_DSCRP|Sarcome Subtype|
|FQN|Name of assay (array:mRNA:Affy:U133A, ...)|
|EXCLUDED|Exclude sample (if column 'Y')|
|FILE_NAME|Assay filename|
|LOCATION|Location of assay file in investigator archive|


    
    
## things to note:

- Some samples were repeated and the original was deprecated, excluded, or were repeated on a higher resolution assay (244k vs 1 M). Make sure not to double count, and to use the highest reslution array (unless you are making a cohort of all one assay type). 

- Avoid working with excluded samples, e.g. ```crdb[!EXCLUDE == "Y" & FQN=="DEPRECATED", ]```

- The BIO-ID which is the core ID was sometimes incorrectly entered by someone and so the ID that you often find in file names is not correct. 

- *MOST IMPORTANT*, you need to use TYPE to get the sample type because although it appears you can get the sample type from the FILENAME or BIOID this does not work 100% of the time.  Similarly, use MOLD_HISTOLOGY_DSCRP for the sarcoma subtype.

