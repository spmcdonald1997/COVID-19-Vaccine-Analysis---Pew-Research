# COVID-19-Vaccine-Analysis---Pew-Research
Analyses of data from Pew Research Report on COVID-19 Vaccine Survey, using Numpy, Pandas, and Matplotlib
# Analyses from Pew Research COVID -19 Vaccine Study

The following are replications and additional analyses from a Pew Research Report and DataSet found here: 

https://www.pewresearch.org/science/2021/03/05/growing-share-of-americans-say-they-plan-to-get-a-covid-19-vaccine-or-already-have/

### Initial Install:

pyreadstat

numpy

Pandas

Matplotlib

pip install pyreadstat

import numpy as np

import pandas as pd

import matplotlib as mpl

import matplotlib.pyplot as plt

#import data from Pew files

pewdata = pd.read_spss('ATP W83.sav')

#initial explore of the data

#pewdata.head()

#view all columns in the data set

#for col in pewdata.columns:
    #print (col)

## View of Economic Impact if Majority of Americans Vaccinated Against COVID-19  

In the Pew report, the following question was asked: 

If a large majority of Americans get a vaccine for COVID-19, what do you think the impact would be on the U.S. economy? Do you think it would...

1 Help the economy a lot

2 Help the economy a little

3 Not make much of a difference

This is denoted by the variable VACCECON in the codebook, and VACCECON_W83 in the pewdata dataset

#view of impact on the economy if majority americans vaccinated: VACCECON_W83

econimpact = pewdata.VACCECON_W83.value_counts()
econimpact

#normalizing and rounding these numbers 
econimpact = pewdata.VACCECON_W83.value_counts(normalize = True).round(2)
econimpact

# pie chart using pandas series plot()

pewdata.VACCECON_W83.value_counts().plot(kind='pie', title = 'Respondent View: Economic Impact if Majority of Americans Vaccinated',colors = ["cornflowerblue", "lavender", "lightblue", "wheat"], autopct = '%1.1f%%' , labeldistance=None).legend(loc = 'lower right')




pewdata.SC1_W83.value_counts(normalize = True).round(2)

## Relationship Between View of COVID-19 Vaccine Impact on Economy and Effect of Science on Society

In the same pew report as above, the following question was asked: 
Overall, would you say science has had a mostly positive effect on our society or a mostly negative effect on our society?

1 Mostly positive

2 Mostly negative

3 Equal positive and negative effects

This is denoted by the variable SC1 in the codebook, SC1_W83 in the pewdata dataset

#rearrange the axes from science positive to science negative, help economy a lot to not make a difference

pd.crosstab(pewdata.SC1_W83, pewdata.VACCECON_W83, normalize = 'index').round(2).reindex(['Mostly positive', 'Equal positive and negative effects','Mostly negative', 'Refused'])[['Help the economy a lot', 'Help the economy a little', 'Not make much of a difference', 'Refused']]


