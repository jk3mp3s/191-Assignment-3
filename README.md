# Sony PS5 Price Analysis
By:

Daniel Dean: dcdean

Kempes Pandey: sumantra

Pranav Penmetsa: nagapran

![image](https://github.com/user-attachments/assets/236569b6-dd23-46af-a8a0-c1394cc286eb)

<strong><span style="font-size:30px;">Introduction:</span></strong>

The Sony PS5 is a globally popular gaming console, highly sought after by gamers worldwide. However, its price varies significantly across countries, influenced by factors such as import taxes, currency exchange rates, local market demand, and purchasing power. As avid gamers ourselves, we’ve noticed these disparities and wanted to delve deeper into how purchasing power impacts the affordability of the PS5 in different regions. Our goal was to build a comprehensive pricing index that compares the PS5's cost across 10+ countries, including Canada, while analyzing the role of purchasing power in these price differences.

<strong><span style="font-size:30px;">Step 1 - Scrape the PS5 pricing data from the web</span></strong>
![image](https://github.com/user-attachments/assets/c5f73ae5-2f6f-4711-96b1-ab521c6a1bde)

The site <a href="https://www.theworldranking.com/statistics/160/playstation-5-prices-country/">theworldranking.com</a> contains data on the prices of the PS5 in a multitude of different countries. The data is from 2023 but it should be fine for our purposes, as our goal is more to analyze trends.

<strong><span style="font-size:30px;">Step 2 - Tidying up the data</span></strong> 

After scraping the data we wanted, we did some cleaning via the following steps

First I selected a smaller number of countries to use for our purposes. I selected 11 of the more popular countries in the world and dropped the rest.
Since all of the pricing data was given in USD, I used a function to convert it all to CAD
Since the new prices are now in CAD, I changed the column label to ‘Prices (CAD)’

This new data is stored in table called ps5_pricing.

<strong><span style="font-size:30px;">Step 3 - Scraping the currency codes</span></strong>

Using the CurrencyScoop API, I scraped and cleaned a table that contained only the countries names and the currency codes. I named this table ‘currency code’ and then I joined it with my ps5_pricing table by the country column. This produced a table containing the country, the ps5 price in CAD, and the currency code for the country. 

The problem now was that we had the currency code but the prices were still in CAD. We will fix this in the next step.

<strong><span style="font-size:30px;">Step 4 - Adding the local prices</span></strong>

Now that we have the currency code in our table, we can upload a table that contains currency conversions as with currency codes and join that with our pricing data.

I imported a file called ‘exchange rates.csv’ into a table which I called ‘exchange_rates’. This table contained currency codes as well as their conversion from CAD. Using this I wrote a function that took in a currency code and a price and converted the price from CAD to the local currency. Applying this to the ps5 pricing table, we obtained a table containing the local prices which I called ‘ps5_pricing_tbl’.

<strong><span style="font-size:30px;">Step 5 - Finding the price difference</span></strong>

Finding the price difference was simply a matter of subtracting the price of the PS5 in Canada from the price of the PS5 in every other country. The given price of the PS5 in Canada was $658.47, therefore we subtracted this from every other price.

The final table contains all the data we need for further analysis.

![image](https://github.com/user-attachments/assets/84ee9b8f-058d-4ed7-9a03-8149f0b406b0)

<strong><span style="font-size:30px;">Step 6 - Visualizing the difference</span></strong>

To visualize the difference in price we simply use the barh.() method to create a horizontal bar chart of the price differences.
![image](https://github.com/user-attachments/assets/5c2cc889-fc32-446d-a486-09620af91721)

As can be seen by the data above, Japan is the only country in which it would save money to purchase a PS5 there, although you would only save about $5 CAD. On the other hand, purchasing in China would result in an additional cost of about $520 CAD as opposed to purchasing in Canada.

<strong><span style="font-size:30px;">Step 7 - Introducing the external factor</span></strong>

We thought that purchasing power index (PPI) would be an external factor that could affect PS5 pricing in different countries. To check if this was true, I first scraped and cleaned a table from the web that contained the purchasing power indices of different currencies. I then joined this table to our ps5 pricing table. From there I created a scatter plot of the PPI vs the price difference of the PS5 for all of our chosen countries.

![image](https://github.com/user-attachments/assets/c40ad291-fab8-4cb5-8e11-3bd860c4ccd5)

Here we can see that there is indeed a correlation between PPI and the pricing difference of the PS5. Calculating the correlation coefficient of this plot, we ended up with a value of -0.75 which suggests the data is correlated relatively strongly.

<strong><span style="font-size:30px;">The Purchasing Power Index:</span></strong>

The <strong>Purchasing Power Index (PPI)</strong> measures the relative value of money in different locations or periods, showing how much goods and services a unit of currency can buy. It is calculated based on the cost of a "basket of goods and services" that reflects typical consumer spending habits, making it a useful tool for comparing the cost of living and economic conditions. The PPI helps assess disparities in living costs between regions, set fair wages, and understand economic differences globally. Unlike Purchasing Power Parity (PPP), which focuses on currency comparisons, the PPI emphasizes localized purchasing power. However, it relies on accurate price data and is influenced by inflation, making regular updates essential for reliable insights.

<strong><span style="font-size:30px;">Conclusion:</span></strong>

The graph "Purchasing Power Index vs. PS5 Pricing Difference" reveals a trend where countries with higher ps5 pricing differences  generally have smaller Purchasing Power Index. Indicating a negative correlation. This suggests that stronger currencies and greater affordability often lead to more competitive pricing. However, outliers with significant price differences despite moderate purchasing power highlight the influence of additional factors, such as import taxes, shipping costs, and local demand. The data supports the hypothesis that purchasing power plays a key role in pricing, while also suggesting that regional policies and market conditions are significant contributors to global price disparities.












