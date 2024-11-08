<div align="center">

# Hi! <img src="https://github.com/user-attachments/assets/d21e6cd6-76a9-4934-8910-809aa4815251" alt="Wave" width="30"/>, I'm Vince Joriz E. Supsup  
From 2ECE-D, and this is my Exploratory Data Analysis on Spotify 2023 Dataset in ECE2112  
Submitted: 

</div>

# Version History
V1.0 (11-04-24) - Initial Editing of Github Repository  
V1.1 (11-05-24) - Editing of Documentation on Github Readme File Part 1  
V1.2 (11-06-24) - Editing of Documentation on Github Readme File Part 2  
V1.3 (11-07-24) - Editing of Documentation on Github Readme File Part 3  
V2.0 (11-08-24) - Editing of Documentation on Github Readme File Part 4  
V2.1 (11-09-24) - Finalization, Proofreading and Revision    

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

* When creating the summary statistics, set the parameters for the describe function to include='all' in order to provide also summary statistics for the string (object) data type columns
```
dfdesc = df.describe(include='all')
```
- But I noticed that some columns that are supposed to be an integer type column, are in string (object) data type columns because some of their data are appearing as NaN such as the mean and std   

- So I tried to convert the said columns into an integer type column, but an error appeared that it can't convert to an integer data type  
<img src="https://github.com/user-attachments/assets/0cb31de6-6dbb-4976-864f-ad76c48aadc1" alt="interror" width="500"/>  


- So I looked what went wrong, then noticed that in the site where I downloaded the file, the data type of the column 'streams' are in string. So I opened the discussion tab of the said dateset in the kaggle website, then I saw someone said that in the streams column, there is one corrupted value, where the value is a text instead of a number  
<img src="https://github.com/user-attachments/assets/9d169bb0-50c5-4b5a-a6bf-01467a25ad87" alt="corruptvalue" width="600"/>  


So I searched it in the dataset, and here it is :(  
<img src="https://github.com/user-attachments/assets/081014a1-2cbb-4fe8-ba2d-e25166ae28f5" alt="corruptvalue2" width="600"/>


- I then used the function pd.to_numeric in order to remove the corrupted value and turn the 'streams' column into a numerical data type  
```
df['streams'] = pd.to_numeric(df['streams'], errors='coerce')
```

- But when I tried to convert the other columns that are in string (object) data type, another error occured in columns 'in_deezer_playlists' and 'in_shazam_charts' since it's numerical values have commas  
<img src="https://github.com/user-attachments/assets/777a5d01-aebb-4cee-9a4a-ceefd73135cc" alt="commaerror" width="600"/>    

- So I used the .replace() function to remove the commas then converted the columns into a numerical data type
```
#Removing first the commas in in_deezer_playlists column then converting it to a numerical column
df['in_deezer_playlists'] = df['in_deezer_playlists'].str.replace(',', '')
df['in_deezer_playlists'] = pd.to_numeric(df['in_deezer_playlists'], errors='coerce')

#Removing first the commas in in_shazam_charts column then converting it to a numerical column
df['in_shazam_charts'] = df['in_shazam_charts'].str.replace(',', '')
df['in_shazam_charts'] = pd.to_numeric(df['in_shazam_charts'], errors='coerce')
```
*Note that when using the pd.to_numeric() function and set the parameters of error to 'coerce', python will convert the columns into numerical data and remove string entries, replacing it with missing values (NaN), making the entire column into a float data type, since float can handle NaN values. But if the column is complete with no missing values, it will convert it into an integer data type.*  

For this project, in majority I used **seaborn** as my primary data visualization tool in analyzing trends and correlations between different variables  

# Overview of Dataset

* In the given dataset, there are 953 rows and 24 columns
```
#Number of rows and columns of the Dataset. Note that the output of the .shape function is (Rows, Columns)
rows, columns = df.shape
print('Rows: ', rows, '\nColumns: ', columns)
```

* The data types of each column are as follows. Note that object data type are string (object) data types. Also, the 'streams' and 'in_shazam_charts' are in float since both contain missing values
**Insert Picture**

* There is 1 missing value in 'streams', 50 missing values in 'in_shazam_charts', and 95 missing values in 'key'. *Note that the 1 missing value in streams is the removed corrupted value*
**Insert Picture**

# Basic Descriptive Statistics

* Mean, Median, and Standard Deviation of the streams column  
**Insert Picture**

* Relationship between released_year and artist_count  
I noticed the trend where in the number of artists increases as the year progresses, in other words, more and more people are becoming an artist as the year goes by that by 2023, a lot of single artists have emereged. Also, the artist count increases as the year passes, hence many artists tries to make music in groups.  
As for the outliers, I noticed that in the early 1930s, artists are formed in groups rather than being single.
**Insert Picture**

# Top Performers

* The top 5 most streamed tracks are as follows
**Insert Picture**

* Top 5 most frequent artists based on the number of tracks
**Insert Picture**

# Temporal Trends

* Number of tracks released per year
Based on the given bar graph, we can see that the tracks released increases as year progresses
**Insert Picture**

* Number of tracks released per month
Based on the graph outcome, the number of tracks released per month does not follow any noticeable trends, meaning that artists release their music at any time of the year. Also, the month of January has the highest number of tracks released **Paraphrase**

# Genre and Music Characteristics
