# Text-Analytics-String-Distances

## Table of Contents

- [Project Goals](#project-goals)
- [Exploratory Analysis](#exploratory-analysis)
- [Correlation Table and Plot for each method](#correlation-table-and-plot-for-each-method)
- [Comparison of String Distance Metrics](#comparison-of-string-distance-metrics)
- [Closest Matches per Distance Metric and End Results](#closest-matches-per-distance-metric-and-end-results)
- [References](#references)

### Data Source
The dataset we are using is from the babynames library and iscalled 'babynames' it was collected by the Social Security Administration (SSA), It was collected from the years 1880 to 2017, it has columns for the name, how many children were named that name, their gender, the year, and the proportion. This dataset also only takes into account names that have over 5 uses.

You can check out the 'babynames' github [here](https://github.com/hadley/babynames).
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

- **[Great Depression (1929-1939)](https://www.federalreservehistory.org/essays/great-depression)**: The lowest point on the graph occurs during the Great Depression, a time of severe economic hardship. This period saw a substantial impact on the financial stability of families, leading many to delay or avoid having children altogether.

- **[Post-World War II Baby Boom (1946-1964)](https://www.khanacademy.org/humanities/us-history/postwarera/postwar-era/a/the-baby-boom)**: After 1939, we notice a slight increase in birth rates, followed by a sharp peak. This corresponds to the Baby Boom, which occurred between 1946 and 1964. Following the end of World War II in 1945, there was widespread optimism and economic prosperity in the United States, resulting in a significant increase in births.

- **[Economic Challenges in the 1970s](https://www.khanacademy.org/humanities/us-history/postwarera/1970s-america/a/stagflation-and-the-oil-crisis#:~:text=Unemployment%20rates%20rose%2C%20while%20a,wage%2D%20and%20price%2Dfreezes.)**: The graph shows another decline in the 1970s, reflecting the economic challenges of the era, including the oil crisis, high inflation, and unemployment. These conditions caused financial instability for many families, leading them to delay or avoid having children, similar to the impact seen during the Great Depression.

- **[Economic Stabilization (1980s-Early 2000s)](https://www.nber.org/system/files/working_papers/w22693/w22693.pdf)**: From the 1980s to the early 2000s, the US economy began to stabilize. This period allowed families to avoid the severe financial hardships experienced in previous years. Additionally, changes in societal norms and advances in family planning and reproductive health contributed to a more conscious approach to parenthood.

- **[Great Recession (2007-2009)](https://www.federalreservehistory.org/essays/great-recession-of-200709)**: The Great Recession, spanning from 2007 to 2009, had a significant impact on the economy, leading to job losses and financial difficulties for many. This period is marked by another noticeable decline in birth rates.

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/104a0cb4-cc21-4fca-8935-960648498438" alt="Number of Births M vs F" style="width: 45%; margin: 10px;">
</div>

From the 1880s to around the mid-1930s, there were slightly more female births than male births. After the mid-1930s, this trend reversed, with male births exceeding female births, a pattern that has persisted to the present day.

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/5b14949d-d8fe-4b71-9b9a-9d6aa9fdf930" alt="Christian M vs F all time" style="width: 45%; margin: 10px;">
</div>

The plot above illustrates the historical frequency of the name "Christian" for both males and females, highlighting a significantly higher prevalence among males. This disparity indicates that we have a more extensive dataset for male "Christian" names, providing a richer and more detailed foundation for our string distance analysis. In contrast, the comparatively lower frequency of the name among females means we have less data to work with for female "Christian" names. Understanding this distribution is crucial, as it allows us to account for gender differences in name usage patterns and ensures that our analysis accurately reflects these trends.

Now we will take a look how the measures we wil use are correlated. Using hierarchical clustering with Euclidean distance and Ward's D method.

### Correlation Table and Plot for each method

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/b4fd5efd-5a27-4625-82e7-aa72f0f3a3c2" alt="Correlation Plot" style="width: 45%; margin: 10px;">
</div>

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


The most correlated methods are the Levenshtein distance (lv) and Optimal String Alignment (osa) with a correlation of 0.99, indicating they produce very similar results. Conversely, the least correlated methods are Soundex and Jaro-Winkler (jw) with a correlation of 0.12, suggesting they capture different aspects of string similarity.

### Comparison of String Distance Metrics

In this section we will show the top 10 names that are the closest to the first name 'Christian'  that each distance metric gives. We utilize the distance metrics on just males, just females and on both genders.

#### Full Damerau-Levenshtein Distance (dl)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/d1e57359-b5f1-4680-abb6-ad4d2a21982a" alt="dl Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/1a0ab9eb-de8e-4425-9e86-2a01cf2fb11f" alt="dl Both Genders" style="width: 100%; margin: 10px;">
</div>

The Damerau-Levenshtein Distance graphs show that "Christian" is the most common name for both genders, with a significant peak around the year 2000. Other similar names such as "Christain" and "Christia" have much lower frequencies and shorter periods of popularity.

#### Optimal String Alignment (osa)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/a376281b-4248-4b50-9656-410861f9d770" alt="osa Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/bf23f8f6-2359-4d1e-bdca-5bac375b45ea" alt="osa Both Genders" style="width: 100%; margin: 10px;">
</div>

The Optimal String Alignment graphs highlight "Christian" as the dominant name, particularly for males, with a notable increase in usage from the 1960s to the early 2000s. For females, variations like "Christain" and "Christia" also appear but are less common.

#### Longest Common Substring Distance (lcs)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/43fc5520-521f-4971-be95-58c553b3ed2c" alt="lcs Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/3189f393-350f-43e0-b668-a20dff62a0fa" alt="lcs Both Genders" style="width: 100%; margin: 10px;">
</div>

The Longest Common Subsequence Distance graphs illustrate that "Christian" saw a sharp rise in popularity starting in the 1960s, peaking around 2000. Variants such as "Christia" and "Christiaan" are less frequent and have shorter periods of prominence.

#### Levenshtein Distance (lv)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/8edb0ddf-b120-4885-bf26-8e6ac895ea03" alt="lv Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/69bf28c6-a148-4e9c-b866-87796f442524" alt="lv Both Genders" style="width: 100%; margin: 10px;">
</div>

Levenshtein Distance graphs show that "Christian" is consistently the most prevalent name, especially for males, with a peak in the late 1990s and early 2000s. Names like "Christan" and "Christiane" are present but with much lower occurrences.

#### Q-Gram Distance (qgram)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/2c9afe12-83f3-4cb3-bcc1-1be65534af39" alt="qgram Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/c6fad2e6-e41f-49f3-9855-c4fc96c90dfa" alt="qgram Both Genders" style="width: 100%; margin: 10px;">
</div>

The Q-Gram Distance graphs reveal that "Christian" saw a substantial rise in usage starting in the 1960s, reaching its peak around 2000. Notably, this distance also highlights the female name "Christina," which experienced a similar significant increase in popularity from the 1950s, peaking in the 1980s.

#### Jaro-Winkler Distance (jw)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/a5b87135-7de9-405e-8827-50ef4e898634" alt="jw Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/beed835a-5172-4880-810f-730007d69f41" alt="jw Both Genders" style="width: 100%; margin: 10px;">
</div>

The Jaro-Winkler Distance graphs reveal "Christian" as the predominant name, especially for males, with a rise in popularity from the 1960s and a peak around 2000. For females, "Christiana" and "Christiann" appear as similar names but with lower occurrences.

#### Jaccard Distance Between Q-Gram Profiles (jaccard)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/84a407aa-5f75-4500-88eb-9a47fd84f7f7" alt="jaccard Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/f8c145f0-db0c-48f5-910f-139ea845720b" alt="jaccard Both Genders" style="width: 100%; margin: 10px;">
</div>

The Jaccard Distance graphs don't preform as well as the above methods as we don't see the name "Christian". Here we have two primarily main names the first being "Christan" which saw a small increase of usage from the mid 1960's, reaching peaks around the mid 1980's. We also see the name "Chrisitan" with a similar small rise in usage from 1970's, reaching peaks in the early 2000's. 

#### Cosine Distance Between Q-Gram Profiles (cosine) 

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/cc179363-f42f-419f-92a0-68c4c8f9fcd2" alt="cosine Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/3701b9ac-0e1d-4d85-9dc3-4c25d09a4291" alt="cosine Both Genders" style="width: 100%; margin: 10px;">
</div>

The Cosine Distance preformed very similarly to the Q-Gram Distance. Where we get to see both "Christian" and "Christina" with popularity explained above in the Q-Gram Distance plot. However, we do see the difference in the other names recognized by the distance methods. For the Cosine Distance Methods we see names such as "Chrisanthi" and "Christinia" while Q-Gram Distance saw names like "Cristhian" and "Chistian"

#### Distance Based on Soundex Encoding (soundex)

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/0f7cd46f-abf6-4f19-ab78-bef70d6964cb" alt="soundex Female and Male" style="width: 100%; margin: 10px;">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/2f8d112b-9027-475e-9baa-d89b7fdfaeb7" alt="soundex Both Genders" style="width: 100%; margin: 10px;">
</div>

The Soundex Distance graphs preformed notatably the worst as expected. The most popular name we see is "Carsten" which saw an increase in popularity starting around the 1990's and peaking in the late 2000's. 

### Closest Matches per Distance Metric and End Results

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


The table presented showcases the results of various string distance algorithms used to find the closest names to "Christian." Each column represents a different string distance measure: Longest Common Subsequence (LCS), Levenshtein (LV), Optimal String Alignment (OSA), Damerau-Levenshtein (DL), Q-gram, Jaro-Winkler (JW), Jaccard, Cosine, and Soundex. These methods compare the similarity of strings based on different principles, resulting in varying lists of names closest to "Christian."

For most algorithms, "Christian" itself appears as the closest match, reflecting the precision of these algorithms in identifying exact matches. Notably, slight variations like "Chistian," "Christan," and "Christhian" frequently appear across multiple methods. These names demonstrate the algorithms' sensitivity to minor alterations in the string, such as missing letters or transpositions. For instance, "Chistian" is highly ranked by the LCS, LV, OSA, DL, and JW methods, which are designed to handle insertions, deletions, and substitutions efficiently. In contrast, Q-Gram and Cosine ranked "Christian" lower in the table.

Soundex, which is phonetic-based, identifies names like "Carista" and "Carsten" as close matches due to their similar sounds. This diversity in the closest names across different algorithms underscores the unique way each method evaluates string similarity, ranging from exact character matching to phonetic resemblance. The variations in results demonstrate the importance of choosing the right string distance algorithm depending on the specific application, whether it be for data correction, name matching, or linguistic research.

The Jaccard distance did not perform well because it measures similarity based on the presence or absence of common character n-grams, which can be less effective for names with minor variations. This method can struggle to differentiate between names with similar but slightly rearranged characters, leading to less accurate matches compared to other distance measures that consider character order and specific edits. Consequently, we see names such as "Chirstian" and "Chirstina" inaccurately ranked as close matches.

### References
1. [Irene-arch](https://github.com/Irene-arch/Documenting_Example/blob/main/README.md)
2. [Dr. Aaron Smith](https://www.statistics.ninja/home)
3. [Baby Names Github](https://github.com/hadley/babynames)
4. [The Great Depression](https://www.federalreservehistory.org/essays/great-depression)
5. [Post-World War II Baby Boom](https://www.khanacademy.org/humanities/us-history/postwarera/postwar-era/a/the-baby-boom)
6. [Economic Challenges in the 1970s](https://www.khanacademy.org/humanities/us-history/postwarera/1970s-america/a/stagflation-and-the-oil-crisis#:~:text=Unemployment%20rates%20rose%2C%20while%20a,wage%2D%20and%20price%2Dfreezes.)
7. [Economic Stabilization (1980s-Early 2000s)](https://www.nber.org/system/files/working_papers/w22693/w22693.pdf)
8. [Great Recession (2007-2009)](https://www.federalreservehistory.org/essays/great-recession-of-200709)
