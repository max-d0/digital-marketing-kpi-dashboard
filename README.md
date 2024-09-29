Project Overview
========
This project provides a basic monthly performance analysis of digital media marketing campaigns during the month of February. The purpose is to provide a holistic view of February's marketing KPI's, as well as provide a cost impact analysis, and identify areas for potential optimization in budget allocation.

Interactive dashboards can be found [here](https://public.tableau.com/app/profile/max.d4182/viz/MarketingCampaignPerformanceAnalysis_17275645130830/CampaignPerformanceDashboard).

![image1](Content/page1.png)

![image2](Content/page2.png)

Summary of Insights
===========

- Social media campaigns show high conversion rates but lower-than-expected return on investment (ROI), suggesting potential inefficiencies.
- Multimedia campaigns consistently generate the highest number of impressions but exhibit significantly lower click-through rates (CTR) compared to other channels
- Influencer campaigns drive both higher lead conversion and return on investment (ROI), but cost efficiency is mixed.

Recommendations
===========
- Further analysis is warranted to explore the scalability of high-performing, cost-efficient campaigns.
- Investigation into the discrepancy between social media campaign's strong conversion rate and suboptimal cost efficiency could reveal opportunities for optimization.


```python
import pandas as pd
import numpy as np
from datetime import datetime, timedelta

df = pd.read_csv('Marketing.csv')

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>c_date</th>
      <th>campaign_name</th>
      <th>category</th>
      <th>campaign_id</th>
      <th>impressions</th>
      <th>mark_spent</th>
      <th>clicks</th>
      <th>leads</th>
      <th>orders</th>
      <th>revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2021-02-01</td>
      <td>facebook_tier1</td>
      <td>social</td>
      <td>349043</td>
      <td>148263</td>
      <td>7307.37</td>
      <td>1210</td>
      <td>13</td>
      <td>1</td>
      <td>4981.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2021-02-01</td>
      <td>facebOOK_tier2</td>
      <td>social</td>
      <td>348934</td>
      <td>220688</td>
      <td>16300.20</td>
      <td>1640</td>
      <td>48</td>
      <td>3</td>
      <td>14962.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2021-02-01</td>
      <td>google_hot</td>
      <td>search</td>
      <td>89459845</td>
      <td>22850</td>
      <td>5221.60</td>
      <td>457</td>
      <td>9</td>
      <td>1</td>
      <td>7981.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2021-02-01</td>
      <td>google_wide</td>
      <td>search</td>
      <td>127823</td>
      <td>147038</td>
      <td>6037.00</td>
      <td>1196</td>
      <td>24</td>
      <td>1</td>
      <td>2114.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2021-02-01</td>
      <td>youtube_blogger</td>
      <td>influencer</td>
      <td>10934</td>
      <td>225800</td>
      <td>29962.20</td>
      <td>2258</td>
      <td>49</td>
      <td>10</td>
      <td>84490.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>303</th>
      <td>304</td>
      <td>2021-02-28</td>
      <td>instagram_tier2</td>
      <td>social</td>
      <td>983498</td>
      <td>775780</td>
      <td>760.75</td>
      <td>1024</td>
      <td>4</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>304</th>
      <td>305</td>
      <td>2021-02-28</td>
      <td>facebook_retargeting</td>
      <td>social</td>
      <td>4387490</td>
      <td>1933</td>
      <td>224.81</td>
      <td>58</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>305</th>
      <td>306</td>
      <td>2021-02-28</td>
      <td>facebook_lal</td>
      <td>social</td>
      <td>544756</td>
      <td>25840</td>
      <td>6844.80</td>
      <td>248</td>
      <td>5</td>
      <td>1</td>
      <td>1491.0</td>
    </tr>
    <tr>
      <th>306</th>
      <td>307</td>
      <td>2021-02-28</td>
      <td>instagram_blogger</td>
      <td>influencer</td>
      <td>374754</td>
      <td>94058</td>
      <td>4845.65</td>
      <td>594</td>
      <td>12</td>
      <td>1</td>
      <td>5008.0</td>
    </tr>
    <tr>
      <th>307</th>
      <td>308</td>
      <td>2021-02-28</td>
      <td>banner_partner</td>
      <td>media</td>
      <td>39889</td>
      <td>8490000</td>
      <td>6822.62</td>
      <td>849</td>
      <td>18</td>
      <td>2</td>
      <td>7030.0</td>
    </tr>
  </tbody>
</table>
<p>308 rows × 11 columns</p>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 308 entries, 0 to 307
    Data columns (total 11 columns):
     #   Column         Non-Null Count  Dtype  
    ---  ------         --------------  -----  
     0   id             308 non-null    int64  
     1   c_date         308 non-null    object 
     2   campaign_name  308 non-null    object 
     3   category       308 non-null    object 
     4   campaign_id    308 non-null    int64  
     5   impressions    308 non-null    int64  
     6   mark_spent     308 non-null    float64
     7   clicks         308 non-null    int64  
     8   leads          308 non-null    int64  
     9   orders         308 non-null    int64  
     10  revenue        308 non-null    float64
    dtypes: float64(2), int64(6), object(3)
    memory usage: 26.6+ KB
    


```python
df.isnull().sum()
```




    id               0
    c_date           0
    campaign_name    0
    category         0
    campaign_id      0
    impressions      0
    mark_spent       0
    clicks           0
    leads            0
    orders           0
    revenue          0
    dtype: int64




```python
df.duplicated().sum()
```




    np.int64(0)




```python
df.columns = df.columns.str.replace('_', ' ').str.title()
df = df.rename(columns={'Mark Spent': 'Cost'})

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>C Date</th>
      <th>Campaign Name</th>
      <th>Category</th>
      <th>Campaign Id</th>
      <th>Impressions</th>
      <th>Cost</th>
      <th>Clicks</th>
      <th>Leads</th>
      <th>Orders</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2021-02-01</td>
      <td>facebook_tier1</td>
      <td>social</td>
      <td>349043</td>
      <td>148263</td>
      <td>7307.37</td>
      <td>1210</td>
      <td>13</td>
      <td>1</td>
      <td>4981.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2021-02-01</td>
      <td>facebOOK_tier2</td>
      <td>social</td>
      <td>348934</td>
      <td>220688</td>
      <td>16300.20</td>
      <td>1640</td>
      <td>48</td>
      <td>3</td>
      <td>14962.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2021-02-01</td>
      <td>google_hot</td>
      <td>search</td>
      <td>89459845</td>
      <td>22850</td>
      <td>5221.60</td>
      <td>457</td>
      <td>9</td>
      <td>1</td>
      <td>7981.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2021-02-01</td>
      <td>google_wide</td>
      <td>search</td>
      <td>127823</td>
      <td>147038</td>
      <td>6037.00</td>
      <td>1196</td>
      <td>24</td>
      <td>1</td>
      <td>2114.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2021-02-01</td>
      <td>youtube_blogger</td>
      <td>influencer</td>
      <td>10934</td>
      <td>225800</td>
      <td>29962.20</td>
      <td>2258</td>
      <td>49</td>
      <td>10</td>
      <td>84490.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>303</th>
      <td>304</td>
      <td>2021-02-28</td>
      <td>instagram_tier2</td>
      <td>social</td>
      <td>983498</td>
      <td>775780</td>
      <td>760.75</td>
      <td>1024</td>
      <td>4</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>304</th>
      <td>305</td>
      <td>2021-02-28</td>
      <td>facebook_retargeting</td>
      <td>social</td>
      <td>4387490</td>
      <td>1933</td>
      <td>224.81</td>
      <td>58</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>305</th>
      <td>306</td>
      <td>2021-02-28</td>
      <td>facebook_lal</td>
      <td>social</td>
      <td>544756</td>
      <td>25840</td>
      <td>6844.80</td>
      <td>248</td>
      <td>5</td>
      <td>1</td>
      <td>1491.0</td>
    </tr>
    <tr>
      <th>306</th>
      <td>307</td>
      <td>2021-02-28</td>
      <td>instagram_blogger</td>
      <td>influencer</td>
      <td>374754</td>
      <td>94058</td>
      <td>4845.65</td>
      <td>594</td>
      <td>12</td>
      <td>1</td>
      <td>5008.0</td>
    </tr>
    <tr>
      <th>307</th>
      <td>308</td>
      <td>2021-02-28</td>
      <td>banner_partner</td>
      <td>media</td>
      <td>39889</td>
      <td>8490000</td>
      <td>6822.62</td>
      <td>849</td>
      <td>18</td>
      <td>2</td>
      <td>7030.0</td>
    </tr>
  </tbody>
</table>
<p>308 rows × 11 columns</p>
</div>




```python
df['ROI'] = ((df['Revenue'] - df['Cost']) / df['Cost']) * 100
df['ROI'] = df['ROI'].map('{:.2f}%'.format)

df['CPL'] = (df['Cost'] / df['Leads'])
df['CPL'] = df['CPL'].round(2)

df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>C Date</th>
      <th>Campaign Name</th>
      <th>Category</th>
      <th>Campaign Id</th>
      <th>Impressions</th>
      <th>Cost</th>
      <th>Clicks</th>
      <th>Leads</th>
      <th>Orders</th>
      <th>Revenue</th>
      <th>ROI</th>
      <th>CPL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2021-02-01</td>
      <td>facebook_tier1</td>
      <td>social</td>
      <td>349043</td>
      <td>148263</td>
      <td>7307.37</td>
      <td>1210</td>
      <td>13</td>
      <td>1</td>
      <td>4981.0</td>
      <td>-31.84%</td>
      <td>562.11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2021-02-01</td>
      <td>facebOOK_tier2</td>
      <td>social</td>
      <td>348934</td>
      <td>220688</td>
      <td>16300.20</td>
      <td>1640</td>
      <td>48</td>
      <td>3</td>
      <td>14962.0</td>
      <td>-8.21%</td>
      <td>339.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2021-02-01</td>
      <td>google_hot</td>
      <td>search</td>
      <td>89459845</td>
      <td>22850</td>
      <td>5221.60</td>
      <td>457</td>
      <td>9</td>
      <td>1</td>
      <td>7981.0</td>
      <td>52.85%</td>
      <td>580.18</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2021-02-01</td>
      <td>google_wide</td>
      <td>search</td>
      <td>127823</td>
      <td>147038</td>
      <td>6037.00</td>
      <td>1196</td>
      <td>24</td>
      <td>1</td>
      <td>2114.0</td>
      <td>-64.98%</td>
      <td>251.54</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2021-02-01</td>
      <td>youtube_blogger</td>
      <td>influencer</td>
      <td>10934</td>
      <td>225800</td>
      <td>29962.20</td>
      <td>2258</td>
      <td>49</td>
      <td>10</td>
      <td>84490.0</td>
      <td>181.99%</td>
      <td>611.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['CPC'] = (df['Cost'] / df['Clicks'])
df['CPC'] = df['CPC'].map('{:.2f}'.format)

df['Lead Conversion Rate'] = ((df['Leads'] / df['Clicks']) * 100)
df['Lead Conversion Rate'] = df['Lead Conversion Rate'].map('{:.2f}%'.format)

df['CTR'] = ((df['Clicks'] / df['Impressions']) * 100)
df['CTR'] = df['CTR'].map('{:.2f}%'.format)

df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>C Date</th>
      <th>Campaign Name</th>
      <th>Category</th>
      <th>Campaign Id</th>
      <th>Impressions</th>
      <th>Cost</th>
      <th>Clicks</th>
      <th>Leads</th>
      <th>Orders</th>
      <th>Revenue</th>
      <th>ROI</th>
      <th>CPL</th>
      <th>CPC</th>
      <th>Lead Conversion Rate</th>
      <th>CTR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2021-02-01</td>
      <td>facebook_tier1</td>
      <td>social</td>
      <td>349043</td>
      <td>148263</td>
      <td>7307.37</td>
      <td>1210</td>
      <td>13</td>
      <td>1</td>
      <td>4981.0</td>
      <td>-31.84%</td>
      <td>562.11</td>
      <td>6.04</td>
      <td>1.07%</td>
      <td>0.82%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2021-02-01</td>
      <td>facebOOK_tier2</td>
      <td>social</td>
      <td>348934</td>
      <td>220688</td>
      <td>16300.20</td>
      <td>1640</td>
      <td>48</td>
      <td>3</td>
      <td>14962.0</td>
      <td>-8.21%</td>
      <td>339.59</td>
      <td>9.94</td>
      <td>2.93%</td>
      <td>0.74%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2021-02-01</td>
      <td>google_hot</td>
      <td>search</td>
      <td>89459845</td>
      <td>22850</td>
      <td>5221.60</td>
      <td>457</td>
      <td>9</td>
      <td>1</td>
      <td>7981.0</td>
      <td>52.85%</td>
      <td>580.18</td>
      <td>11.43</td>
      <td>1.97%</td>
      <td>2.00%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2021-02-01</td>
      <td>google_wide</td>
      <td>search</td>
      <td>127823</td>
      <td>147038</td>
      <td>6037.00</td>
      <td>1196</td>
      <td>24</td>
      <td>1</td>
      <td>2114.0</td>
      <td>-64.98%</td>
      <td>251.54</td>
      <td>5.05</td>
      <td>2.01%</td>
      <td>0.81%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2021-02-01</td>
      <td>youtube_blogger</td>
      <td>influencer</td>
      <td>10934</td>
      <td>225800</td>
      <td>29962.20</td>
      <td>2258</td>
      <td>49</td>
      <td>10</td>
      <td>84490.0</td>
      <td>181.99%</td>
      <td>611.47</td>
      <td>13.27</td>
      <td>2.17%</td>
      <td>1.00%</td>
    </tr>
  </tbody>
</table>
</div>




```python
def random_time_by_category(category):
    time_ranges = {
        'social': (9, 21),
        'email': (7, 12),
        'search': (6, 23)
    }
    
    start_hour, end_hour = time_ranges.get(category, (9, 18))
    
    random_hour = np.random.randint(start_hour, end_hour)
    random_minute = np.random.randint(0, 60)
    random_second = np.random.randint(0, 60)
    
    return timedelta(hours=random_hour, minutes=random_minute, seconds=random_second)

df['Time'] = df['Category'].apply(random_time_by_category)

df['Time'] = df['Time'].apply(lambda x: (pd.to_datetime(x.total_seconds(), unit='s').strftime('%I:%M:%S %p')))

df['Date:Time'] = pd.to_datetime(df['C Date'] + ' ' + df['Time'], format='%Y-%m-%d %I:%M:%S %p')

cols = list(df.columns)
cols.remove('Date:Time')
cols.insert(1, 'Date:Time')
df = df[cols]

to_delete = ['C Date', 'Time']
df = df.drop(columns=to_delete)

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Date:Time</th>
      <th>Campaign Name</th>
      <th>Category</th>
      <th>Campaign Id</th>
      <th>Impressions</th>
      <th>Cost</th>
      <th>Clicks</th>
      <th>Leads</th>
      <th>Orders</th>
      <th>Revenue</th>
      <th>ROI</th>
      <th>CPL</th>
      <th>CPC</th>
      <th>Lead Conversion Rate</th>
      <th>CTR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2021-02-01 13:07:45</td>
      <td>facebook_tier1</td>
      <td>social</td>
      <td>349043</td>
      <td>148263</td>
      <td>7307.37</td>
      <td>1210</td>
      <td>13</td>
      <td>1</td>
      <td>4981.0</td>
      <td>-31.84%</td>
      <td>562.11</td>
      <td>6.04</td>
      <td>1.07%</td>
      <td>0.82%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2021-02-01 18:54:41</td>
      <td>facebOOK_tier2</td>
      <td>social</td>
      <td>348934</td>
      <td>220688</td>
      <td>16300.20</td>
      <td>1640</td>
      <td>48</td>
      <td>3</td>
      <td>14962.0</td>
      <td>-8.21%</td>
      <td>339.59</td>
      <td>9.94</td>
      <td>2.93%</td>
      <td>0.74%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2021-02-01 09:10:33</td>
      <td>google_hot</td>
      <td>search</td>
      <td>89459845</td>
      <td>22850</td>
      <td>5221.60</td>
      <td>457</td>
      <td>9</td>
      <td>1</td>
      <td>7981.0</td>
      <td>52.85%</td>
      <td>580.18</td>
      <td>11.43</td>
      <td>1.97%</td>
      <td>2.00%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2021-02-01 20:44:58</td>
      <td>google_wide</td>
      <td>search</td>
      <td>127823</td>
      <td>147038</td>
      <td>6037.00</td>
      <td>1196</td>
      <td>24</td>
      <td>1</td>
      <td>2114.0</td>
      <td>-64.98%</td>
      <td>251.54</td>
      <td>5.05</td>
      <td>2.01%</td>
      <td>0.81%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2021-02-01 11:34:45</td>
      <td>youtube_blogger</td>
      <td>influencer</td>
      <td>10934</td>
      <td>225800</td>
      <td>29962.20</td>
      <td>2258</td>
      <td>49</td>
      <td>10</td>
      <td>84490.0</td>
      <td>181.99%</td>
      <td>611.47</td>
      <td>13.27</td>
      <td>2.17%</td>
      <td>1.00%</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>303</th>
      <td>304</td>
      <td>2021-02-28 12:45:52</td>
      <td>instagram_tier2</td>
      <td>social</td>
      <td>983498</td>
      <td>775780</td>
      <td>760.75</td>
      <td>1024</td>
      <td>4</td>
      <td>0</td>
      <td>0.0</td>
      <td>-100.00%</td>
      <td>190.19</td>
      <td>0.74</td>
      <td>0.39%</td>
      <td>0.13%</td>
    </tr>
    <tr>
      <th>304</th>
      <td>305</td>
      <td>2021-02-28 10:19:07</td>
      <td>facebook_retargeting</td>
      <td>social</td>
      <td>4387490</td>
      <td>1933</td>
      <td>224.81</td>
      <td>58</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-100.00%</td>
      <td>inf</td>
      <td>3.88</td>
      <td>0.00%</td>
      <td>3.00%</td>
    </tr>
    <tr>
      <th>305</th>
      <td>306</td>
      <td>2021-02-28 16:57:46</td>
      <td>facebook_lal</td>
      <td>social</td>
      <td>544756</td>
      <td>25840</td>
      <td>6844.80</td>
      <td>248</td>
      <td>5</td>
      <td>1</td>
      <td>1491.0</td>
      <td>-78.22%</td>
      <td>1368.96</td>
      <td>27.60</td>
      <td>2.02%</td>
      <td>0.96%</td>
    </tr>
    <tr>
      <th>306</th>
      <td>307</td>
      <td>2021-02-28 12:39:57</td>
      <td>instagram_blogger</td>
      <td>influencer</td>
      <td>374754</td>
      <td>94058</td>
      <td>4845.65</td>
      <td>594</td>
      <td>12</td>
      <td>1</td>
      <td>5008.0</td>
      <td>3.35%</td>
      <td>403.80</td>
      <td>8.16</td>
      <td>2.02%</td>
      <td>0.63%</td>
    </tr>
    <tr>
      <th>307</th>
      <td>308</td>
      <td>2021-02-28 17:53:21</td>
      <td>banner_partner</td>
      <td>media</td>
      <td>39889</td>
      <td>8490000</td>
      <td>6822.62</td>
      <td>849</td>
      <td>18</td>
      <td>2</td>
      <td>7030.0</td>
      <td>3.04%</td>
      <td>379.03</td>
      <td>8.04</td>
      <td>2.12%</td>
      <td>0.01%</td>
    </tr>
  </tbody>
</table>
<p>308 rows × 16 columns</p>
</div>




```python
df.to_csv('Marketing_modified.csv', index=False)
```

