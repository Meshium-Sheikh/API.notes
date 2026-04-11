## cell 1 & cell 2
---
### Cell 1
---
```python
# cell 1
import requests
# ISO3 to ISO2 conversion for World Bank
def iso3_to_iso2(iso3):
    url = f"https://restcountries.com/v3.1/alpha/{iso3}"
    try:
        r = requests.get(url, timeout=5)
        return r.json()[0]['cca2']
    except:
        return None
# Get GDP from World Bank
def get_gdp(iso2):
    url = f"https://api.worldbank.org/v2/country/{iso2}/indicator/NY.GDP.MKTP.CD?format=json&mrv=1"
    try:
        r = requests.get(url, timeout=5)
```
#### Plan:
---
*DataFram country (ISO3) -> convert to ISO2 -> ask World Bank for GDP -> store it back*
#### Understanding
---
- dataset has iso3 codes -> converting them to iso2 : which world bank api understands
- cca2 is the ISO2 code
- steps:
1. calls the url, API returns a JSON response
2. We pull out cca2 and we get the coutry name
3. ie. "USA" --> "US"
+ Try/except is there if the country code is wrong, or the API fails or the internet drops it'd return *None* and move on instead of the program crashing.

### Cell 2
---
``` python
# cell 2
# Get unique countries only (avoid 1000s of API calls)
unique_countries = df['country_code'].dropna().unique()
country_gdp = {}
for iso3 in unique_countries:
    iso2 = iso3_to_iso2(iso3)
    if iso2:
        country_gdp[iso3] = get_gdp(iso2)
    print(f"{iso3} done")  # so you can see progress
# Map back to dataframe
df['country_gdp'] = df['country_code'].map(country_gdp)
print(df[['name', 'country_code', 'country_gdp']].head())

        data = r.json()[1]
        return data[0]['value'] if data else None
    except:
        return None
```
#### Plan:
---
1. Breaking down the URl (from cell # 1)
2. 
   worldbank.org/v2/country/ US /indicator/ NY.GDP.MKTP.CD ?format=json&mrv=1
                          ↑                    ↑                      ↑
                       country            GDP indicator          give me 1
                                                               most recent value
3. index 0 has metadata which we ignore hence [data[0]['value'] at index 1 we get the GDP number
4. nstead of calling the API for every single row (imagine 10,000 rows with only 50 unique countries — that's 10,000 API calls!), it:
5. Then .map(country_gdp) just says — "for every value in country_code, look it up in this dictionary and put the result in a new column."
#### Mental Mode
---
```
1. What do I have?        → country_code (ISO3)
2. What do I need?        → GDP (from World Bank)
3. What's the bridge?     → need ISO2 first (conversion step)
4. How do I get it?       → API call (requests.get)
5. Where is the value?    → dig into the JSON response
6. How do I do it smart?  → unique only + map back
```
- What Went Wrong
---
1. The data frame had missing values which meant that our run/except was running and we didn't get the correct data ,so now first we will drop them
```pandas ruby
df_clean = df.dropna(subset=['country_code'].copy)
df_clean['country_code'] = df_clean['country_code'].str.strip()
```
- we can use clean variable twice thats okay
- Two most variables : df_raw & df_clean
- always add .copy() : it creates a new copy from the og data without messing it
