# Bakery sales dataset

This is the dataset of the course project: forecasting the daily sales of a bakery branch in Kiel. It was provided by [meteolytix GmbH](https://www.meteolytix.de/), a Kiel company that produces sales forecasts for bakeries and retailers based on weather, holidays, school holidays, promotions and sales history.

The dataset consists of three files that can be joined on the date:

| File | Content | Period | Rows |
| --- | --- | --- | --- |
| [`umsatzdaten_gekuerzt.csv`](umsatzdaten_gekuerzt.csv) | Daily turnover per product group | 01.07.2013 – 31.07.2018 | 9,334 |
| [`wetter.csv`](wetter.csv) | Daily weather in Kiel | 01.01.2012 – 01.08.2019 | 2,601 |
| [`kiwo.csv`](kiwo.csv) | Days of Kiel Week (Kieler Woche) | 2012 – 2019 | 72 |

The column names are in German. The tables below give the English meaning.

## Sales data – `umsatzdaten_gekuerzt.csv`

"Umsatzdaten gekürzt" means "turnover data, shortened": the data ends on 31.07.2018. The following year (01.08.2018 – 31.07.2019) is held back as test data for the Kaggle competition of the course.

| Column | English | Description |
| --- | --- | --- |
| `id` | ID | Unique key of the row in the format `YYMMDD` + product group, e.g. `1307011` = 01.07.2013, product group 1. The Kaggle test data and submissions use the same format. |
| `Datum` | date | Date (`YYYY-MM-DD`) |
| `Warengruppe` | product group | Number of the product group, see below |
| `Umsatz` | turnover | Turnover of the product group on that day (target variable of the forecast). The currency is not stated in the source. |

### Product groups (`Warengruppe`)

| Code | German | English | Notes |
| --- | --- | --- | --- |
| 1 | Brot | Bread | |
| 2 | Brötchen | Rolls | |
| 3 | Croissant | Croissants | |
| 4 | Konditorei | Confectionery | No rows on 53 days |
| 5 | Kuchen | Cakes | |
| 6 | Saisonbrot | Seasonal bread | Only sold from October to January (292 days in total) |

### Things to know

- There is one row per date and product group, and only for days with sales. On 38 days there are no sales at all, mostly public holidays such as 25/26 December, 1 January, Good Friday and 1 May. Missing combinations of date and product group are therefore not missing values in the usual sense – think about what they mean before you fill them in.
- Turnover varies strongly between product groups (from about 7 to about 1,880 per day, median about 160). Compare product groups with each other only if you take these different levels into account.

## Weather data – `wetter.csv`

| Column | English | Description |
| --- | --- | --- |
| `Datum` | date | Date (`YYYY-MM-DD`) |
| `Bewoelkung` | cloud cover | Mean cloud cover of the day in octas: 0 = clear sky, 8 = completely overcast |
| `Temperatur` | temperature | Mean temperature of the day in °C |
| `Windgeschwindigkeit` | wind speed | Mean wind speed of the day in m/s |
| `Wettercode` | weather code | Weather code of the day following the WMO code for present weather (00–99), e.g. 61 = slight continuous rain. A list of the codes with descriptions is available [here](http://www.seewetter-kiel.de/seewetter/daten_symbole.htm). |

### Things to know

- The file has no row for 169 days between 2012 and 2019; 3 of these days fall into the period of the sales data.
- `Bewoelkung` is missing on 10 days, `Wettercode` on 669 days. A missing weather code most likely means that no notable weather was reported, so it is probably *not* missing at random.
- These are observed values. For a real forecast you would only know the weather *forecast* of the next day.

## Kiel Week – `kiwo.csv`

| Column | English | Description |
| --- | --- | --- |
| `Datum` | date | Date of a Kiel Week day |
| `KielerWoche` | Kiel Week | Always `1` |

The file only contains Kiel Week days (9 per year). When you merge it with the sales data, the days without Kiel Week are missing and have to be set to `0`.

## Loading the data

```python
import pandas as pd

BASE_URL = "https://raw.githubusercontent.com/opencampus-sh/intro-to-data-science-and-ml/main/data/bakery/"

sales = pd.read_csv(BASE_URL + "umsatzdaten_gekuerzt.csv", parse_dates=["Datum"])
weather = pd.read_csv(BASE_URL + "wetter.csv", parse_dates=["Datum"])
kiel_week = pd.read_csv(BASE_URL + "kiwo.csv", parse_dates=["Datum"])

data = (
    sales.merge(weather, on="Datum", how="left")
         .merge(kiel_week, on="Datum", how="left")
)
data["KielerWoche"] = data["KielerWoche"].fillna(0).astype(int)
```

After the merge, `data` must still have exactly as many rows as `sales` (9,334).
