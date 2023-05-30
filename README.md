# Income Status by Zip Code Project

The purpose of this project is to understand our customer demographic and to reaaffirm that our user base reflects the mission of the company. The mission of the company is to create a more equitable alternative to outdated employment practices using equity as the starting point. 

## Project Summary: 

The goal of this project is to have a dataset with a list of Zip Codes and correspoding income statuses. When finalized this will be used as a 'look up' table to definie our users based on the Zip Code they have provided. There are multiple ways to describe income statuses: low income, very low income, and extremely low income. For this project we will be using the Low Income definition.

## Data Sets: 

There are a total of 4 data sets used during this project. 

### 1. Median Income by Zip Code 
[American Community Survey 1901 (Income in the past 12 months) - 2021, 5 Year Estimates Subject Tables](https://data.census.gov/table?q=income&g=010XX00US$8600000&tid=ACSST5Y2021.S1901)

Columns Utilized: Zip Code, Median Income 
    
### 2. Average Household Size by Zip Code 
[American Community Survey S1101 - Household and Families ](https://data.census.gov/table?q=household+size&g=0400000US06$8600000&tid=ACSST5Y2021.S1101)

Columns Utilized: Zip Code, Average Household Size

### 3. Low Income Limit by Counthy 
[The Department of Housing and Urban Development](https://www.huduser.gov/portal/datasets/HOME-Income-limits.html#data)

Columns Utilized: fips2010, lim80 1-8
- fips2010: code with a combination of different sub code categoriations. In this project we will be uing the first 5 numbers which is a categorization of state + county. 
- lim80 1-8 stands for household sizes up to 8 people with the various income limits PER household size. 


### 4. Lookup Data to Convert Zip Code - County 
[The Department of Housing and Urban Development](https://www.huduser.gov/portal/datasets/usps_crosswalk.html)

Columns Untilized: Zip Code, County


## Methodology: 

Low Income Household: 
Those with household incomes at or below 80 percent of the statewide median income 

Low Income Community:
Census tracts with median household incomes at or below 80 percent of the statewide median income.

Adjusted Median Income: .8 * median income 

![Zip Code Presentation](https://github.com/brandon-rhee/zipcode/assets/129556483/4a87357d-80f2-469c-80c2-db3af9933c80)

The diagram shows the flow of where each dataset should go. Utilizing zip codes for all datasets except for low limit by county dataset to merge each dataset with one another.

After dataset cleaning, median_income will be merged onto zip_county dataset. Utilizing this new dataset (merged_data), avg_household_size will be merged onto merged_dat and income_limit will be merged to merged_data.

After merging we have come close to finalizing the look up data. Using average household size (rounded) per zip code, we define a function that retrieves the income limit for the average household size given. This will allow us to compare the income limit based on average household size and compare the number against the adjusted median income. 

If income limit < adjusted median income that zip code is considered low income else normal income status. 


## Data challenges: 
- For zipcode to county dataset there can be instances where there are duplicate zip codes but unique counties (zip 02130) and duplicate counties, but unique zip codes (Example: county 3309).
- For income_limit dataset, there are instances where the fips state/county code have the same code but different income_limits for each household (Example: fips state/county: 25027).  

- This is important to address and be aware of because there can be instances where using this methodology will result in a zip code having income status conflicts based on the income limits used. 

- To bypass this block, for income_limit dataset we will group by fips state/county and average all the income limits. 

- After merges are done on dataset we will do the same for the merged_data by grouping by zip and averaging the low_income_limit. 










































