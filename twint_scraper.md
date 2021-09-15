```python
import nest_asyncio
import twint
import pandas as pd
nest_asyncio.apply()
c = twint.Config()
```


```python
def columne_names():
    return twint.output.panda.Tweets_df.columns
def twint_to_pd(columns):
    return twint.output.panda.Tweets_df[columns]

c.Search= 'Sandy elderly'
c.Lang= 'en'
c.Pandas= True
c.Limit= 100
c.Since = '2012-10-20'
c.Until = '2012-11-02'
twint.run.Search(c)
```


```python
data= twint_to_pd(['tweet'])
```


```python
#clean_df = data.drop([0, 1,])
```


```python
#emergency_df = pd.concat([emergency_df, row])
```


```python
emergency_df["class_label"] = 'emergency'
emergency_df.rename(columns={"tweet" : "tweet_text"}, inplace=True)
```


```python
emergency_df = emergency_df.reset_index(drop=True)
```


```python
#emergency = emergency_df.drop(0, 1)
#emergency_df = emergency
```


```python
#emergency_df.to_csv('twint.csv', index=False)
```
