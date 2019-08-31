# Potential Missclassifications of Chinese Imports
GateHouse Media analysis suggests companies might be miscoding to avoid tariffs.


## Methodology

1. **Data Acquisition.** 

The data is obtained from the "[U.S. Census Bureau](https://usatrade.census.gov/)." 
- choose HTS code and Imports for the type of data 
- Select all commodities with 10-digit HTS code
- Choose China for country
- Select all months in 2017 and 2018
- Select Customs Value (Gen), Customs Value (Cons), Dutiable Value and Calculated Duty

2. **Data Preparation.**

I used Python/Pandas for major data cleaning. I changed all trade values into integers for later calculation, and extracted information like month, year and HTS code into new columns using the regular expression. 

3. **Tariff Rate Calculation.** 

The original data only contain each commodity's monthly dutiable value and calculated duty. In order to get the tariff rate, I calculated: 
```
the tariff rate = [(calculated duty) / (custom value for consumption* 100)] * 100.
```

4. **Data Combination.** 

I pivoted 2017 and 2018 dataframes and merged them. So, the overall dataframe has rows of specific commodity and columns in months with suffix saying it's a duitlbe value or a tariff rate.

5. **Comparison and Match.** 

The analysis is conducted from the perspective of an exporter, who would want to decrease the export quantity of high-tariffed products and increase the export quantity of zero- or lower-tariffed products in order to maximize profits. So, if goods have increased tariff rates and decreased dutiable values, they are more vulnerable to misclassifications. On the other hand, if goods don't have increased tariff rates and have increased dutiable value, they tend to be substitutions for those goods imposed high taxations.

6. **Find Tariff Changes.** 

In order to capture the full effect of Trump's new tariff policy, I decided to use **October 2018's tariff rate**, as my major reference point, which would capture a full month worth of tariffed goods, and compare it with the tariff rates in January 2018. The time frame was chosen because Trump’s new tariff policy went into effect in July, which means that by October the full brunt of the tariff would be felt by importers. The difference of these two rates indicates the change of tariff rates. The percentage change of dutiable value was calculated as:
```
(dutibale value in October 2018)-( dutiable value in October 2017)/dutiable value in October 2017) * 100
```

7. **Group Into Classes of Goods.** 

I grouped goods with increased tariff rates and decreased dutiable values, into **class_up_decreased**, which are 1,474 groups. For goods with no-change or a decreased tariff rate and increased values, I grouped them into **class_down_increased**, which are 1,646 groups. 

8. **Find Categories with Both Good Types.** 

The final result is a table with the count of each of the two groups for every category of good — the first four digits of an HTS code. Because I am interested in classes where goods may have been displaced I looked for categories with at least four HTS codes in each group. There were 10 categories that fit this criteria.

## Notes
The entire analysis was based on the data from the U.S. Census Bureau. According to its website, the calculated duty for each commodity, one of the key factor in the analysis, is an estimated value of the real duty. There are cases, such as returned goods that are duty-free or variable rates, where the duty paid may be over- or underestimated. The data was used because it was the possible best data on Chiense imported good.

## Acknowledgements
<<<<<<< HEAD
In developing this analysis, I worked with my advisor at Columbia Graduate School of Journalism, John Templon, who is also a data reporter at BuzzFeed News. I consulted my methodology with  Gary Hufbauer, senior fellow at Peterson Institute for International Trade, Geoffrey Carliner, economics professor at Boston University, Zhi Wang, research professor at George Mason University, and Xuepeng Liu, economics professor at Kansas State University.

=======
In developing this analysis, I worked with my professor at Columbia Graduate School of Journalism, John Templon, who is also a data reporter at BuzzFeed News. I also consulted with  Gary Hufbauer, a senior fellow at Peterson Institute for International Trade, Geoffrey Carliner, an economics professor at Boston University, Zhi Wang, a research professor at George Mason University, and Xuepeng Liu, an economics professor at Kansas State University.
>>>>>>> 9e315cdbe64427656dd37f83fd46fa226035c7d2

## Contact me
Dian Zhang
dzhang@gatehousemedia.com

[Twitter](https://twitter.com/dian_zhang_)
