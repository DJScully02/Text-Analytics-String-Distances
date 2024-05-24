# Text-Analytics-String-Distances

## Table of Contents

- [Project Goals](#project-goals)
- [Correlation Table & Plot for each method](#correlation-table-&-plot-for-each-method)
- [Comparison of String Distance Metrics](#comparison-of-string-distance-metrics)
- [References](#references)

### Data Source
The dataset we are using is from the babynames library and iscalled 'babynames' it was collected by the Social Security Administration (SSA), It was collected from the years 1880 to 2017, it has columns for the name, how many children were named that name, their gender, the year, and the proportion. This dataset also only takes into account names that have over 5 uses.

### Project Categories

**Data Science, Text Analytics, String Matching/Distance Calculation, Data Visualization, R Programming**

### Project Goals

1. **Finding Similar Names Using String Distances**
   - Find the ten names in the babynames::babynames data set that are the most similar to the first name "Christian" using various string distance metrics.
Time Series Plotting

2. **Time Series Plotting**
   - Plot the identified names as time series by year.

3. **Comparison of String Distance Metrics**
   - Articulate the similarities and differences observed for each string distance metric used.
   - Utilize **Full Damerau-Levenshtein Distance (dl), Optimal String Alignment (osa), Longest Common Substring Distance (lcs), Levenshtein Distance (lv), Q-Gram Distance (qgram), Jaro-Winkler Distance (jw), Jaccard Distance Between Q-Gram Profiles (jaccard), Cosine Distance Between Q-Gram Profiles (cosine), Distance Based on Soundex Encoding (soundex)**

### Tools
- R programming language - Data Analysis and Data Visualization
  - [Download here](https://posit.co/download/rstudio-desktop/)
 
### Libraries Used

- **dplyr:** Data manipulation and transformation.
- **viridis:** Color palettes for data visualization.
- **ggplot2:** Data visualization and plotting.
- **babynames:** Data set containing baby names and their frequencies by year.
- **stringdist:** Calculating string distances using various metrics.

### Exploratory Analysis
We first want to start with a bit of exploratory analysis to familiarize ourselves with the dataset. We started by looking into how many people were born for every year in our dataset as well as how many were Male vs Female.

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/eefae060-9e52-4dde-a9ae-b33cab4a8699" alt="Total Births" style="width: 45%; margin: 10px;">
</div>
In the image above, we observe several significant trends in birth rates across different historical periods:

- **Late 1930s (1929-1939)**: The lowest point on the graph occurs during the Great Depression, a time of severe economic hardship. This period saw a substantial impact on the financial stability of families, leading many to delay or avoid having children altogether.

- **Post-World War II Baby Boom (1946-1964)**: After 1939, we notice a slight increase in birth rates, followed by a sharp peak. This corresponds to the Baby Boom, which occurred between 1946 and 1964. Following the end of World War II in 1945, there was widespread optimism and economic prosperity in the United States, resulting in a significant increase in births.

- **Economic Challenges in the 1970s**: The graph shows another decline in the 1970s, reflecting the economic challenges of the era, including the oil crisis, high inflation, and unemployment. These conditions caused financial instability for many families, leading them to delay or avoid having children, similar to the impact seen during the Great Depression.

- **Economic Stabilization (1980s-Early 2000s)**: From the 1980s to the early 2000s, the US economy began to stabilize. This period allowed families to avoid the severe financial hardships experienced in previous years. Additionally, changes in societal norms and advances in family planning and reproductive health contributed to a more conscious approach to parenthood.

- **Great Recession (2007-2009)**: The Great Recession, spanning from 2007 to 2009, had a significant impact on the economy, leading to job losses and financial difficulties for many. This period is marked by another noticeable decline in birth rates.

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/104a0cb4-cc21-4fca-8935-960648498438" alt="Number of Births M vs F" style="width: 45%; margin: 10px;">
</div>

From the 1880s to around the mid-1930s, there were slightly more female births than male births. After the mid-1930s, this trend reversed, with male births exceeding female births, a pattern that has persisted to the present day.

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/b4fd5efd-5a27-4625-82e7-aa72f0f3a3c2" alt="Correlation Plot" style="width: 45%; margin: 10px;">
</div>

The plot above illustrates the historical frequency of the name 'Christian' for both males and females, highlighting a significantly higher prevalence among males. This disparity indicates that we have a more extensive dataset for male 'Christian' names, providing a richer and more detailed foundation for our string distance analysis. In contrast, the comparatively lower frequency of the name among females means we have less data to work with for female 'Christian' names. Understanding this distribution is crucial, as it allows us to account for gender differences in name usage patterns and ensures that our analysis accurately reflects these trends.

Now we will take a look how the measures are correlated. Using hierarchical clustering with Euclidean distance and Ward's D method.

#### Correlation Table & Plot for each method

|           | lcs  | lv   | osa  | dl   | qgram | jw   | jaccard | cosine | soundex |
|-----------|------|------|------|------|-------|------|---------|--------|---------|
| lcs       | 1.00 | 0.77 | 0.77 | 0.77 | 0.78  | 0.47 | 0.57    | 0.59   | 0.18    |
| lv        | 0.77 | 1.00 | 0.99 | 0.99 | 0.67  | 0.62 | 0.60    | 0.64   | 0.20    |
| osa       | 0.77 | 0.99 | 1.00 | 1.00 | 0.67  | 0.63 | 0.61    | 0.64   | 0.20    |
| dl        | 0.77 | 0.99 | 1.00 | 1.00 | 0.68  | 0.63 | 0.62    | 0.65   | 0.20    |
| qgram     | 0.78 | 0.67 | 0.67 | 0.68 | 1.00  | 0.54 | 0.85    | 0.83   | 0.14    |
| jw        | 0.47 | 0.62 | 0.63 | 0.63 | 0.54  | 1.00 | 0.63    | 0.68   | 0.12    |
| jaccard   | 0.57 | 0.60 | 0.61 | 0.62 | 0.85  | 0.63 | 1.00    | 0.88   | 0.19    |
| cosine    | 0.59 | 0.64 | 0.64 | 0.65 | 0.83  | 0.68 | 0.88    | 1.00   | 0.12    |
| soundex   | 0.18 | 0.20 | 0.20 | 0.20 | 0.14  | 0.12 | 0.19    | 0.12   | 1.00    |


<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/b4fd5efd-5a27-4625-82e7-aa72f0f3a3c2" alt="Correlation Plot" style="width: 45%; margin: 10px;">
</div>
The most correlated methods are the Levenshtein distance (lv) and Optimal String Alignment (osa) with a correlation of 0.99, indicating they produce very similar results. Conversely, the least correlated methods are Soundex and Jaro-Winkler (jw) with a correlation of 0.12, suggesting they capture different aspects of string similarity.

### Comparison of String Distance Metrics

In this section we will show the top 10 names that are the closest to the first name 'Christian'  that each distance metric gives. We utilize the distance metrics on just males, just females and on both genders.

#### Full Damerau-Levenshtein Distance (dl)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/d1e57359-b5f1-4680-abb6-ad4d2a21982a" alt="dl Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/1a0ab9eb-de8e-4425-9e86-2a01cf2fb11f" alt="dl Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Optimal String Alignment (osa)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/a376281b-4248-4b50-9656-410861f9d770" alt="osa Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/bf23f8f6-2359-4d1e-bdca-5bac375b45ea" alt="osa Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Longest Common Substring Distance (lcs)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/43fc5520-521f-4971-be95-58c553b3ed2c" alt="lcs Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/3189f393-350f-43e0-b668-a20dff62a0fa" alt="lcs Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Levenshtein Distance (lv)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/8edb0ddf-b120-4885-bf26-8e6ac895ea03" alt="lv Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/69bf28c6-a148-4e9c-b866-87796f442524" alt="lv Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Q-Gram Distance (qgram)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/2c9afe12-83f3-4cb3-bcc1-1be65534af39" alt="qgram Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/c6fad2e6-e41f-49f3-9855-c4fc96c90dfa" alt="qgram Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Jaro-Winkler Distance (jw)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/a5b87135-7de9-405e-8827-50ef4e898634" alt="jw Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/beed835a-5172-4880-810f-730007d69f41" alt="jw Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Jaccard Distance Between Q-Gram Profiles (jaccard)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/84a407aa-5f75-4500-88eb-9a47fd84f7f7" alt="jaccard Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/f8c145f0-db0c-48f5-910f-139ea845720b" alt="jaccard Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Cosine Distance Between Q-Gram Profiles (cosine) 

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/cc179363-f42f-419f-92a0-68c4c8f9fcd2" alt="cosine Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/3701b9ac-0e1d-4d85-9dc3-4c25d09a4291" alt="cosine Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Distance Based on Soundex Encoding (soundex)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/0f7cd46f-abf6-4f19-ab78-bef70d6964cb" alt="soundex Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/2f8d112b-9027-475e-9baa-d89b7fdfaeb7" alt="soundex Both Genders" style="width: 100%; margin: 10px;">
</div>

#### Closest Matches per Distance Metric

| lcs          | lv           | osa          | dl           | qgram       | jw           | jaccard      | cosine       | soundex       |
|--------------|--------------|--------------|--------------|-------------|--------------|--------------|--------------|---------------|
| Christian    | Christian    | Christian    | Christian    | Chirstian   | Christian    | Chirstian    | Chirstian    | Carista       |
| Chistian     | Chistian     | Chirstian    | Chirstian    | Chirstina   | Christhian   | Chirstina    | Chirstina    | Carsten       |
| Christan     | Christan     | Chistian     | Chistian     | Chrisitan   | Christiaan   | Chrisanthi   | Chrisitan    | Carston       |
| Christhian   | Christean    | Chrisitan    | Chrisitan    | Christain   | Christiana   | Chrisitan    | Christain    | Carstyn       |
| Christia     | Christhian   | Christain    | Christain    | Christian   | Christiane   | Christain    | Christian    | Cchristopher  |
| Christiaan   | Christia     | Christan     | Christan     | Christina   | Christiann   | Christan     | Christina    | Charistopher  |
| Christiana   | Christiaan   | Christean    | Christean    | Chrsitina   | Christiano   | Christana    | Chrsitina    | Charkita      |
| Christiane   | Christiam    | Christhian   | Christhian   | Cristhian   | Chirstian    | Christann    | Cristhian    | Charquita     |
| Christiann   | Christiana   | Christia     | Christia     | Chistian    | Chistian     | Christanna   | Christinia   | Chirstian     |
| Christiano   | Christiane   | Christiaan   | Christiaan   | Chistina    | Chrisitan    | Christhian   | Chrisanthi   | Chirstina     |
### References
1. [Irene-arch](https://github.com/Irene-arch/Documenting_Example/blob/main/README.md)
2. [Dr. Aaron Smith](https://www.statistics.ninja/home)
