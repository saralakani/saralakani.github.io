---
layout: post
title: Example of dara preparation
subtitle: A trial with LTE/5G Radio Access Network data
#cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/5G_logo.png
#share-img: /assets/img/path.jpg
tags: [Data preparation, RAN, 5G, LTE, Machine learning]
---

## Where to start...
Being an electrical engineer specialized in cellular communication, I was interested to play around with the data in my field. Among different features in radio access technology, I decided to work with channel quality indicator known as **_CQI_**.
There are valuable articles in the web to learn more about CQI, but in simple words, this is a value that cellphone calculates and sends to the base station so that the base station can allocate required radio rasources accordingly. Calculation of CQI is the secret sauce of chipset makers and requires a complex algorithm and the main criteria is a measurement called Signal  to Noise Ratio _SNR_.

Simplifying the calculation complexity of CQI has become my motivaion to design a machine learning model that can learn the coordination between SNR and CQI and be able to predict the CQI accordingly.

## Data Exploration

For this very first experiment, I have found a [data set](https://crawdad.org/eurecom/elasticmon5G2019/20190828/index.html) that includes _SNR_ and _CQI_ in a **LTE/5G** RAN setting. The data is recorded in a scenario with one eNB and a single mobile User Equipment (UE) in five different mobility scenarios by following different motions and distance patterns relative to the eNB. I have chosen the data record where the UE  moves  back and forth  relative to  the  eNB, from  a  0 distance up to approximately 10 meters. Another important note is that the UE used for this data set is an Android v8.0 (Oreo) Nexus 6P phone connected to an eNB (carrier band 7). In this data set we are intereted in _RSRP_, _RSRQ_ which collectively represent _SNR_ value, as well as _CQI_. Check this [read](https://www.cablefree.net/wirelesstechnology/4glte/rsrp-rsrq-measurement-lte/#:~:text=In%20LTE%20network%2C%20a%20UE,(Reference%20Signal%20Received%20Quality).&text=The%20RSRQ%20measurement%20provides%20additional,handover%20or%20cell%20reselection%20decision.) to get some info on _RSRP_ and _RSRQ_.
Based on the [documantation](https://www.researchgate.net/publication/337103962_Dataset_of_4G_and_5G_RAN_monitoring_data_collected_using_ElasticMon_5G_monitoring_framework_over_FlexRan) of this data set, _CQI_ value is sometimes erroneous and needs to be corrected using median or mean of the neighboring rows. I plotted that value versus time which gives me a good visibility of what outliers look like.

![_CQI_ outliers](/assets/img/CQI_outliers.png "CQI versus time stamp")

I use the following code to replace outliers:

~~~
 #replacing outliers, note that it can be seen that the wbcqi=0 is outside of the normal #pattern. So we take it as outlier and replace it with mean of wbcqi value in two #neighboring rows
 outlier_index=list(data2[data2['wbcqi']==0].index)
 for i in outlier_index:
    data2.iloc[i]['wbcqi']=abs(0.5*(data2.iloc[i-1]['wbcqi']+data2.iloc[i+1]['wbcqi'] ))
~~~

![_CQI_ outliers1](/assets/img/wbcqi_ouliers1.png "CQI versus time stamp after first round")

You can see that _CQI_ is almost following a considtent pattern except one point which is _CQI_=6. Let's clean that out too. Now here is our _CQI_ values ready for the ML model.

![_CQI_ outliers2](/assets/img/wbcqi_ouliers2.png "CQI versus time stamp after second round")


You can check out more details of exploring data and finding useful features that I have presented in this [notebook](https://github.com/saralakani/ML_RAN/blob/master/4gV5gRAN.data_exp.ipynb).

My essential toolbox of exploratory pandas dataframe methods (after reading the data set into pandas dataframe) are listed below which help me to do a better **Feature Selection** job:
~~~
 data.info() #shows the type of values e.g. int64
 data.corr() #shows the correlation between columns
 data.nunique() #gives insight about range of the values
 data.describe() #list the statiscical characteristics of each feature e.g. mean, std, 25%, etc
~~~ 
Method _corr()_ can help to reduce features in the sense that if you see two features have higher than 90% correlation, you better just use one of the two. In other words, having two features that have 90% or higher correlation cannot add helpful info for the ML model.

|  | rsrp	| rsrq	| wbcqi |
|:--- |:--- | :--- | :--- |
| rsrp  | 1.000000 | 0.786645 | 0.807675
| rsrq | 0.786645 | 1.000000 | 0.849339
| wbcqi | 0.807675 | 0.849339 | 1.000000

Method _info()_ tells us that all the three features above are integer valuse and we have 6532 rows. Method _describe()_ can give insight of the data characteristics as well as checking if data is erroneous, like if you see the min and max values are not reasonable.

Visualization also helps to have a better understanding of the feature behavior. 

![_RSRP_ and _RSRQ_ versus CQI](/assets/img/output_11_1.png "_RSRP__ and _RSRQ_ _versus CQI")

![_RSRP_ vs _time stamp_](/assets/img/output_9_0.png "_RSRP_ vs _time stamp_")

![_RSRQ_ vs _time stamp_](/assets/img/rsrqVScqi.png "_RSRQ_ vs _time stamp_")

At this point we decide to stick to _RSRP_ and _RSRQ_ as our feature set and ignore time stamp because neiher _CQI_ calculation nor signal strenght are functions of time.

