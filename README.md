# Text-Analytics-String-Distances

## Table of Contents

- [Project Goals](#project-goals)
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

##

#### Correlation Table & Plot for each method

|           | lcs    | lv     | osa    | dl     | qgram  | jw     | jaccard | cosine | soundex |
|-----------|--------|--------|--------|--------|--------|--------|---------|--------|---------|
| lcs       | 1.000  | 0.772  | 0.771  | 0.772  | 0.781  | 0.474  | 0.570   | 0.587  | 0.179   |
| lv        | 0.772  | 1.000  | 0.994  | 0.991  | 0.670  | 0.625  | 0.605   | 0.637  | 0.197   |
| osa       | 0.771  | 0.994  | 1.000  | 0.997  | 0.674  | 0.628  | 0.614   | 0.645  | 0.200   |
| dl        | 0.772  | 0.991  | 0.997  | 1.000  | 0.679  | 0.631  | 0.620   | 0.650  | 0.201   |
| qgram     | 0.781  | 0.670  | 0.674  | 0.679  | 1.000  | 0.535  | 0.853   | 0.835  | 0.138   |
| jw        | 0.474  | 0.625  | 0.628  | 0.631  | 0.535  | 1.000  | 0.626   | 0.676  | 0.120   |
| jaccard   | 0.570  | 0.605  | 0.614  | 0.620  | 0.853  | 0.626  | 1.000   | 0.882  | 0.193   |
| cosine    | 0.587  | 0.637  | 0.645  | 0.650  | 0.835  | 0.676  | 0.882   | 1.000  | 0.122   |
| soundex   | 0.179  | 0.197  | 0.200  | 0.201  | 0.138  | 0.120  | 0.193   | 0.122  | 1.000   |

<div align="center">
  <img src="https://github.com/DJScully02/Text-Analytics-String-Distances/assets/129353692/b3e0a3f7-3542-4e93-8b35-f99e527c0846" alt="Correlation Plot" style="width: 45%; margin: 10px;">
</div>

### References
1. [Irene-arch](https://github.com/Irene-arch/Documenting_Example/blob/main/README.md)
2. [Dr. Aaron Smith](https://www.statistics.ninja/home)
