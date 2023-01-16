
# INTRODUCTION

In this project, we will be **analyzing**, **cleaning**, **transforming** and **visualizing** the 'The Internet Movie Database (IMDb)' movies dataset.

The IMDb is an online database of movies all around the world which consists information about statistics and information about the movies, TV shows, directors etc.

The information comes from this dataset: https://www.kaggle.com/datasets/harshitshankhdhar/imdb-dataset-of-top-1000-movies-and-tv-shows

# PROJECT TASKS

1. [Data Exploration.](#data-exploration)
2. [Data Information.](#data-information)
3. [Data Cleaning.](#data-cleaning)
4. [Data Statistics.](#data-statistics)
5. [Displaying movies with runtime more than or equal to 150 minutes.](#displaying-movies-with-runtime-more-than-or-equal-to-150-minutes)
6. [Finding the year with highest average voting.](#finding-the-year-with-highest-average-voting)
7. [Highest average revenue per year.](#highest-average-revenue-per-year)
8. [Finding average rating for each director.](#finding-average-rating-for-each-director)
9. [Extracting the Top 10 lengthy movies title and runtime.](#finding-top-10-lengthy-movies-title-and-runtime)
10. [Displaying number of movies per year.](#displaying-number-of-movies-per-year)
11. [Finding the top 5 highest rated movie title and directors.](#finding-the-top-5-highest-rated-movie-title-and-directors)
12. [Top 15 highest revenue movie titles.](#top-15-highest-revenue-movie-titles)
13. [Average rating of movies year-wise.](#average-rating-of-movies-year-wise)
14. [Observing if the ratings affect the revenue?](#observing-if-the-ratings-affect-the-revenue)
15. [Classifying movies as Excellent, Good and Average on the basis of ratings.](#classifying-movies-as-excellent-good-and-average-on-the-basis-of-ratings)
16. [Finding number of Sci-Fi movies.](#finding-number-of-sci-fi-movies)
17. [Analyzing how to many movies of each genre was made?](#analyzing-how-to-many-movies-of-each-genre-was-made)

# DATA EXPLORATION

**Importing Libraries**
```
#importing libraries
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns
```
**Read the files**
```
#importing the dataset
movie_data=pd.read_csv("IMDB-Movie-Data.csv")
```

**Extracting top 5 rows of the dataset**
```
movie_data.head(5)
```
![Top 5 dataset](https://user-images.githubusercontent.com/90107841/212729755-3ebed32a-655e-432e-be15-499424a01e77.png)

**Extracting last 5 rows of the dataset**

```
#displaying last 5 rows of the dataset
movie_data.tail(5)
```
![Screenshot 2023-01-16 222356](https://user-images.githubusercontent.com/90107841/212730829-7bf21e90-6230-4d6c-ae30-54cc48c5735a.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# DATA INFORMATION
```
#dataset shape including no. of rows and columns
movie_data.shape
```
![shape_ouput](https://user-images.githubusercontent.com/90107841/212731393-63499884-69d4-496c-90bc-4007d6205916.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
```
#information about dataset 
movie_data.info()
```

![data_infor_output](https://user-images.githubusercontent.com/90107841/212731483-119da5ac-e938-42ca-bbb0-d620f459ccf8.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# DATA CLEANING
```
#checking missing values in the dataset
print("Any missing values?",movie_data.isnull().values.any())
```
![missing_values_output](https://user-images.githubusercontent.com/90107841/212731594-763e6389-a63d-4322-aef3-bcd9901a5935.png)


```
movie_data.isnull().sum()
```
![output_missing_values_sum](https://user-images.githubusercontent.com/90107841/212731825-1fb818d2-f9a3-4612-b0f3-d0376d2abc0d.png)

```
#visualising the missing values
sns.heatmap(movie_data.isnull()
```
![heat_map_output](https://user-images.githubusercontent.com/90107841/212731853-2a72571c-8a65-4dde-ae42-78caa6c6251e.png)


```
percentage_null= movie_data.isnull().sum() * 100 / len(movie_data)
percentage_null
```
![output_null_percentage](https://user-images.githubusercontent.com/90107841/212731961-92bde461-b775-4379-898a-b3f2a4dbce2d.png)


```
#dropping missing values
movie_data.dropna(axis=0)
```
![ouput_dropped_values](https://user-images.githubusercontent.com/90107841/212732195-36ec5788-f8e1-4c07-8324-897b8db571f6.png)


![duplicate_values_print](https://user-images.githubusercontent.com/90107841/212732554-0150b2a5-180a-4c86-a4d1-f3837b5e0af4.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# DATA STATISTICS

```
#statistics about the dataset
movie_data.describe()
```
![output_movie_data](https://user-images.githubusercontent.com/90107841/212732610-57f89bac-6ca3-4600-806c-d0393a3630c8.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Displaying movies with runtime more than or equal to 150 minutes.
```
#displaying movie with runtime >= 150 minutes
movie_data[movie_data["Runtime (Minutes)"] >=150]['Title']
```
![output_more_than150](https://user-images.githubusercontent.com/90107841/212732642-3f8eba41-0dbf-4a0f-a489-fd3f6a9a31ed.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Finding the year with highest average voting.
```
#finding the year with highest average voting 
movie_data.groupby('Year')['Votes'].mean().sort_values(ascending=False)
```
![ouput_average_voting](https://user-images.githubusercontent.com/90107841/212732709-5e79a2cb-38a2-4124-834a-11e86cc3851b.png)

```
#visualsing the above result using seaborn
sns.barplot(x='Year',y='Votes',data=movie_data)
plt.title('Votes by Year')
plt.show()
```

![visual_avg_voting2](https://user-images.githubusercontent.com/90107841/212732821-a1e677a3-3cfb-4f62-8bbc-032938dd77de.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Highest average revenue per year.
```
#finding year with the highest avergae revenue
movie_data.groupby("Year")["Revenue (Millions)"].mean().sort_values(ascending=False)
```
![average_highest_rev_output](https://user-images.githubusercontent.com/90107841/212732876-5a708c5a-b50d-481e-9720-fb8e02c07e8b.png)


```
#visualising the above result
sns.barplot(x="Year",y="Revenue (Millions)", data=movie_data)
plt.title("Revenue Per Year")
plt.show()
```
![visual_average_highest_rev_output](https://user-images.githubusercontent.com/90107841/212732905-6a15f068-2627-4799-8ff0-d6c5656d0092.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Finding average rating for each director.
```
#finding average rating for each director
movie_data.groupby("Director")["Rating"].mean().sort_values(ascending=False)
```
![avg_rating_director_output](https://user-images.githubusercontent.com/90107841/212733269-e9aa58bc-f1c9-436f-83bd-07dd33b7df71.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Finding top 10 lengthy movies title and runtime.
```
#finding top 10 lengthy movies title and runtime
top10_len_runtime=movie_data.nlargest(10, "Runtime (Minutes)")[["Title", "Runtime (Minutes)"]].set_index("Title")

top10_len_runtime
```
![top10_len_movies_output](https://user-images.githubusercontent.com/90107841/212733606-33762e89-839d-498d-a5c7-7cd9d99dcf2e.png)

```
#visualising the above dataset
sns.barplot(x="Runtime (Minutes)",y=top10_len_runtime.index,data=top10_len_runtime)
plt.show()
```
![top10_len_movies visual](https://user-images.githubusercontent.com/90107841/212733656-7b8b97f9-8afb-4620-bf21-e1c06919e73c.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Displaying number of movies per year.
```
#displaying no. of movies per year
movie_data["Year"].value_counts()

```
![num_of_movies_per_year_output](https://user-images.githubusercontent.com/90107841/212733691-54e7b0e5-7ae2-42a9-ad0c-e7e50eb76b47.png)


```
#visualising the above data
sns.countplot(x="Year", data=movie_data)
plt.title("No. of movies per year")
plt.show()
```
![num_of_movies_per_year_visual2](https://user-images.githubusercontent.com/90107841/212733728-1681f1d2-03d7-4264-9fc9-0d8bc97fb200.png)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Finding the top 5 highest rated movie title and directors.

![high_rated5](https://user-images.githubusercontent.com/90107841/212733863-9da6acea-1a1e-428d-94f8-a093112202c9.png)


```
#visulaising the above data
sns.barplot(x="Rating", y=highest_rated5.index, data=highest_rated5, hue="Director",dodge=False)
plt.legend(bbox_to_anchor=(1,1),loc=2)
plt.show()
```
![high_rated5_visual2](https://user-images.githubusercontent.com/90107841/212733937-299c8396-ec5e-491c-b8dd-96913b9a7c1f.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Top 15 highest revenue movie titles.
```
#top 15 highest revenue movie titles
high_15_revenue=movie_data.nlargest(15, "Revenue (Millions)")[["Title","Revenue (Millions)"]].set_index("Title")

high_15_revenue
```
![top15_high_rev output](https://user-images.githubusercontent.com/90107841/212734171-9ea46191-9706-40b4-94c5-424eb9dd2a2d.png)


```
#visualising the above data
sns.barplot(x="Revenue (Millions)", y=high_15_revenue.index, data=high_15_revenue)
plt.title("Top 15 Highest Revenue Movies Titles")
plt.show()
```
![top15_high_rev output_visual2](https://user-images.githubusercontent.com/90107841/212734191-7e7d8bb3-c357-4b2e-ad68-97d57cdb769d.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Average rating of movies year-wise.
```
#finding average ratings of movie year wise
movie_data.groupby("Year")["Rating"].mean().sort_values(ascending=False)
```
![avg_rating_YW_output](https://user-images.githubusercontent.com/90107841/212734230-abbcb474-4cd6-4527-bb71-83664ea0708f.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Observing if the ratings affect the revenue?
```
#observing if the ratings affect the revenue
sns.scatterplot(x="Rating",y="Revenue (Millions)", data=movie_data)
plt.title("Yes, ratings affect the revenue")
plt.show()
```
![rating_observation_visual](https://user-images.githubusercontent.com/90107841/212734277-ffd49bee-e979-48bb-896e-98c58f401e47.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Classifying movies as Excellent, Good and Average on the basis of ratings.
```
#classifying movies as Excellent, Good and Average on the basis of ratings
def rating(rating):
    if rating>=7.0:
        return "Excellent"
    elif rating>=5:
        return "Good"
    else:
        return "Average"

movie_data["Rating_Cateogory"]=movie_data["Rating"].apply(rating)

movie_data.head()
```
![rating_observation_visual3](https://user-images.githubusercontent.com/90107841/212734510-c93f975b-9917-4334-afca-361cc9d588f7.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Finding number of Sci-Fi movies.
```
#counting number of Sci-Fi movies
movie_data['Genre'].dtype
```
![sci_fi_len_output](https://user-images.githubusercontent.com/90107841/212734578-f166e2cb-4f98-4fb6-89a4-237a87deaa0f.png)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Analyzing how to many movies of each genre was made?
```
#how to many movies of each genre was made
movie_data['Genre']
```
![movie_by_genre_output](https://user-images.githubusercontent.com/90107841/212734803-8d7da51c-8ad5-4661-a29b-43aa67748b53.png)

```
#step 1 (separating each items by commas)
list_first=[]
for value in movie_data['Genre']:
    list_first.append(value.split(',')) #separating items by ',' and adding to list_first
    
list_first
```
![movie_by_genre2](https://user-images.githubusercontent.com/90107841/212734905-e0295d75-2ed0-4a21-a1dd-9cf5bac2f8f9.png)


```
#since list_first is two-dimensional, it needs to be converted in one-dimensional
oneD_list=[]
for item1 in list_first:
    for item in item1:
        oneD_list.append(item)
        
oneD_list
```
![movie_by_genre4](https://user-images.githubusercontent.com/90107841/212734956-1d4cc5be-4b8b-4535-903c-f8efb04f3d05.png)


```
from collections import Counter
Counter(oneD_list)
```
![movie_by_genre6](https://user-images.githubusercontent.com/90107841/212734989-b6152823-8738-4f27-aff7-ea772f141ebb.png)

