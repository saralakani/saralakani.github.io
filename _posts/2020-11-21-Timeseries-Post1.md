---
layout: post
title: Timeseries Post One
subtitle: A trial with Radio Access Network data related to LTE/5G technology
#cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/Timeseries_wikipedia.png
#share-img: /assets/img/path.jpg
tags: [Timeseries, RAN, 5G, LTE]
---

## My first deliberate project with timeseries data.
Being an electrical engineer specialized in cellular communication, I was interested to play around with the data in my field. Among different features in radio access technology, I decided to work with channel quality indicator known as **_CQI_**.
There are valuable articles in the web to learn more about CQI, but in simple words, this is a value that cellphone calculates and sends to the base station so that the base station can allocate required radio rasources accordingly. Calculation of CQI is the secret sauce of chipset makers and requires a complex algorithm and the main criteria is a measurement called Signal  to Noise Ratio _SNR_.

Simplifying the calculation complexity of CQI has become my motivaion to design a timeseries model that can learn the coordination between SNR and CQI and be able to predict the CQI accordingly.

For this very first experiment, I have found a [data set](https://crawdad.org/eurecom/elasticmon5G2019/20190828/index.html) that includes _SNR_ and _CQI_ in a **LTE/5G** RAN setting. First step is exploring data and finding useful features that I have presented in this [link](https://github.com/saralakani/TimeSeries_ML/blob/master/MovingCloserFarCloser_data_expl.ipynb).

In this timeseries data set we are intereted in are _RSRP_, _RSRQ_ which collectively represent _SNR_ value, as well as _CQI_. After some initial exploration, we see that we have 6532 timestamps. My essential exploratory pandas dataframe methods (after reading the data set into pandas dataframe) are as below which help me to do a better **Feature Selection** job:
~~~
 data.info() #shows the type of values e.g. int64
 data.corr() #shows the correlation between columns
 data.nunique() #gives insight about range of the values
 data.describe() #list the statiscical characteristics of each feature e.g. mean, std, 25%, etc
~~~ 
_corr()_ can help to reduce features in the sense that if you see two features have higher than 90% correlation, you better just use one of the two. In other words, having two features that have 90% or higher correlation cannot add helpful info for the ML model.

| date_index | rsrp	| rsrq	| wbcqi |
| :------ |:--- | :--- | :--- |
| date_index | 1.000000 | 0.204227 | 0.113856 | 0.029653 |
| rsrp | 0.204227 | 1.000000 | 0.786645 | 0.807675
| rsrq | 0.113856 | 0.786645 | 1.000000 | 0.849339
| wbcqi | 0.029653 | 0.807675 | 0.849339 | 1.000000

Visualization also helps to have a better understanding of the feature behavior. 

![_RSRP_ and _RSRQ_ versus time stamps](/assets/img/output_11_1.png "_RSRP_ and _RSRQ_ versus time stamps")

![_RSRP_ vs _CQI_](/assets/img/output_9_0.png "_RSRP_ vs _CQI_")

![_RSRQ_ vs _CQI_](/assets/img/rsrqVScqi.png "_RSRQ_ vs _CQI_")