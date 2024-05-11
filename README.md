# Mini Project_Crisp DM
## Business Understanding
During the FIFA World Cup, various sports events are held, one of which is World Cup Matches. The World Cup Matches dataset contains information about football matches that occurred during the FIFA World Cup from 1930 to 2014.

Source Data: https://www.kaggle.com/datasets/abecklas/fifa-world-cup 

**Business Questions:** Based on the dataset, several questions arise:
1. What is the distribution of teams scoring goals while hosting matches in 2014 (showing the top 5 data)?
2. What is the total attendance in 2014 based on the stadium?
3. How many matches ended in a draw in 2014?
4. What is the distribution of match results based on the 'win condition'?
5. Which stadiums were frequently used during the World Cup matches in 2014 (showing the top 5 data)?

## Data Understanding
Data Understanding contains information about the existing dataset, explanations regarding its columns, whether the dataset is complete or not, and other relevant details.

**Insights and Considerations** 
- This dataset spans from 1930 to 2014. 
- The total number of rows in this dataset is 4572, while there are 20 columns. 
- All columns have missing values, with 'Attendance' having the highest number of missing values, totaling 3722.

**Columns**
- **Year:** The year of the match. 
- **Home Team Name:** The name of the home team. 
- **Away Team Name:** The name of the away team.
- **Home Team Goals:** The score of the match and the performance of the home team in scoring goals.
- **Away Team Goals:** The score of the match and the performance of the away team in scoring goals.
- **Attendance:** The number of spectators in the match.
- **Datetime:** The date and time of the match. (to be manipulated later)
- **Half-time Home Goals:** The number of goals scored by the home team in the first half.
- **Half-time Away Goals:** The number of goals scored by the away team in the first half.
- **City:** The city where the match took place.
- **Stadium:** The name of the stadium where the match took place.
- **Stage:** The stage or phase of the tournament.
- **RoundID:** The ID of the tournament round.
- **MatchID:** The ID of the match.
- **Win conditions:** The conditions for winning the match.
- **Referee:** The name of the match referee.
- **Assistant** 1: The name of the first assistant referee.
- **Assistant** 2: The name of the second assistant referee.
- **Home Team Initials:** The initials of the home team.
- **Away Team Initials:** The initials of the away team.

## Data Preparation
- Check data conditions: Determine the number of columns and rows, and inspect whether all columns are fulfilled or not. Also, examine the data types of each column to ensure their correctness.
- Check and remove duplicate rows from the dataframe: After examining the data, it was found that there are 3,735 duplicate rows, out of which 3,720 are NaN data. Upon further investigation, it was confirmed that 15 of the duplicates were indeed duplicate data, so these 15 duplicate rows were dropped. The 3,720 NaN rows were also dropped as they were empty after a thorough check of the entire dataset.
- Some data types in certain columns are incorrect. Therefore, data type conversion was performed: changing the dtype of 'Year' from float to int, changing the dtype of 'Datetime' from object to datetime, changing the dtype of 'Home Team Goals' from object to int, changing the dtype of 'Away Team Goals' from float to int, changing the dtype of 'Attendance' from float to int, changing the dtype of 'Half-time Home Goals' from float to int, changing the dtype of 'Half-time Away Goals' from float to int, changing the dtype of 'RoundID' from float to int, and changing the dtype of 'MatchID' from float to int.
- Upon checking missing values, it was found that there are 10 missing values in the 'Datetime' column.
- Handling missing values: Imputation was performed on the 'Datetime' column, which still had missing values because the percentage of missing values was 1.19%. After imputation, all columns were fulfilled with 835 non-null values.

### Python Libraries Import 
                                                  import pandas as pd
                                                  import numpy as np
                                                  import matplotlib.pyplot as plt
                                                  %matplotlib inline
                                                  import seaborn as sns

### Load Data
Create a data frame then load the data set. Here the dataset used is WorldCupMatches

                                                  #Load data
                                                  
                                                  df = pd.read_csv('WorldCupMatches.csv')

Display the data set that has been loaded

                                                        df.head()
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/096dde33-3dd9-4983-8a42-0ab4f6d0e397">
</div>

### Data Cleansing
#### Check Data Condition
                                                        df.shape
                                                        
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/99573327-95c1-4f15-8d3e-4b2cde2e8b3a" width="20%">
</div>

                                                        df.info()
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/926f5c38-94ab-4363-931f-9dd81196d5db" width="40%">
</div>

From the description, we can see that some columns have fewer non-null values than the total entries (4572), indicating the presence of null or empty values in the DataFrame. Additionally, we can also observe the data types of each column, where there are columns whose data types are not yet appropriate.

#### Check and remove duplicate rows from theData Frame
**keep**
- {‘first’, ‘last’, False}, default ‘first’
- Determines which duplicates (if any) to mark.
- first : Mark duplicates as True except for the first occurrence.
- last : Mark duplicates as True except for the last occurrence.
- False : Mark all duplicates as True.

                                                  df[df.duplicated(keep='first')]
                                                  df[df.duplicated(keep='last')]
                                                  df.duplicated().sum() 
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/b54c029e-d5e2-406f-8ed9-a0e4b0cbf61c" width="20%">
</div>

Count duplicate is 3735. Remove these duplicate rows to ensure data integrity and accuracy.

Due to the presence of numerous NaN values, our first step will be to drop rows containing NaN values.

                                                  df.dropna(inplace=True)
                                                  df.duplicated().sum()
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/4d2b75ad-20ae-45c3-aad4-ad7e9f506c43" width="20%">
</div>

                                                  df[df.duplicated(keep='first')]
                                                  df[df.duplicated(keep='last')]
                                                  df.drop_duplicates(inplace=True)
                                                  df.duplicated().sum()
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/a5732d71-54f5-4a06-b6f7-22c4c821cb60" width="20%">
</div>

                                          df.shape  # Check the shape of the DataFrame after removing duplicates
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/41051be2-d3dc-46a9-95aa-215a5ffb8ae5" width="20%">
</div>                                         

### Convert Dtype
Converting data types ensures that the data is in the correct format for analysis and allows for more efficient and accurate data processing.

                                      # Replacing non-finite values with valid ones (e.g., 0)
                                      df['Year'] = df['Year'].fillna(0).astype(int)
                                      df['Home Team Goals'] = df['Home Team Goals'].fillna(0).astype(int)
                                      df['Away Team Goals'] = df['Away Team Goals'].fillna(0).astype(int)
                                      df['Attendance'] = df['Attendance'].fillna(0).astype(int)
                                      df['Half-time Home Goals'] = df['Half-time Home Goals'].fillna(0).astype(int)
                                      df['Half-time Away Goals'] = df['Half-time Away Goals'].fillna(0).astype(int)
                                      df['RoundID'] = df['RoundID'].fillna(0).astype(int)
                                      df['MatchID'] = df['MatchID'].fillna(0).astype(int)
                                      df['Datetime'] = pd.to_datetime(df['Datetime'], errors='coerce')


                                      # Deleting rows containing non-finite values while changing the data type.
                                      df = df.dropna(subset=['Year'])
                                      df['Year'] = df['Year'].astype(int)
                                      df = df.dropna(subset=['Home Team Goals'])
                                      df['Home Team Goals'] = df['Home Team Goals'].astype(int)
                                      df = df.dropna(subset=['Away Team Goals'])
                                      df['Away Team Goals'] = df['Away Team Goals'].astype(int)
                                      df = df.dropna(subset=['Attendance'])
                                      df['Attendance'] = df['Attendance'].astype(int)
                                      df = df.dropna(subset=['Half-time Home Goals'])
                                      df['Half-time Home Goals'] = df['Half-time Home Goals'].astype(int)
                                      df = df.dropna(subset=['Half-time Away Goals'])
                                      df['Half-time Away Goals'] = df['Half-time Away Goals'].astype(int)
                                      df = df.dropna(subset=['RoundID'])
                                      df['RoundID'] = df['RoundID'].astype(int)
                                      df = df.dropna(subset=['MatchID'])
                                      df['MatchID'] = df['MatchID'].astype(int)


                                      df.info()

<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/63980b6c-677e-4ab5-9ee1-5b1cdc7cbb24" width="50%">
</div>

### Check Percentage Missing Values
checking the percentage of missing values provides valuable insights into the data quality and guides decision-making regarding data preprocessing and analysis strategies.

                                      missing_values = df.isnull().sum()
                                      missing_percentage = (missing_values/len(df)) * 100
                                      missing_info = pd.DataFrame({
                                          'Column' : missing_values.index,
                                          'Missing Values' : missing_values.values,
                                          'Missing Percentage' : missing_percentage.values
                                      })
                                      print(missing_info)
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/7ac647e8-84a9-4566-b55a-e864f32b2b21" width="50%">
</div>

It turns out that only the 'Datetime' column has missing values. Although the number of missing values is not significant, considering that 'Datetime' is a crucial column for analysis, we have decided to retain the missing values in the 'Datetime' column.

                                      df_sorted = df.sort_values(by='Datetime', ascending=True)
                                      print(df_sorted)

                                      df.Datetime.value_counts()

                                      df['Datetime'] = df['Datetime'].fillna(method='backfill')

### Data Manipulation
Data manipulation involves making changes to the dataset to prepare it for analysis or to extract valuable insights. This process includes tasks such as cleaning the data, transforming its structure, creating new features, and aggregating information.
#### Drop Non-Essential Columns
This step involves removing columns from the dataset that are deemed non-essential for the analysis. Non-essential columns are those that do not contribute significantly to the analysis or do not align with the research objectives. By dropping these columns, we can streamline the dataset and focus only on the most relevant features.

                                      df.drop(['Referee', 'Assistant 1', 'Assistant 2', 'Home Team Initials', 'Away Team Initials'], 
                                              axis = 1, inplace=True)
                                      df.columns
                                      
We drop columns such as 'Referee', 'Assistant 1', 'Assistant 2', 'Home Team Initials', and 'Away Team Initials' as they are not critical for the analysis at hand.
#### Make Column Draw, Date, and Time
We will perform data manipulation here. Manipulation here does not involve altering data values but rather restructuring the data to make it easier for machines to read.

To determine whether a match ended in a draw or not, we can use the "Home Team Goals" and "Away Team Goals" columns.

                                      # We'll create a new column to indicate whether the match ended in a draw or not.
                                      df['Draw'] = df['Home Team Goals'] == df['Away Team Goals']
                                      
                                      # We'll change the values in the "Draw" column to True or False.
                                      df['Draw'] = df['Draw'].astype(str).replace({'True': 'Yes', 'False': 'No'})
                                      
                                      # Display the manipulation result
                                      print(df[['Home Team Goals', 'Away Team Goals', 'Draw']].head())
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/ef93a4a0-0fa9-4071-9907-99668f8e008d" width="50%">
</div>

                                      df['Tanggal'] = df['Datetime'].dt.date
                                      df['Waktu'] = df['Datetime'].dt.time
                                      df.head()
                                      
                                      # Changing the date format to "day - month"
                                      df['Tanggal'] = df['Datetime'].dt.strftime('%d - %b')
                                      
                                      # Example to display the manipulation result
                                      print(df[['Datetime', 'Tanggal']].head())
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/b3ed5776-6c8c-4879-bd37-199b320b3efe" width="50%">
</div>

                                      df.drop(columns=['Datetime'], inplace=True)
                                      df.rename(columns={'Tanggal': 'Date'}, inplace=True)
                                      df.rename(columns={'Waktu': 'Time'}, inplace=True)
                                      
                                      df.head()

<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/3d8798bd-9b02-4c5d-9836-f20add828b17" width="100%">
</div>

## Modeling
### 1. Who are the top five teams that scored the most goals when hosting matches in 2014?
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/05163f07-5ed6-4102-99cd-11edc070b15e" width="8A0%">
</div>

Based on the data in the above graph, the top 5 data for the year 2014 indicate that teams from **Germany, Brazil, and Colombia have the same distribution, which is 7. This means that these countries scored a total of 7 goals each in 2014.** Meanwhile, France and Argentina have the same distribution level, which is 5. This implies that **France and Argentina scored a total of 5 goals each in 2014.**

### 2. What is the total attendance in 2014 based on the stadium?
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/cdc130c5-868c-4520-b8fe-e818bf37b7e3" width="80%">
</div>

Based on the above graph, it is evident that **the highest total attendance in 2014 was recorded at Estadio do Maracana, with a total of 519,189 spectators.** Meanwhile, **the fifth highest position is held by Estadio Mineirao with an attendance of 345,350 spectators.**

### 3. How many matches ended in a draw in 2014?
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/9b6e507c-e97f-41b5-a858-436fa6211711" width="80%">
</div>

Based on the data presented, there are two main categories for the outcomes of football matches: **"No" (not drawn) and "Yes" (drawn).** Out of 63 matches in the year 2014, a total of **50 matches (approximately 79.4%) ended without a draw**, while only **13 matches (approximately 20.6%) resulted in a draw.** From this, it can be concluded that **draw results tend to be less frequent occurrences in football matches**, with the majority of matches tending to produce a clear winner without the need for extra time or penalty shootouts.

### 4. What is the distribution of match results based on the 'win condition'?
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/9b5269b1-57d3-4dc8-90aa-6d638d0341eb" width="80%">
</div>

Out of 63 matches in 2014, **56 matches ended without any special conditions**, meaning there were no draws and no need for extra time or penalties. Meanwhile, **7 other matches had victory conditions, such as Brazil winning through a penalty shootout (3-2), Germany winning in extra time, and Argentina winning through a penalty shootout (2-4).** These matches occurred during the group stage and ended in a draw, thus requiring extra time and penalties to determine the winner.

### 5. Which stadium was most frequently used during matches in 2014?
<div align="center"><img src="https://github.com/nabilahkh/Mini-Project_Crisp-DM/assets/92252191/df04f98e-6abd-4913-89a4-ff4b26a47103" width="80%">
</div>

From the data above, it can be observed that the top 5 stadiums with **the highest usage in 2014 were Estadio Maracana and Estadio Nacional, each being used 7 times.** These stadiums are well-known for their large capacity and being located in major cities, making them easily accessible for teams, fans, and media.

## Evaluation
- The distribution of teams scoring goals when playing at home in 2014 is dominated by teams from Germany, Brazil, and Colombia, each with a distribution of 7.
- Estadio do Maracana is the stadium with the highest total attendance, hosting 519,189 spectators.
- There are two main categories for the outcomes of football matches: "No" (not drawn) and "Yes" (drawn). Out of 63 matches played in 2014, 50 ended without a draw, while the remaining 13 ended in a draw.
- Out of 63 matches in 2014, 56 ended without any special conditions, meaning there were no draws and no need for extra time or penalties. Meanwhile, 7 other matches had specific winning conditions.
- Estadio Maracana and Estadio Nacional are the stadiums most frequently used in FIFA World Cup matches, each being used 7 times in 2014.

