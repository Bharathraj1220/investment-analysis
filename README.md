# investment-analysis
Spark Funds, an asset management company, wants to make investments in a few companies. The CEO of Spark Funds wants to understand the global trends in investments so that she can take the investment decisions effectively.

### Business and Data Understanding
Spark Funds has two minor constraints for investments:

- It wants to invest between 5 to 15 million USD per round of investment
- It wants to invest only in English-speaking countries because of the ease of communication with the companies it would invest in
- For our analysis, consider a country to be English speaking only if English is one of the official languages in that country
- List of countries where English is an official language: https://en.wikipedia.org/wiki/List_of_countries_and_territories_where_English_is_an_official_language

These conditions will give sufficient information for our initial analysis. Before getting to specific questions, let’s understand the problem and the data first.

#### 1. What is the strategy?
Spark Funds wants to invest where most other investors are investing. This pattern is often observed among early stage startup investors.

#### 2. Where did we get the data from?
The investment data was taken from crunchbase.com, so the insights we get may be incredibly useful. For this assignment, we have divided the data into the following files:
1. companies.csv
2. mapping.csv
3. rounds2.csv
#### 3. What is Spark Funds’ business objective?
The business objectives and goals of data analysis are pretty straightforward.

- **Business objective**: The objective is to identify the best sectors, countries, and a suitable investment type for making investments. The overall strategy is to invest where others are investing, implying that the 'best' sectors and countries are the ones 'where most investors are investing'.
- **Goals of data analysis**:
  - **Investment type analysis**: Comparing the typical investment amounts in the venture, seed, angel, private equity etc. so that Spark Funds can choose the type that is best suited for their strategy.
  - **Country analysis**: Identifying the countries which have been the most heavily invested in the past. These will be Spark Funds’ favourites as well.
  - **Sector analysis**: Understanding the distribution of investments across the eight main sectors. (Note that we are interested in the eight 'main sectors' provided in the mapping file. The two files — companies and rounds2 — have numerous sub-sector names; hence, we need to map each sub-sector to its main sector.)

### Checkpoint 1: Data Cleaning 1
Load the companies and rounds data into two data frames and name them companies and rounds2 respectively.

#### Table 1.1: Understand the Data Set
Results Expected: Table 1.1

1. How many unique companies are present in rounds2?
2. How many unique companies are present in companies?	                       
3. In the companies data frame, which column can be used as the unique key for each company?	 
4. Are there any companies in the rounds2 file which are not present in companies?	 
5. Merge the two data frames so that all variables (columns) in the companies frame are added to the rounds2 data frame. Name the merged frame master_frame. How many observations are present in master_frame?

### Checkpoint 2: Funding Type Analysis
This is the first of the three goals of data analysis – investment type analysis.

The funding types such as seed, venture, angel, etc. depend on the type of the company (startup, corporate, etc.), its stage (early stage startup, funded startup, etc.), the amount of funding (a few million USD to a billion USD), and so on. For example, seed, angel and venture are three common stages of startup funding.

- Seed/angel funding refer to early stage startups whereas venture funding occurs after seed or angel stage/s and involves a relatively higher amount of investment.
- Private equity type investments are associated with much larger companies and involve much higher investments than venture type. Startups which have grown in scale may also receive private equity funding. This means that if a company has reached the venture stage, it would have already passed through the angel or seed stage/s.
 
**Spark Funds wants to choose one of these four investment types for each potential investment they will make.**

Considering the constraints of Spark Funds, you have to decide one funding type which is most suitable for them.

1. Calculate the most representative value of the investment amount for each of the four funding types (venture, angel, seed, and private equity)
2. Based on the most representative investment amount calculated above, which investment type do you think is the most suitable for Spark Funds?

Considering that Spark Funds wants to invest between **5 to 15 million USD** per investment round, which investment type is the most suitable for it? Identify the investment type and, for further analysis, filter the data so it only contains the chosen investment type.

### Checkpoint 3: Country Analysis
This is the second goal of analysis — country analysis.

Spark Funds wants to invest in countries with the highest amount of funding for the chosen investment type. This is a part of its broader strategy to invest where most investments are occurring.

1. Spark Funds wants to see the top nine countries which have received the highest total funding (across ALL sectors for the chosen investment type)

2. For the chosen investment type, make a data frame named top9 with the top nine countries (based on the total investment amount each country has received)

**Identify the top three English-speaking countries in the data frame top9.**

### Checkpoint 4: Sector Analysis 1
This is the third goal of analysis — sector analysis.

When we say sector analysis, we refer to one of the eight main sectors (named main_sector) listed in the mapping file (note that ‘Other’ is one of the eight main sectors). This is to simplify the analysis by grouping the numerous category lists (named ‘category_list’) in the mapping file. For example, in the mapping file, category_lists such as ‘3D’, ‘3D Printing’, ‘3D Technology’, etc. are mapped to the main sector ‘Manufacturing’.

Also, for some companies, the category list is a list of multiple sub-sectors separated by a pipe (vertical bar |). For example, one of the companies’ category_list is Application Platforms|Real Time|Social Network Media.

We need to discuss with the CEO and come up with the business rule that the first string before the vertical bar will be considered the primary sector. In the example above, ‘Application Platforms’ will be considered the primary sector.

Extract the primary sector of each category list from the category_list column

Use the mapping file 'mapping.csv' to map each primary sector to one of the eight main sectors (Note that ‘Others’ is also considered one of the main sectors)

### Checkpoint 5: Sector Analysis 2
Now, the aim is to find out the most heavily invested main sectors in each of the three countries (for funding type FT and investments range of 5-15 M USD).

- Create three separate data frames D1, D2 and D3 for each of the three countries containing the observations of funding type FT falling within the 5-15 million USD range. The three data frames should contain all the columns of the master_frame along with the main sector and the primary sector. Using the three data frames, we can calculate the total number of investments and the total amount of investments in each main sector for each of the three countries.

### Checkpoint 6: Plots
As a final step, we have to present our findings to the CEO of Spark Funds. Specifically, she wants to see the following plots:

1. A plot showing the representative amount of investment in each funding type. This chart should make it clear that a certain funding type (FT) is best suited for Spark Funds.   

2. A plot showing the top 9 countries against the total amount of investments of funding type FT. This should make the top 3 countries (Country 1, Country 2, and Country 3) very clear.

3. A plot showing the number of investments in the top 3 sectors of the top 3 countries on one chart (for the chosen investment type FT). This plot should clearly display the top 3 sectors each in Country 1, Country 2, and Country 3.
