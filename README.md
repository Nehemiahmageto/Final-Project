# Final-Project

Database page can be viewed via this link: https://github.com/AhmedFrz/Final-Project/tree/Database-setup

DATABASE/FINAL-PROJECT

1.	Data Cleaning

Data cleaning means fixing bad data in the data set. 

The first thing I did was that I imported the dataset to see which of the data are bad, empty, and wrong (format) data by using the following code:

a.	Loading the data

df=pd.read_csv("raw_data.csv")

df.head()

 ![image](https://user-images.githubusercontent.com/104377031/189553021-b8c61c7f-0dbb-4e1f-a469-ee7aecb4c179.png)


b.	Renaming the columns

df = df.rename(columns = {'Unnamed: 9':'TC','human_development_index (HDI)':'HDI','Unnamed: 10':'TD','Unnamed: 11':'STI','Unnamed: 12':'POP','Unnamed: 13':'GDPCAP'})

df

 ![image](https://user-images.githubusercontent.com/104377031/189553054-23a6a933-6ac5-4f9c-9ef3-efe09bb5352d.png)


c.	Converting #NUM to NaN

df['TC'] = pd.to_numeric(df['TC'],errors = 'coerce')

df['TD'] = pd.to_numeric(df['TD'],errors = 'coerce')

df['STI'] = pd.to_numeric(df['STI'],errors = 'coerce')

df['GDPCAP'] = pd.to_numeric(df['GDPCAP'],errors = 'coerce')

df

![image](https://user-images.githubusercontent.com/104377031/189553087-234d7a7e-f1d4-43e9-b609-984ee3b7cc79.png)
 

d.	Checking the numbers of NaN values

df.isnull().sum()

![image](https://user-images.githubusercontent.com/104377031/189553107-23d48e00-37e7-48b6-9036-29da88bbe6df.png)
 

e.	Replacing NaN values with a float

df['total_cases'] = df['total_cases'].replace(np.nan, float(0))

df['total_deaths'] = df['total_deaths'].replace(np.nan, float(0))

df['stringency_index'] = df['stringency_index'].replace(np.nan, float(0))

df['population'] = df['population'].replace(np.nan, float(0))

df['gdp_per_capita'] = df['gdp_per_capita'].replace(np.nan, float(0))

df['HDI'] = df['HDI'].replace(np.nan, float(0))

df

![image](https://user-images.githubusercontent.com/104377031/189553137-a8564c51-42f9-426e-b2fc-72dcc00ce560.png)

 

![image](https://user-images.githubusercontent.com/104377031/189553148-703b355c-85fd-419a-97ce-4bcfb2828028.png)
 


f.	Replacing NaN for remaining columns

df['TC'] = df['TC'].combine_first(0 * df['total_cases'])

df['TD'] = df['TD'].combine_first(0 * df['total_deaths'])

df['STI'] = df['STI'].combine_first(0 * df['stringency_index'])

df['GDPCAP'] = df['GDPCAP'].combine_first(0 * df['gdp_per_capita'])

df.head()


 
![image](https://user-images.githubusercontent.com/104377031/189553179-8688c577-08c2-42b2-869d-c063bc08f5bb.png)


![image](https://user-images.githubusercontent.com/104377031/189553190-5dce7faf-52c3-43a7-8c61-9b1150ab0f57.png)
 


g.	Description of the data in the dataset

df.describe()

 
![image](https://user-images.githubusercontent.com/104377031/189553199-d9f010ac-fe18-4aa9-95c6-d36ad2ade1ad.png)



h.	Saving the cleaned data to a new file

df.to_csv("cleaned_covid_data.csv",index=False)

2.	PgAdmin

A database named “covid_db” was created in the PgAdmin database to hold our data. Since we are working on only one dataset, we could not create an ERD for the work.

3.	CONNECTING TO DATABASE

After creating the database the following command were used to interface the database

i.	from config import db_password

ii.	db_string = f"postgresql://postgres:{db_password}@127.0.0.1:5432/covid_db"

iii.	engine = create_engine(db_string)

iv.	df.to_sql(name='covid', con=engine)
