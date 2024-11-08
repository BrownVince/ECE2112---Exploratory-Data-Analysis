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
import matplotlib.pyplot as plt

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

* **In the given dataset, there are 953 rows and 24 columns.** *This also appears at the bottom left of the dataset when loading it*  
The .shape function helps us identify the dimensions of the dataset in rows and columns  
```
rows, columns = df.shape
print('Rows: ', rows, '\nColumns: ', columns)
```

* **The data types of each column are shown in a table using the .dtype function.** Note that object data type are string (object) data types. Also, the 'streams' and 'in_shazam_charts' are in float since both contain missing values  
In order to show the data types of each column, the .dtype function is a must function in order to get the data types of each column in a dataset. This helps when your dataset has a lot of columns, using this will just display all your columns and their data types in a table.
```
df.dtypes
```
![Screenshot 2024-11-06 224728](https://github.com/user-attachments/assets/899f6b99-cb0c-495d-a250-594df7e6a671)

* There is 1 missing value in 'streams', 50 missing values in 'in_shazam_charts', and 95 missing values in 'key'. *Note that the 1 missing value in streams is the removed corrupted value*  
The function .isnull() helps in finding cells that are empty or of no value, together with the .sum() function, it will add the total number of cells that are empty. Then after that, we need to print columns with empty cells and on how many empty cells are there by indexing and filtering the data that have more than 0 values.
```
mcount = df.isnull().sum()
print('COLUMN \t\t MISSING COUNT')
print(mcount[mcount>0])
```
![Screenshot 2024-11-09 010457](https://github.com/user-attachments/assets/d425ce85-e4a8-4aa0-86e7-0fab5ccbab32)

# Basic Descriptive Statistics

* **Mean, Median, and Standard Deviation of the streams column**  
In finding the mean, median, and std, python has a standard built in function to use in order to find the results you want in a fast and easy way.
```
print('Mean: ', round(df['streams'].mean(), 2))
print('Median: ', round(df['streams'].median(), 2))
print('Standard Deviation: ', round(df['streams'].std(), 2))
```
![Screenshot 2024-11-09 011210](https://github.com/user-attachments/assets/241a9a07-489d-4c2f-956f-66ecc2920f1e)

* **Relationship between released_year and artist_count**  
In displaying the relationship between the two, I used seaborn's scatterplot/stripplot.
```
plt.figure(figsize=(24,10))
sns.stripplot(x='artist_count', y='released_year', data=df)
```
I noticed the trend where in the number of artists increases as the year progresses, in other words, more and more people are becoming an artist as the year goes by that by 2023, a lot of single artists have emereged. Also, the artist count increases as the year passes, hence many artists tries to make music in groups.   
As for the outliers, I noticed that in the early 1930s, artists are formed in groups rather than being single.  
![Screenshot 2024-11-07 004254](https://github.com/user-attachments/assets/1ed0476d-f969-4934-beae-378aace1022e)

# Top Performers

* **The top 5 most streamed tracks** are as follows  
In finding the top 5 most streamed tracks, we first need to sort the date set using the .sort_values() function and set the parameters by='streams', since we want to output most streamed tracks, then set ascending to false in order tp have a descending order. After that, display only five using the .head() function and set the parameters to 5 and display only columns 'track_name' and 'streams'
```
toptracks = df.sort_values(by='streams', ascending=False)
top5tracks = toptracks.head(5)[['track_name', 'streams']]

plt.figure(figsize=(17,7))
sns.barplot(x='track_name', y='streams', data=top5tracks)
plt.xlabel('Track Name')
plt.ylabel('Total Streams')
```
With the number one spot, we have Blinding Lights! as the most streamed track making it the most popular one, followed by Shape of You, Someone You Loved, Dance Monkey, and Sunflower - Spider-Man: Into the Spider-Verse.  
*Additionaly, if you want to display the artists that owns these tracks, you can add the column name in this code toptracks.head(5)[['COLUMN NAME']]*  

![Screenshot 2024-11-09 053630](https://github.com/user-attachments/assets/1c311d28-6354-4397-a2d4-915b47dae507)

* **Top 5 most frequent artists based on the number of tracks**    
In this problem, I was having a hard time at first since I noticed that some cells have multiple artists.  
So I first split the column of artist(s)_name in order to explode the column. The .explode() function will make individual rows for each artists, hence separating multiple artists that are present in a single cell, creating more rows. After that, I used the .value_counts() function in order to count duplicate entries for each individual cell in a column, note that when using the .value_counts() function, it will automatically present the output in a descending order, hence we can just add .head(5) in order to display the top 5 frequent artists based on the number of tracks.
```
splitnames = df['artist(s)_name'].str.split(', ')
srows = splitnames.explode()
freqartist = srows.value_counts().head(5)
dffreqartist = pd.DataFrame(freqartist)

plt.figure(figsize=(17,7))
sns.barplot(x='artist(s)_name', y='count', data=dffreqartist)
plt.xlabel('Artist Name')
plt.ylabel('Count')
```
Congrats to Bad Bunny for having the highest number of tracks garnering a total number of 40 tracks! followed by, Taylor Swift, The Weeknd, SZA, and Kendrick Lamar.  
![Screenshot 2024-11-09 053647](https://github.com/user-attachments/assets/2fd9c4ac-c17d-44aa-97bd-9116bddb3702)

# Temporal Trends

* **Number of tracks released per year**
In analyzing this problem, I used the .groupby() function in order to group tracks according to what year they are released and then counted how many tracks are present in a specific year. In plotting the data, I used seaborn's barplot.
```
numtrackyear = df.groupby('released_year')['track_name'].count()
plt.figure(figsize=(24,10))
sns.barplot(data=numtrackyear)
plt.ylabel('Number of Tracks')
```
Based on the given bar graph, we can see that the number of tracks released increases as year progresses. As early as 1930 up to 2023, 1930? That's very old.  
![Screenshot 2024-11-09 053916](https://github.com/user-attachments/assets/bc0cdd9b-c3dc-4512-9187-43c17cf2196b)

* **Number of tracks released per month**
This problem is the same with the number of tracks released per year, the only difference is that I grouped the tracks according to what month they are released in.
```
numtrackmnth = df.groupby('released_month')['track_name'].count()
plt.figure(figsize=(24,10))
sns.barplot(data=numtrackmnth)
plt.ylabel('Number of Tracks')
```
Based on the graph outcome, the number of tracks released per month does not follow any noticeable trends, meaning that artists release their music at any time of the year. Also, the month of January has the highest number of tracks released.    
![Screenshot 2024-11-09 053935](https://github.com/user-attachments/assets/61e8de38-5b31-48fb-aee4-c96b0b7141bd)

# Genre and Music Characteristics
* **Correlation between streams and musical attributes**
In coding this problem, I used a simple syntax using seaborn's scatterplot in order to determine the correletion between streams and different musical attributes  
```
plt.figure(figsize=(10,10))
sns.scatterplot(x='NAME OF MUSICAL ATTRIBUTE', y='streams', data=df)
```
After creating all the graphs, I noticed that almost all of them have little to no correlation. Meaning that music types totally depends on the taste of a person.  
*Compilation of Graphs:*  

* **Correlation between danceability_% and energy_%**
```
```

* **Correlation between valence_% and acousticness_%**
```
```

# Platform Popularity
* **Comparing number of tracks in spotify_playlists, apple_playlists, and deezer_playlists**  
When I compared the number of tracks in the different platforms, I first created a new variable containing a Data Frame with the total or sum of the values of each platform's columns from the original data set using the function df['PLATFORM NAME'].sum() and stored it in a new column named 'Total # of Tracks' and assigned it according to their names by creating another column containing the names of each platform.
Then I used seaborn's barplot to plot the values with names in the x-axis, and their values in the y-axis.
```
ntracks = pd.DataFrame({'Platform': ['Spotify', 'Apple', 'Deezer'],
                       'Total # of Tracks': [df['in_spotify_playlists'].sum(), df['in_apple_playlists'].sum(), 
                                                df['in_deezer_playlists'].sum()]})
print(ntracks)
sns.barplot(x='Platform', y='Total # of Tracks', data=ntracks)
```
We can see that spotify domainates in the number of tracks present in their playlists. The second place belongs to deezer, and the third place belongs to apple.
**INSERT PIC**

* **Which platform favors the most popular tracks**  
In this problem, it is the same as the previous one, but this finds which platform has the highest number of most popular tracks present in their playlist. Hence, we start by selecting the most popular tracks, whereas I cosidered the top 10 tracks.
```
top10 = toptracks.head(10)[['track_name', 'streams', 'in_spotify_playlists', 'in_apple_playlists', 'in_deezer_playlists']]

poppform = pd.DataFrame({'Platform': ['Spotify', 'Apple', 'Deezer'],
                       'Total # of Playlists': [top10['in_spotify_playlists'].sum(), top10['in_apple_playlists'].sum(), 
                                                top10['in_deezer_playlists'].sum()]})
print(poppform)
sns.barplot(x='Platform', y='Total # of Playlists', data=poppform)
```
As usual, as a result, spotify favors the most popular tracks, deezer as second, and apple being third.
**INSERT PIC**

# Advanced Analysis
* **Patterns among tracks with the same key and mode based on streams data**
Again, in this problem I used the .groupby() function by grouping the tracks according to their specific keys or mode and added the all the streams value in a specific group by using the .sum() function.
And since when using the .groupby() function, we get a series as a result, hence we need to convert the data into a data frame in order to graph the values. And of course, since I'm a Seaborn fan, I used seaborn's barplot again to plot the values, with key or mode in the x-axis, and streams on the y-axis.
```
#Based on the streams data, patterns among tracks with the same key
skey = df.groupby('key')['streams'].sum()
dfskey = pd.DataFrame(skey)
plt.figure(figsize=(12,7))
sns.barplot(x='key', y='streams', data=dfskey)

#Based on the streams data, patterns among tracks with the same mode (Major vs. Minor)?
smode = df.groupby('mode')['streams'].sum()
dfsmode = pd.DataFrame(smode)
plt.figure(figsize=(7,7))
sns.barplot(x='mode', y='streams', data=dfsmode)
```
As a result, we get the key C# as the highest playing key, and mode Major as the highest playing mode. Meaning that people like to listen on key C# and mode major the most. While less people listen to key D# and mode minor.  
![Screenshot 2024-11-09 060240](https://github.com/user-attachments/assets/57c6db37-1935-4ebc-abcd-6e578b35059f)  
![Screenshot 2024-11-09 060253](https://github.com/user-attachments/assets/6974ed12-5a97-4422-8a7f-ff416c438b1a)  


* **Most frequently appearing artists in playlists or charts**
Lastly, in this problem we need to split and explode the artists column again since there are multiple artists present in a single cell then make the splitted column into a dataframe in order to add a column that contains the total number of playlists or charts for each artist, so we set the .sum(axis=1) in order to add total playlist or chart for each artist in a row, and not the sum of the entire column. Then after that, we need to explode the resulting data frame in order to separate artists into individual cells or rows. Then we need to group again the set based on artist name using the .groupby() function and add the total playlist or charts for each group (now known as a single artist name). Sorting the values to descending order and display only 5, we now get the top 5 artists for playlists and charts. 
```
dfsnames = pd.DataFrame(splitnames, columns=['artist(s)_name'])
dfsnames['total_playlists'] = df[['in_spotify_playlists', 'in_apple_playlists', 'in_deezer_playlists']].sum(axis=1)
dfsnames['total_charts'] = df[['in_spotify_charts', 'in_apple_charts', 'in_deezer_charts', 'in_shazam_charts']].sum(axis=1)

dfsnexploded = dfsnames.explode('artist(s)_name').reset_index(drop=True)

plrank = dfsnexploded.groupby('artist(s)_name')['total_playlists'].sum()
chrank = dfsnexploded.groupby('artist(s)_name')['total_charts'].sum()

psort = plrank.sort_values(ascending=False).head(5)
csort = chrank.sort_values(ascending=False).head(5)

dfplrank = pd.DataFrame(psort)
dfchrank = pd.DataFrame(csort)

#For the most frequent artist appeared in playlist
plt.figure(figsize=(17,7))
sns.barplot(x='artist(s)_name', y='total_playlists', data=dfplrank)
plt.xlabel('Artist Name')
plt.ylabel('Total Playlist')
plt.title('Most frequently appearing artists in playlists')

#For the most frequent artist appeared in chart
plt.figure(figsize=(17,7))
sns.barplot(x='artist(s)_name', y='total_charts', data=dfchrank)
plt.xlabel('Artist Name')
plt.ylabel('Total Charts')
plt.title('Most frequently appearing artists in charts')
```
For the most frequent artist appeared in playlist, we have The Weeknd, followed by Eminem, Ed Sheeran, Taylor Swift, and Bad Bunny  
For the most frequent artist appeared in chart, we have the number one spot taken again by The Weeknd, followed by, Bad Bunny, Taylor Swift, Peso Pluma, and David Guetta  
Meaning that The Weeknd is the only one consistent in the rankings.  
![Screenshot 2024-11-09 055529](https://github.com/user-attachments/assets/08f794c6-020f-4334-9f3e-daa5f7513ede)  
![Screenshot 2024-11-09 055548](https://github.com/user-attachments/assets/5152ed64-54d6-4f35-af2a-3909f3544712)

