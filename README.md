# Crisp-DM_Mini-Project
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
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/b7814f49-d640-4d61-b88e-b1169cdfcc71" width="4=35%">
</div>

### Load Data
Create a data frame then load the data set. Here the dataset used is WorldCupMatches
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/b1e3f13b-0ad1-4207-b97b-be08268dbfab" width="35%">
</div>
Display the data set that has been loaded
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/4f4487dd-50e8-4385-9684-7c922b3e36df" width="15%">
</div>

### Data Cleansing
#### Check Data Condition
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/f6c4c951-6a1d-45fa-923b-6ce4315d7dfc" width="40%">
</div>
From the description, we can see that some columns have fewer non-null values than the total entries (4572), indicating the presence of null or empty values in the DataFrame. Additionally, we can also observe the data types of each column, where there are columns whose data types are not yet appropriate.

#### Check and remove duplicate rows from theData Frame
**keep**
- {‘first’, ‘last’, False}, default ‘first’
- Determines which duplicates (if any) to mark.
- first : Mark duplicates as True except for the first occurrence.
- last : Mark duplicates as True except for the last occurrence.
- False : Mark all duplicates as True.

<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/f33c1a04-389b-4ea6-9b0c-6c03dfb54ae4" width="35%">
</div>

Count duplicate is 3735

Remove these duplicate rows to ensure data integrity and accuracy.

Due to the presence of numerous NaN values, our first step will be to drop rows containing NaN values.
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/9458cc87-5492-4848-9215-ad878980f61e" width="50%">
</div>

### Convert Dtype
Converting data types ensures that the data is in the correct format for analysis and allows for more efficient and accurate data processing.
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/2edca67c-e43f-4c79-b831-6048821a19d3" width="50%">
</div>

<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/66bdde80-e2b1-4e8e-9357-3b96ad351f37" width="50%">
</div>

### Check Percentage Missing Values
checking the percentage of missing values provides valuable insights into the data quality and guides decision-making regarding data preprocessing and analysis strategies.
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/c61fdf29-b305-424f-81ba-5c13998ffcfa" width="50%">
</div>
It turns out that only the 'Datetime' column has missing values. Although the number of missing values is not significant, considering that 'Datetime' is a crucial column for analysis, we have decided to retain the missing values in the 'Datetime' column.
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/743a8c1c-6599-44c4-8ead-f9d3aca6e963" width="50%">
</div>

### Data Manipulation
Data manipulation involves making changes to the dataset to prepare it for analysis or to extract valuable insights. This process includes tasks such as cleaning the data, transforming its structure, creating new features, and aggregating information.
#### Drop Non-Essential Columns
This step involves removing columns from the dataset that are deemed non-essential for the analysis. Non-essential columns are those that do not contribute significantly to the analysis or do not align with the research objectives. By dropping these columns, we can streamline the dataset and focus only on the most relevant features.
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/6479cc47-3a0c-40ac-becd-fc45bf2293fe" width="50%">
</div>
We drop columns such as 'Referee', 'Assistant 1', 'Assistant 2', 'Home Team Initials', and 'Away Team Initials' as they are not critical for the analysis at hand.
#### Make Column Draw, Date, and Time
We will perform data manipulation here. Manipulation here does not involve altering data values but rather restructuring the data to make it easier for machines to read.

To determine whether a match ended in a draw or not, we can use the "Home Team Goals" and "Away Team Goals" columns.

<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/b27d6c9c-9668-4d99-a2aa-51d4f6c0d189" width="50%">
</div>

<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/48835fa0-da17-4a68-9261-49f004098387" width="50%">
</div>
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/98ce9462-3dd1-4109-a59e-0b2758bafd93" width="80%">
</div>

## Modeling
### 1. Who are the top five teams that scored the most goals when hosting matches in 2014?
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/b9750622-fb80-45ce-87c5-e9c655a49c3d" width="50%">
</div>

Based on the data in the above graph, the top 5 data for the year 2014 indicate that teams from **Germany, Brazil, and Colombia have the same distribution, which is 7. This means that these countries scored a total of 7 goals each in 2014.** Meanwhile, France and Argentina have the same distribution level, which is 5. This implies that **France and Argentina scored a total of 5 goals each in 2014.**

### 2. What is the total attendance in 2014 based on the stadium?
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/40f4c2cc-0bd4-4c9b-8e24-e5b6e693d8b4" width="50%">
</div>

Based on the above graph, it is evident that **the highest total attendance in 2014 was recorded at Estadio do Maracana, with a total of 519,189 spectators.** Meanwhile, **the fifth highest position is held by Estadio Mineirao with an attendance of 345,350 spectators.**

### 3. How many matches ended in a draw in 2014?
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/4270bf86-a11d-4f84-a018-01230d453108" width="50%">
</div>

Based on the data presented, there are two main categories for the outcomes of football matches: **"No" (not drawn) and "Yes" (drawn).** Out of 63 matches in the year 2014, a total of **50 matches (approximately 79.4%) ended without a draw**, while only **13 matches (approximately 20.6%) resulted in a draw.** From this, it can be concluded that **draw results tend to be less frequent occurrences in football matches**, with the majority of matches tending to produce a clear winner without the need for extra time or penalty shootouts.

### 4. What is the distribution of match results based on the 'win condition'?
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/a9e41e7e-adac-4a93-83a6-70b14e87035d" width="50%">
</div>

Out of 63 matches in 2014, **56 matches ended without any special conditions**, meaning there were no draws and no need for extra time or penalties. Meanwhile, **7 other matches had victory conditions, such as Brazil winning through a penalty shootout (3-2), Germany winning in extra time, and Argentina winning through a penalty shootout (2-4).** These matches occurred during the group stage and ended in a draw, thus requiring extra time and penalties to determine the winner.

### 5. Which stadium was most frequently used during matches in 2014?
<div align="center"><img src="https://github.com/Shabiyyahzlf/Crisp-DM_Mini-Project/assets/89763971/39f6c551-5260-4ef8-97b7-38a86c03ebc0" width="50%">
</div>

From the data above, it can be observed that the top 5 stadiums with **the highest usage in 2014 were Estadio Maracana and Estadio Nacional, each being used 7 times.** These stadiums are well-known for their large capacity and being located in major cities, making them easily accessible for teams, fans, and media.

## Evaluation
- The distribution of teams scoring goals when playing at home in 2014 is dominated by teams from Germany, Brazil, and Colombia, each with a distribution of 7.
- Estadio do Maracana is the stadium with the highest total attendance, hosting 519,189 spectators.
- There are two main categories for the outcomes of football matches: "No" (not drawn) and "Yes" (drawn). Out of 63 matches played in 2014, 50 ended without a draw, while the remaining 13 ended in a draw.
- Out of 63 matches in 2014, 56 ended without any special conditions, meaning there were no draws and no need for extra time or penalties. Meanwhile, 7 other matches had specific winning conditions.
- Estadio Maracana and Estadio Nacional are the stadiums most frequently used in FIFA World Cup matches, each being used 7 times in 2014.

