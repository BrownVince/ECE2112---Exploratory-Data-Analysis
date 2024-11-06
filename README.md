<div align="center">

# Hi! <img src="https://github.com/user-attachments/assets/d21e6cd6-76a9-4934-8910-809aa4815251" alt="Wave" width="30"/>, I'm Vince Joriz E. Supsup  
From 2ECE-D, and this is my Exploratory Data Analysis on Spotify 2023 Dataset in ECE2112  
Submitted: 

</div>

# Version History
V1.0 (11-04-24) - Initial Editing of Github Repository  
V1.1 (11-05-24) - Editing of Documentation on Github Readme File Part 1  
V1.2 (11-06-24) - Editing of Documentation on Github Readme File Part 2

# Software(s) Used
<img src="https://github.com/user-attachments/assets/32ea11b3-b4e5-4efa-a673-ce2b102ab4b5" alt="Jupyter Logo" width="80"/> <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png" alt="GitHub Logo" width="100"/>

# ECE2112 - Exploratory Data Analysis
Python - Exploratory Data Analysis on Spotify 2023 Dataset

* Import necessary libraries needed for analyzing the dataset such as pandas and seaborn or matplot then load the given data set
```
import pandas as pd
import seaborn as sns

df = pd.read_csv('spotify2023.csv')
```
When I first tried to load the dataset an error appeared, so I tried to change the file type of the dataset then it worked just fine  

For this project, I used **seaborn** as my primary data visualization tool

* When creating the summary statistics, set the parameters for the describe function to include='all' in order to provide also summary statistics for the string (object) data type columns
```
dfdesc = df.describe(include='all')
```
But I noticed that some columns that are supposed to be an integer type column, are in string (object) data type columns because some of their data are appearing as NaN such as the mean and std  
**Insert Picture**  

So I tried to convert the said columns into an integer type column, but an error appeared that it can't convert to an integer data type  
**Insert Picture**  

So I looked what went wrong, then noticed that in the site where I downloaded the file, the data type of the column 'streams' are in string  
**Insert Picture**  

So I opened the discussion tab of the said dateset in the kaggle website, then I saw someone said that in the streams column, there is one corrupted value, where the value is a text instead of a number  
**Insert 2 Picture**  

I then used the function pd.to_numeric in order to remove the corrupted value and turn the 'streams' column into a numerical data type  
```
df['streams'] = pd.to_numeric(df['streams'], errors='coerce')
```
**Insert Picture**  

But when I tried to convert the other columns that are in string (object) data type, another error occured in columns 'in_deezer_playlists' and 'in_shazam_charts' since it's numerical values have commas  
**Insert Picture**  

So I used the .replace() function to remove the commas then converted the columns into a numerical data type
```
#Removing first the commas in in_deezer_playlists column then converting it to a numerical column
df['in_deezer_playlists'] = df['in_deezer_playlists'].str.replace(',', '')
df['in_deezer_playlists'] = pd.to_numeric(df['in_deezer_playlists'], errors='coerce')

#Removing first the commas in in_shazam_charts column then converting it to a numerical column
df['in_shazam_charts'] = df['in_shazam_charts'].str.replace(',', '')
df['in_shazam_charts'] = pd.to_numeric(df['in_shazam_charts'], errors='coerce')
```
*Note that when using the pd.to_numeric() function and set the parameters of error to 'coerce', python will convert the columns into numerical data and remove string entries, replacing it with missing values (NaN), making the entire column into a float data type, since float can handle NaN values. But if the column is complete with no missing values, it will convert it into an integer data type.*

# Overview of Dataset
* In the given dataset, there are 953 rows and 24 columns
**Insert Picture**

* The data types of each column are as follows. Note that object data type are string (object) data types. Also, the 'streams' and 'in_shazam_charts' are in float since both contain missing values
**Insert Picture**

* There are 1 missing value in 'streams', 50 missing values in 'in_shazam_charts', and 95 missing values in 'key'. *Note that the 1 missing value in streams is the removed corrupted value*
**Insert Picture**

# Basic Descriptive Statistics
