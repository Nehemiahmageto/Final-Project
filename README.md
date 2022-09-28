## FINAL PROJECT - SEGMENT 1. 

## Selected Topic: 


The Effects of COVID-19 on the Global Macroeconomy.


## Reason Why They Selected Their Topic: 


The COVID-19 pandemic has tossed the world into a state of uncertainty, not only from a health standpoint but also from an economic perspective. With global laws that have been enacted requiring many businesses to shut down early and limiting the number of people engaged in gathering activities, this has taken a toll on the level of consumption and total output that build a country’s economy. Our interest in this topic pertains to our willingness to explore the different ways and to what degree ecological forces like the global COVID-19 pandemic can affect a country’s economy both short term and long term.



## Description of Their Source of Data:


Size of data: 200 to 230 countries 


Columns: Location, Date, Total Cases, Total Deaths, Stringency Index, Population, GDP Per Capita, Human Development Index. 


Source: Mendeley Data

https://data.mendeley.com/datasets/b2wvnbnpj9/1



## Questions the Team Hopes to Answer With the Data:

1. Which countries were most and least affected by Covid-19
2. What income group the countries affected fall into?
3. Is GDP per capita a determinant of cross-country differentials in impact of Covid-19?
4. Is HDI a determinant of cross-country differentials in impact of Covid-19?
5. Is population size a determinant of cross-country differentials in impact of Covid-19?



 ## Technologies, Languages, Tools, and Algorithms Used Throughout the Project:
 
 
Excel, SQL, Python/Pandas, Tableau. 



## SEGMENT 2. 


## Description of the Communication Protocols:

- Slack Group Chat: We have a group chat in Slack that we use as our primary form of contact with each other. We collaborate effectively here because we are able to ask questions when they arise, share meaningful ideas, split tasks and give critisms when needed. Its also the best way to give reminders for the project, if we feel the need to bring up an idea or a reminder that may be beneficial to the team, we communicate that through this group chat. It is very open for all team members and is the best strategy in making sure that we are all engaged with one another. 



- Zoom Meetings: We set up 1hr Zoom meetings twice a week, every Thursdays and Saturdays, where we get to dive deeper into the requirements of the project. Here we get the chance to address issues and check in on everyone's progress. We are able to talk freely on our strengths and weaknesses on the project and collaborate together to help one another. We also get to share feedback on each person's deliverable and provide recommendations on areas of improvement. 


2.	RESULTS

(I).		DATABASE


Database page can be viewed via this link: https://github.com/AhmedFrz/Final-Project/tree/Database-setup

Data Cleaning

Data cleaning means fixing bad data in the data set.

The first thing I did was that I imported the dataset to see which of the data are bad, empty, and wrong (format) data by using the following code:

a. Loading the data

df=pd.read_csv("raw_data.csv")

df.head()

 ![image](https://user-images.githubusercontent.com/104377031/189553021-b8c61c7f-0dbb-4e1f-a469-ee7aecb4c179.png)

b. Renaming the columns

df = df.rename(columns = {'Unnamed: 9':'TC','human_development_index (HDI)':'HDI','Unnamed: 10':'TD','Unnamed: 11':'STI','Unnamed: 12':'POP','Unnamed: 13':'GDPCAP'})

df

 ![image](https://user-images.githubusercontent.com/104377031/189553054-23a6a933-6ac5-4f9c-9ef3-efe09bb5352d.png)


c. Converting #NUM to NaN

df['TC'] = pd.to_numeric(df['TC'],errors = 'coerce')

df['TD'] = pd.to_numeric(df['TD'],errors = 'coerce')

df['STI'] = pd.to_numeric(df['STI'],errors = 'coerce')

df['GDPCAP'] = pd.to_numeric(df['GDPCAP'],errors = 'coerce')

df

![image](https://user-images.githubusercontent.com/104377031/189553087-234d7a7e-f1d4-43e9-b609-984ee3b7cc79.png)

d. Checking the numbers of NaN values

df.isnull().sum()

![image](https://user-images.githubusercontent.com/104377031/189553107-23d48e00-37e7-48b6-9036-29da88bbe6df.png)
 

e. Replacing NaN values with a float

df['total_cases'] = df['total_cases'].replace(np.nan, float(0))

df['total_deaths'] = df['total_deaths'].replace(np.nan, float(0))

df['stringency_index'] = df['stringency_index'].replace(np.nan, float(0))

df['population'] = df['population'].replace(np.nan, float(0))

df['gdp_per_capita'] = df['gdp_per_capita'].replace(np.nan, float(0))

df['HDI'] = df['HDI'].replace(np.nan, float(0))

df

![image](https://user-images.githubusercontent.com/104377031/189553137-a8564c51-42f9-426e-b2fc-72dcc00ce560.png)

 

![image](https://user-images.githubusercontent.com/104377031/189553148-703b355c-85fd-419a-97ce-4bcfb2828028.png)
 


f. Replacing NaN for remaining columns

df['TC'] = df['TC'].combine_first(0 * df['total_cases'])

df['TD'] = df['TD'].combine_first(0 * df['total_deaths'])

df['STI'] = df['STI'].combine_first(0 * df['stringency_index'])

df['GDPCAP'] = df['GDPCAP'].combine_first(0 * df['gdp_per_capita'])

df.head()

![image](https://user-images.githubusercontent.com/104377031/189553179-8688c577-08c2-42b2-869d-c063bc08f5bb.png)


![image](https://user-images.githubusercontent.com/104377031/189553190-5dce7faf-52c3-43a7-8c61-9b1150ab0f57.png)
 

g. Description of the data in the dataset

df.describe()

![image](https://user-images.githubusercontent.com/104377031/189553199-d9f010ac-fe18-4aa9-95c6-d36ad2ade1ad.png)

h. Saving the cleaned data to a new file

df.to_csv("cleaned_covid_data.csv",index=False)

PgAdmin
A database named “covid_db” was created in the PgAdmin database to hold our data. Since we are working on only one dataset, we could not create an ERD for the work.

CONNECTING TO DATABASE
After creating the database the following command were used to interface the database

i. from config import db_password

ii. db_string = f"postgresql://postgres:{db_password}@127.0.0.1:5432/covid_db"

iii. engine = create_engine(db_string)

iv. df.to_sql(name='covid', con=engine)


(II).	DASHBOARD

The link to the google slide Dashboard presentation can be accessed via
https://docs.google.com/presentation/d/1-0RUuVZid_4WvvChL8Ro4bMWCxdVINVPieR12Kr9MvE/edit?usp=sharing


The link to the google slide Dashboard presentation can also be accessed via https://public.tableau.com/app/profile/sesan4767/viz/CovidAnalysis3_16634562183400/STORYBOARD?publish=yes

(III).	MACHINE LEARNING






(IV) Dashboard and Vizualization 



## Total Deaths Map
![image](Visualization/Resource/1.png)

## Total Deaths and GDPPC

![image](Visualization/Resource/2.png)


## Total Deaths and HDI

![image](Visualization/Resource/3.png)


## Total Deaths and Population 
![image](Visualization/Resource/4.png)


## Top seven affected countries 
![image](Visualization/Resource/5.png)

## Covid-19 Dashboard

![image](Visualization/Resource/6.png)






3.	SUMMARY/CONCLUSION

As seen in the analysis, the COVID-19 pandemic had a great negative impacts on the world’s economy. The maps and the charts also showed how the pandemic affected the GDP per capita, HDI and the population size generally.

Besides, having used different machine learning algorithms and calculating their mean squared error, r2 score and their max error, we can come to conclusions by inference that the decision tree algorithm is the best algorithm to be used for the prediction of covid 19 since its have r2 t0 be 0.99






