# Machine learning approach based on single nuclear polymorphisms

## big data

### with "big data" 5 phenotype parameters are picked and the phenotype of the users is classified and the results shown in a final dataframe 

-raw data needs to be imported from openSNP, which is a public repository from 23andMe, deCODEme and FamilyTreeDNA (phenotypes_202211021922)
-raw data consists of 6463 rows × 681 columns, most of the cells obtain dash values 
-phenotypes (=column names) are listed and non-dash values are counted for each phenotype
-phenotypes with the most non-dash values are listed and five interesting phenotypes for further analysis picked 

1.Lactose intolerance
<br>2.Nicotine dependence
<br>3.Blood type
<br>4.Aspirin Allergy
<br>5.Haplogroup

-phenotype charactization for 1. - 5. 
<br>-> users with incomplete report are discarded
<br>-> rest of users for <b>binary</b> classification:

1.Lactose tolerant = 0
    <br>Lactose intolerant = 1
<br>2.Nicotine independent = 0
    <br>Nicotine dependent = 1
<br>4.no Aspirin Allergy = 0
    <br>Aspirin Allergy = 1

or <b>quaternary</b> classification:

3.Bloodtype A = 1
    <br>Bloodtype B = 2
    <br>Bloodtype O = 3
    <br>Bloodtype AB = 4
<br>5.Haplogroup L = 1
    <br>Haplogroup M = 2
    <br>Haplogroup N = 3
    <br>Haplogroup R = 4

-after charactization create dataframe with userfilename ( omly 23andMe files are included) and according classification of phenotype
<br>-dataframes: final_lactose_intolerance_df.csv, final_nicotine_dependence_df.csv, final_bloodtype_df.csv, final_aspirin_allergy.csv, final_mtDNA_Haplogroup_df.csv  


## generating preprocessed phenotypes

### with "generating preprocessed phenotypes" users are selected, the data cleaned and rsids selected, in order to recieve a final dataframe which shows the username, rsids and the according genotype

#### this is done for 1., 2. and 4. (3. and 5. had to be discarded due to too much and too less data, respectively)

-import dataframe and change names in column "name"
<br>-with the changed name the according files can be acessed in the directory
<br>-header of 23andMe files need to be cleared and therefore lines with "#" discarded
<br>-rsid, position and genotype of a file is saved as parquet file
<br>-further cleaning: internal IDs (start with i) are being discarded, as well as an incomplete genotype ( "--" or genotype<2)

<br>-once cleaned, all rsids are counted and a .csv file with the counted rsids is created
<br>-list how often a rsid occures in all of the patients together
<br>-take the most common rsids (common in 97% of the patients)
<br>-and take users, which contain all of the common rsids to 100% (this is done, so there will be no gap when it comes to creating the final dataframe)
<br>-create the final dataframe which lists the rsids as column values, the usernames as row values and the according genotype in each cell

1.Lactose_Intolerance_Final_DF.csv
<br>2.Nicotine_Dependence_Final_DF.csv
<br>4.Aspirin_Allergy_Final_DF.csv


## genotype encoding

genotype encoding is based on "Machine learning approach to single nucleotide polymorphism-based asthma prediction" by Gaudillo J. et. al.
-> github:  https://github.com/jdgaudillo/SNP-ML

Outfiles:   lactose_intolerance_encoded_snp.csv
            <br>nicotine_dependence_encoded_snp.csv
            <br>aspirin_allergy_encoded_snp.csv
<br>The outfiles contain n rows with n_patients and x columns with x_rsids, for every rsid genotype encoding was implemented wherein homozygous, <br>heterozygous and variant homozygous rsids were represented by 1, 2, 3, respectively.

## machine learning

machine learning is based on "Machine learning approach to single nucleotide polymorphism-based asthma prediction" by Gaudillo J. et. al.
-> github:  https://github.com/jdgaudillo/SNP-ML

RF-SVM and RF-KNN models were generated and accuracy, sensitivity and specificity calculated


## sampling

Hybrid Sampling, Oversampling and Undersampling were applied for the RF-SVM and RF-KNN models 
<br>The performance metrics used to evaluate the models were accuracy, sensitivity and specificity
