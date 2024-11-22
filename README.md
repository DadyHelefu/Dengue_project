# Dengue_project
## Create the directories

```
mkdir -p Project_dengue/Data/Raw_data Project_dengue/Data/Processed_data Project_dengue/Codes
```

##Download and put in the appropriate directory then unzip the file
##code
'''mv dengue.zip ~/Project_dengue/Data/Raw_data'''
'''unzip dengue.zip'''

##How many files in a zip file
##code
'''ls *.fasta | wc -l'''
 
##output 
>5

##How many lines in each fasta file
##code
```
wc -l *.fasta
```

##output
|No of lines | sequences             |
|------------|-----------------------|
|   42       |  dengueseq1.fasta     |
|  115       |  dengueseq2.fasta     |
|   94       |  dengueseq3.fasta     |
|  113       |  dengueseq4.fasta     |
|  157       |  dengueseq5.fasta     |
|  521       |     total             |

##Merge fasta file to merged.fasta file
##code
'''cat *.fasta > dengue_merged.fasta'''

##How many headers does the the merged.fasta have
##code
'''grep '^>' dengue_merged.fasta | wc -l''' 

##How many sequences does the merged.fasta have
##code
'''grep -v '^>' dengue_merged.fasta | wc -c'''

##Extract the headers and put them in a new file called dengue_headers.txt
##code
'''grep '^>' dengue_merged.fasta > dengue_headers.txt'''

##output
|Unique ID   | Name of viruses           | genome          |
|------------|---------------------------|-----------------|
|NC_001478.1 | Digitaria streak virus    | complete genome |
|NC_001479.1 | Encephalomyocarditis virus| complete genome |
|NC_001480.1 | Eggplant mosaic virus     | complete genome |
|NC_001481.2 | Feline calicivirus        | complete genome |
|NC_001477.1 | Dengue virus 1            | complete genome |

##Extract only the names of viruses and create the file called viruses.txt
##code
'''awk '{print $2 $3 $4}' dengue_headers.txt | sed 's/complete//g''''

##output
|Name of viruses             |
|----------------------------|
|Digitaria streak virus      |
|Encephalomyocarditis virus  |
|Eggplant mosaic virus       |
|Feline calicivirus          |
|Dengue virus 1              |

##Do this for the unique identifier
##code
'''awk '{print $1}' dengue_headers.txt'''

##output
|Unique ID    |
|-------------|
|NC_001478.1  |
|NC_001479.1  |
|NC_001480.1  |
|NC_001481.2  |
|NC_001477.1  |

##Create a file for sequences and name it dengue_seq.txt and replace with small letters
##code
'''grep -v '^>' dengue_merged.fasta | tr '[:upper:] [:lower:]' > dengue_seq.txt'''
