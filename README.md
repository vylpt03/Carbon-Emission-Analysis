# Carbon-Emission-Analysis Overview  
This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends. Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.
# Data Source  
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).
# Data Overview  
The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.
#### 1. Table 'product_emissions'  
id: Identifier for each product emission record.  
company_id: Identifier for the company associated with the product.  
country_id: Identifier for the country where the product is being produced.
industry_group_id: Identifier for the industry group to which the product belongs.  
year: The year in which the emissions data was recorded.  
product_name: The name of the product associated with the emissions data.  
weight_kg: The weight of the product in kilograms.  
carbon_footprint_pcf: The carbon footprint of the product, measured in CO2 equivalent.  
upstream_percent_total_pcf: The percentage of the total carbon footprint attributed to upstream activities.  
operations_percent_total_pcf: The percentage of the total carbon footprint attributed to operations.  
downstream_percent_total_pcf: The percentage of the total carbon footprint attributed to downstream activities.  
<pre>Select * from product_emissions
limit 5;</pre>  
| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 
| 10261-1-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                      | 5.51                         | 63.84                        | 
| 10261-2-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                      | 4.51                         | 70.41                        | 
> Table 'product_emissions''s 5 first lines.
#### 2. Table 'industry_groups'  
id: Unique identifier for each industry group.  
industry_group: The name of the industry group, categorizing businesses within similar sectors based on their products or services offered. 
<pre>SELECT* FROM industry_groups
LIMIT 5;</pre>
| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 
| 4  | "Mining - Iron, Aluminum, Other Metals"                                | 
| 5  | "Pharmaceuticals, Biotechnology & Life Sciences"                       |   

<pre>SELECT COUNT(DISTINCT id) AS 'Num of industry groups' FROM industry_groups;</pre>  
| Num of industry groups | 
| ---------------------: | 
| 30                     | 
> There are 30 industry groups.

#### 3. Table 'companies'  
id: Unique identifier for each company.  
company_name: The name of the company, identifying the specific organization within the dataset.  
<pre>SELECT * FROM companies
limit 5;</pre>
| id | company_name                  | 
| -: | ----------------------------: | 
| 1  | "Autodesk, Inc."              | 
| 2  | "Casio Computer Co., Ltd."    | 
| 3  | "Cisco Systems, Inc."         | 
| 4  | "CNX Coal Resources, LP"      | 
| 5  | "Coca-Cola Enterprises, Inc." |   

<pre>SELECT COUNT(DISTINCT id) AS 'Num of companies' FROM companies;</pre>  
| Num of companies | 
| ---------------: | 
| 145              | 
> There are 145 companies.

#### 4. Table 'countries'
id: Unique identifier for each country.  
country_name: The name of the country.  
<pre>SELECT * FROM countries
LIMIT 5;
</pre>  
| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 
| 4  | Canada       | 
| 5  | Chile        |   

<pre>SELECT COUNT(DISTINCT id) AS 'Num of countries' FROM countries;</pre>  

| Num of countries | 
| ---------------: | 
| 28               | 

# Questions to research  
#### 1. Which products contribute the most to carbon emissions?  
This query attempts to find the top 10 products with the highest carbon footprint (PCF), it groups by product_name. 
<pre>SELECT product_name, 
     ROUND(AVG(carbon_footprint_pcf), 2) AS 'Average PCF'
FROM product_emissions
GROUP BY product_name
ORDER BY carbon_footprint_pcf  DESC
LIMIT 10;</pre>  
| product_name                                                                                                                       | Average PCF | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ----------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00  | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00  | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00  | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00  | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00   | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00   | 
| TCDE                                                                                                                               | 99075.00    | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00    | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00    | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00    |  
> According to the above results, the product that contributes the most to carbon emissions is the Wind Turbine G128 5 Megawatts, at roughly 3718044.00.

#### 2. What are the industry groups of these products?
This query shows the top 10 products with the highest average carbon footprint, along with their respective industry group. It groups by product and industry to correctly match each product with its emission and sector.  
<pre>SELECT 
    p.product_name AS 'Product',
    ROUND(AVG(p.carbon_footprint_pcf), 2) AS 'Average PCF',
    i.industry_group AS 'Industry Group'
FROM 
    product_emissions p
JOIN 
    industry_groups i ON p.industry_group_id = i.id
GROUP BY 
    p.product_name, i.industry_group
ORDER BY 
    AVG(p.carbon_footprint_pcf) DESC
LIMIT 10;
</pre>
| Product                                                                                                                            | Average PCF | Industry Group                     | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ----------: | ---------------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00  | Electrical Equipment and Machinery | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00  | Electrical Equipment and Machinery | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00  | Electrical Equipment and Machinery | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00  | Electrical Equipment and Machinery | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00   | Automobiles & Components           | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00   | Materials                          | 
| TCDE                                                                                                                               | 99075.00    | Materials                          | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00    | Automobiles & Components           | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00    | Automobiles & Components           | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00    | Automobiles & Components           |   
> The first four products that contribute the most to carbon emissions belong to the 'Electrical Equipment and Machinery' industry group. Followed closely by the 'Automobiles & Components' and 'Materials' industry groups. 

#### 3. What are the industries with the highest contribution to carbon emissions?  
This query calculates the sum carbon footprint per industry group and ranks them to find the top 10 industries with the highest emissions. It helps identify which sectors have the greatest environmental impact.  
<PRE>SELECT 
    i.industry_group AS 'Industry Group',
    ROUND(SUM(p.carbon_footprint_pcf), 2) AS 'SUM PCF'
FROM 
    industry_groups i
JOIN 
    product_emissions p ON p.industry_group_id = i.id
GROUP BY 
    i.industry_group
ORDER BY 
    ROUND(SUM(p.carbon_footprint_pcf),2) DESC
LIMIT 10;</PRE>  
| Industry Group                                   | SUM PCF    | 
| -----------------------------------------------: | ---------: | 
| Electrical Equipment and Machinery               | 9801558.00 | 
| Automobiles & Components                         | 2582264.00 | 
| Materials                                        | 577595.00  | 
| Technology Hardware & Equipment                  | 363776.00  | 
| Capital Goods                                    | 258712.00  | 
| "Food, Beverage & Tobacco"                       | 111131.00  | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 72486.00   | 
| Chemicals                                        | 62369.00   | 
| Software & Services                              | 46544.00   | 
| Media                                            | 23017.00   | 
> The industry group of 'Electrical Equipment and Machinery' at the top by such a significant margin, almost four times higher than the folling 'Automobiles & Components' industry groups. At the third place, 'Materials' also makes sense when the energy-intensive processes involved in producing raw materials like steel, cement, and plastics. 

#### 4. What are the companies with the highest contribution to carbon emissions?
This query finds the top 10 companies with the highest average carbon footprint based on the carbon emissions they produce. It's useful for identifying the largest corporate contributors to emissions. 
 <pre>SELECT 
    c.company_name AS 'Company',
    ROUND(AVG(p.carbon_footprint_pcf), 2) AS 'Average PCF'
FROM 
    companies c
JOIN 
    product_emissions p ON p.company_id= c.id
GROUP BY 
    c.company_name
ORDER BY 
    ROUND(AVG(p.carbon_footprint_pcf),2) DESC
LIMIT 10;</pre>  

| Company                                | Average PCF | 
| -------------------------------------: | ----------: | 
| "Gamesa Corporación Tecnológica, S.A." | 2444616.00  | 
| "Hino Motors, Ltd."                    | 191687.00   | 
| Arcelor Mittal                         | 83503.50    | 
| Weg S/A                                | 53551.67    | 
| Daimler AG                             | 43089.19    | 
| General Motors Company                 | 34251.75    | 
| Volkswagen AG                          | 26238.40    | 
| Waters Corporation                     | 24162.00    | 
| "Daikin Industries, Ltd."              | 17600.00    | 
| CJ Cheiljedang                         | 15802.83    |  
> "Gamesa Corporación Tecnológica, S.A." has an extremely high average PCF, 2444616.00. This also marks the results in questions 1, 2, and 3 when" Gamesa Corporación Tecnológica, S.A." is a turbine production company in Spain. Respectively followed by "Hino Motors, Ltd.," Arcelor Mittal, and Weg S/A, companies belong to two noticeable industry groups, 'Automobiles & Components' and 'Materials'.

##### 5. What are the countries with the highest contribution to carbon emissions?  
This query identifies the top 10 countries with the highest sum carbon footprint, reflecting where high-emission products are being manufactured. 
<pre>SELECT 
    c.country_name AS 'Country',
    ROUND(AVG(p.carbon_footprint_pcf), 2) AS 'Average PCF'
FROM 
    countries c
JOIN 
    product_emissions p ON p.country_id= c.id
GROUP BY 
    c.country_name 
ORDER BY 
    ROUND(AVG(p.carbon_footprint_pcf),2) DESC
LIMIT 10;</pre>  
| Country      | Average PCF | 
| -----------: | ----------: | 
| Spain        | 699009.29   | 
| Luxembourg   | 83503.50    | 
| Germany      | 33600.37    | 
| Brazil       | 9407.61     | 
| South Korea  | 5665.61     | 
| Japan        | 4600.26     | 
| Netherlands  | 2011.91     | 
| India        | 1535.88     | 
| USA          | 1332.60     | 
| South Africa | 1119.27     | 
> Spain leads with an average PCF of over 699,000, mainly due to the presence of Gamesa. Followed by Luxembourg, Germany, Brazil, South Korea.

#### 6. What is the trend of carbon footprints (PCFs) over the years?
This query shows the average carbon footprint for all products by year, giving a view of whether emissions are increasing or decreasing over time.  
<pre>SELECT 
  year, 
  ROUND(AVG(carbon_footprint_pcf),2) AS 'AVG PCF'
FROM product_emissions
GROUP BY year;</pre>  
| year | AVG PCF  | 
| ---: | -------: | 
| 2013 | 2399.32  | 
| 2014 | 2457.58  | 
| 2015 | 43188.90 | 
| 2016 | 6891.52  | 
| 2017 | 4050.85  |   

![image](https://github.com/user-attachments/assets/d4f3bdae-1ae9-48ca-816c-1867ce276ee6)
> 2015 recorded a record high average emission level, approximately 43.188, significantly higher than other years.

#### 7. Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?  
This query filters five selected industry groups and shows the total carbon footprint by year, allowing you to track emission trends over time per industry. It helps identify whether industries are improving or worsening in terms of sustainability.  
<pre>SELECT
  i.industry_group AS 'Industry Group',
  p.year, 
  ROUND(SUM(p.carbon_footprint_pcf),2) AS 'SUM PCF'
FROM product_emissions p
JOIN industry_groups i ON p.industry_group_id=i.id
WHERE 
  i.industry_group IN ('Electrical Equipment and Machinery',  
     'Automobiles & Components','"Pharmaceuticals,  
     Biotechnology & Life Sciences"',  
     'Capital Goods','Materials')
GROUP BY i.industry_group, p.year
ORDER BY i.industry_group, p.year DESC;</pre>  
| Industry Group                                   | year | SUM PCF    | 
| -----------------------------------------------: | ---: | ---------: | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 2014 | 40215.00   | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 2013 | 32271.00   | 
| Automobiles & Components                         | 2016 | 1404833.00 | 
| Automobiles & Components                         | 2015 | 817227.00  | 
| Automobiles & Components                         | 2014 | 230015.00  | 
| Automobiles & Components                         | 2013 | 130189.00  | 
| Capital Goods                                    | 2017 | 94949.00   | 
| Capital Goods                                    | 2016 | 6369.00    | 
| Capital Goods                                    | 2015 | 3505.00    | 
| Capital Goods                                    | 2014 | 93699.00   | 
| Capital Goods                                    | 2013 | 60190.00   | 
| Electrical Equipment and Machinery               | 2015 | 9801558.00 | 
| Materials                                        | 2017 | 213137.00  | 
| Materials                                        | 2016 | 88267.00   | 
| Materials                                        | 2014 | 75678.00   | 
| Materials                                        | 2013 | 200513.00  |  

![image](https://github.com/user-attachments/assets/78dbcb74-bf91-4d1c-a075-337f40618067)  
> Automobiles & Components: from the peak in 2016 (roundly 1.4 million) has decreased significantly compared to previous years.
Materials: emissions in 2013 (200 thousands) decreased to around 75 thousands –213 thousands in the following years.
Capital Goods has fluctuated but generally has a downward trend from 2014 onwards.

# CONCLUSIONS
#### The product plays the biggest role in carbon emissions
Wind turbines are the products that contribute the most to carbon emissions. It shows that the manufacturing and installing process of wind turbines has a very large carbon footprint, even though they are clean energy products during the use phase. For that results, although the final products are eco-friendly and sustainable, their manufactoring process some how still affect to the environment.  
#### The industries with the highest contribution to carbon emissions
It can be assumed that 'Electrical Equipment and Machinery' has the largest impact on carbon emissions because the production process requires the use of many metals, materials, and energy, especially energy from fossil fuels. But do not neglect the industry groups 'Automobiles & Components' and 'Materials', also are the leading contributor to carbon emissions.
#### The companies with the highest contribution to carbon emissions  
Although working in the renewable energy industry," Gamesa Corporación Tecnológica, S.A." is at the top of the largest carbon emissions because of its complicated production process and energy-consuming materials. Similarly, the following companies belong to 'Automobiles & Components' and 'Materials' and also contribute significantly to carbon emissions when they produce and install their products.  
#### The countries with the highest contribution to carbon emissions  
Countries with heavy industry or energy equipment manufacturing plants often have higher emissions levels.  
#### The trend of carbon footprints (PCFs) over the years (From 2013 To 2017)  
2015 recorded a record high average emission level, significantly higher than other years, mainly from fossil fuel burning and industrial activities.  
#### Demonstration of the most notable decrease in carbon footprints (PCFs) over time by industry groups  
Decreasing of carbon footprints from the industry groups shows that some industries have shown signs of improving processes or using cleaner technologies that have reduced overall emissions over time.




