
# Liftover from hg18 to hg19

Following QC, we have to change the genome build from hg18 to hg19 for impuation with the [University of Michican Imputation Server](https://imputationserver.sph.umich.edu/index.html#!). We know that the build is in hg18 because when looking up SNPs on the UCSC genome browser, the SNPs are only found with their identifier and respective position under hg18.

The editted [LiftMap.py](https://github.com/WheelerLab/Neuropsychiatric-Phenotypes/blob/master/SCZ-BD_Px/LiftMap.py) is available in this github repository.
```
nano newfile

##From here, we pasted the "LiftMap.py" script from the Michigan website (https://genome.ucsc.edu/cgi-bin/hgGateway) into the file.
##Make the following changes to the script:
  ##['LIFTOVERBIN']='/usr/local/bin/liftOver
  ##['CHAIN']='/home/peter/AA_nonGAIN_SCZ/liftover/hg18ToHg19.over.chain.gz'
nano LiftMap.py
##Repeat the same step from above
  ##['LIFTOVERBIN']='/usr/local/bin/liftOver
  ##['CHAIN']='/home/peter/AA_nonGAIN_SCZ/liftover/hg18ToHg19.over.chain.gz'
  
plink --bfile /home/peter/AA_nonGAIN_SCZ/QCSteps/QCStep2/QCStep2 --recode --out /home/peter/AA_nonGAIN_SCZ/liftover/newfile

python LiftMap.py -m newfile.map -p newfile.ped -o new

plink --file new --make-bed --out hg19_forImputationPrep
```
From here, proceed to prepping the data for Imputation