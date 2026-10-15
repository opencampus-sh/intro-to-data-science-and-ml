# Datasets

| Folder | Content | Used in |
| --- | --- | --- |
| [`bakery/`](bakery/) | **Course project:** daily turnover of a bakery branch per product group, weather data and Kiel Week dates. Full documentation in [bakery/README.md](bakery/README.md). | Weeks 1–10, team project, Kaggle competition |
| [`pedestrians_kiel/`](pedestrians_kiel/) | Pedestrian counts in Kiel's Holstenstraße per day and per hour (05.05.2020 – 03.01.2022) with temperature and weather condition. Separator `;`. | Preparation, week 5 |
| [`house_pricing/`](house_pricing/) | House sales with property characteristics (bedrooms, living area, condition, …), split into training and test data | Weeks 6 and 8 |
| [`airquality/`](airquality/) | Daily air quality measurements in New York, May – September 1973 (classic R dataset `airquality`, contains missing values) | Week 9 |

Load a file directly from GitHub, so that it also works in your team repository or in Google Colab:

```python
import pandas as pd

pd.read_csv("https://raw.githubusercontent.com/opencampus-sh/intro-to-data-science-and-ml/main/data/bakery/wetter.csv")
```

Please do not change the files in this folder. Save derived or cleaned data in your own repository.
