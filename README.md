# Movies ETL
#### Developing an algorithm that will predict which low budget movies that are being released will become popular.

### Amazing Prime
Amazing Prime is the world's largest online streaming movies, TV shows online retailer. The Amazing Prime video team would like to develop and algorithm that will predict which low budget movies is being released will become popular so they can buy the streaming rights at a bargain.  

To inspire the team have some fun, and connect with the local recording community, Amazing Prime has decided to sponsor a hackathon, providing a clean set of movie data and asking participants to predict popular pictures. In data analysis, a hackathon is an event where teams of analysts collaborate to work intensively on a project, using data to solve a problem. Hackathons generally last several days and teams work around the clock on their projects.

By a member of the Amazing Prime team, we have been tasked with creating the dataset for the hacketon. There are two data sources. A scraping Wikipedia from movies released since 1990 and rating data from Movie Land's website, Kaggle. 

Using Python language through Jupyter Notebook, we will extract data from both Wikipedia and Kaggle files, clean and then combine them, and finally save them into a SQL database (Figure 1) so that the hackathon participants have a nice, clean dataset to use. 


##### Figure 1: The long shot of the process

----------------------------

![0a-overall-process.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/0a-overall-process.png)

---------------------------------

#### Extracting, Transforming and Cleaning data

To create a clean and reliable dataset we need to follow the ETL process:
    
	1- extract the Wikipedia and Kaggle data from their respective files, 
	2- transform the datasets by cleaning them up and joining them together, 
	3- and load the cleaned dataset into a SQL database (Figure 2). 
	

##### Figure 2: The Extract, Transform and Load (ETL) Process

----------------------------

![0b-ETL-process.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/0b-ETL-process.png)

---------------------------------



For Amazing Prime team member, we will extract the scraped Wikipedia data stored as a JSON file, and Kaggle data stored in CSV.

Britta has determined that a SQL database is the best solution for sharing the data in the hackathon, so we'll be loading our data into a PostgreSQL table. 


Moreover, Amazing Prime loves the dataset and wants to keep it updated on a daily basis. Therefore, we have been tasked to create an automated pipeline that takes in new data, performs the appropriate transformations, and loads the data into existing tables. We will need to refactor the code from this module to create one function that takes in the three files—Wikipedia data, Kaggle metadata, and the MovieLens rating data—and performs the ETL process by adding the data to a PostgreSQL database.


### Part A: Writing an ETL Function to Read the Three Data Files

To perform the task, an ETL function was written to read the three data files including two csv and a json file (respectively, kaggle_file, ratings_file, and wiki_file,)

Upon running the function, the dataframes were checked to see if they had been correctly imported. 

The Wikipedia movie data frame is shown in Figure 3.  There are 193 columns in this file many of which might have data we don not need for our analysis or little to no data at all.


##### Figure 3: Wikipedia movie data frame

-------------------------------

![1a-wiki-movie-df.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/1a-wiki-movie-df.png)


-------------------------------


The Kaggle movie dataframe is more polished and it contains 24 columns (Figure 4)



##### Figure 4: Kaggle movie data frame

-------------------------------

![1b-kaggle-metadata.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/1b-kaggle-metadata.png)


-------------------------------


Head of the movie ratings file and its columns is shown in Figure 5.


#####Figure 5: Movie ratings 

-------------------------------

![1c-ratings.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/1c-ratings.png)


-------------------------------


####Merging Wikipedia and Kaggle Metadata

Since we wanted to keep everything in movies_df, we used a left merge to get the needed data for the hackaton. 



###Handling Alternative Titles

In the cleaning process we worked on the files we had received and kept the columns that had useful data for the competition and the compared the two files for alternative titles in columns and plotted them out to have a more solid assessment of what was going on with the data stored in similar columns. In doing so we looked for consistency in data and also outliers. The following scatter plots are just a few examples amng many similar tiles (Figure 6). 


##### Figures 6: Scatter plots of three different variables. Axis_x = Wikipedia data, Axis_y = Kaggle data


-------------------------------

![1d-scatter-plots.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/1d-scatter-plots.png)


-------------------------------
 * Yellow color is encircling an outlier in the Wikipedia release dates data.


Comparing similar columns we decided which columns were superior to similar columns in data quality and consistency to keep (Figure 7) 


##### Figure 7: Results of comparative analysis of similar columns between Wikipedia and Kaggle movie metafiles. 

-------------------------------

![1g-columns-to-keep.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/1g-columns-to-keep.png)


-------------------------------

Importing all the cleaned movies and ratings data into SQL database took some time and the results are shown in Figures 8.


#####Figure 8: Import completed by reading 26024289 rows in to the SQL database in 15203 seconds.  

--------------------------

![Del0-imported-rows-.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/Del0-imported-rows-.png)

--------------------------



##### Confirming tables imported in to the SQL database

After importing the cleaned movies (6077) and ratings data (26024289 rows) in to the SQL database two quesries were performed to confirm the data have been imported to the tables (Figures 9 and 10)   
   

#####Figure 9: Confirming data imported to movies table

--------------------------

![movies_query.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/movies_query.png)

--------------------------


#####Figure 10: Confirming data import to ratings table

--------------------------

![ratings_query.png](https://github.com/BHashemi2021/Movies-ETL/blob/main/Resources/ratings_query.png)

--------------------------


