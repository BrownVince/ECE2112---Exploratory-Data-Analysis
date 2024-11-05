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


