# Capstone Assignment | Restaurant location scouting in Mumbai
### Prabhav Pratyaksh, August 2021

## Table of Contents
1. [Introduction](#introduction)
2. [Business Problem](#Business)
3. [Data](#Data)
4. [Methodology](#Methodology)
    1. [Webscraping](#Webscraping)
    2. [Geocoding](#Geocoding)
    3. [Geographic Visualization](#Geographic)
    4. [Foursquare API call](#Foursquare)
    5. [Heatmap Visualization](#Heatmap)


## Introduction <a name="introduction"></a>

<div align="justified">Mumbai is India's second largest city and its financial capital. The city is home to around 12 million people and continues to attract thousands of migrants from rest of the country, thereby earning the moniker 'City of Dreams'. </div>
<div align="justified">The backbone of the city is indubitably its railway network, called the Mumbai Suburban Railway. The network consists of 6 lines and has an average daily ridership of around 7 million. It would not be wrong to say that the daily lives of the people in Mumbai heavily depends on the functioning of the railway network. As such, the network plays an important role in the economic progress of the city.</div> <br>
<br>

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/4/45/Mumbai_Metropolitan_Railway_Schematic_Map_%28simplified%29.svg/800px-Mumbai_Metropolitan_Railway_Schematic_Map_%28simplified%29.svg.png "Mumbai Suburban Railway Map (Image courtsey: Wikipedia)") <br>

**Fig 1.** Suburban railway network map

## Business Problem <a name="Business"></a>

<div align="justified"><p>As mentioned earlier, the daily lives of the people revolves around the functioning of the railway network. This presents multiple business opportunities for entrepreneurs who can look to set up different outlets around the railway stations in order to cater to the millions of commuters that travel daily. We will explore one such instance in this case. </p></div>

<div align="justified"><p> For this case study, we will adopt the perspective of a budding chef who wants to decide on the location of his new restaurant. Like the rest of the people in the city, he is acutely aware of the importance of railways in shuffling the people to and fro throughout the city. As such, he decides that any location that is close enough to the railway station will attract more customers and thereby make his restaurant business profitable.</p> </div>

<div align="justified"><p> However, he is also aware that he is not the only one with this particular idea and thousands, if not millions, of other budding chefs must have also thought about this idea. Therefore, he has to apply some data analytics to hone in on the location of his new restaurant. To do this, he decides on a list of simple criteria that he believes will deliver the most profits. These are: </p> </div>
  <p>1. The restaurant needs to be located near the stations on the Western line of the railway network. This is because of the higher ridership on the line compared to other lines</p>
  <p>2. The restaurnt needs to be located within the Mumbai city only, and not the adjoining suburban regions. For this purpose, he will only consider locations south of Borivali (refer map above)</p>
  <p>3. The restaurant should be within the walkable distance of the station. Therefore, locations within 500m of the station will be considered</p>
  <p>4. The restaurant will serve Indian cuisine, Chinese cuisine, and also provide some fast food snacks</p>
  <p>5. And finally, it would be ideal if the restaurant did not have any competing restaurants nearby, since they would also be vying for the same customers and will drive down his business</p>

<div align="justified"><p> With these criteria in mind, let us look at the data that will be required for the analysis. </p><div align="justified">
  
## Data <a name="Data"></a>
  
The data required for this exercise will be pretty trivial. We will use Foursquare data in conjunction with the list of the stations on the Western Line.
  
To obtain the list of the stations we will utilise this [Wikipedia link](https://en.wikipedia.org/wiki/List_of_Mumbai_Suburban_Railway_stations) to get the list of stations. Once we get that, we can use the Foursquare API to request data for different venues around the station within a 500m radius.
  
As for the tools used in Python, we installed the following libraries:
  1. Numpy
  2. Pandas
  3. Requests
  3. BeautifulSoup
  4. Geocoder
  5. Folium 
  
## Methodology <a name="Methodology"></a>
  
### Webscraping  <a name="Webscraping"></a>

As mentioned earlier in the introduction, we will be relying on the Wikipedia page to get a list of train stations on the suburban railway network. For properly scraping the relevant data and transforming it into a presentable format, we will use the BeautifulSoup library. Using some simple coding, we can extract all the stations from the table and convert it to a dataframe. The data frame looks like this:
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20Wikipedia%20page.png "Wikipedia table")

We use the html parsing capabilities of BeautifulSoup to get only the relevant fields from the above table
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20Wikipedia%20convert%20to%20dataframe.png "Dataframe of stations")
  
Now, we filer for the stations on the Western Line and then append the word "Station" to every record. The former step is done since we limit our search to only the Western line (due to higher ridership) and the latter step is done so that the geocoding of our stations can be done without ambiguity. Finally, we get the following dataframe
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20Station%20df.png "Station dataframe")
  
### Geocoding <a name="Geocoding"></a>  
  
To geocode the stations, we will use the geopy and the geocoder libraries in conjunction with the Nominatim package. This step is pretty simple and we simply pass in the station names to the function and get the coordinate data as output. However, some refinement will be needed due to the limitations of the Nominatim package. To be precise, certain stations had incorrect coordinate data as they had common names which were found in multiple countries. For such cases, we have to get the correct data by typing in the full name of the station. Once we do that, we get the following dataframe:  
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20geocoded%20stations.png "Geocoded station dataframe")
  
### Geographic Visualization <a name="Geographic"></a>  
  
In this step, we attempt to place the stations on a map of the city. Furthermore, as explained in the business problem section, we will only be concentrating on locations within a 500 metre radius of the station. To visualise this, we will draw circles around the station that denote this 500m restriction. We finally get this map 
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20second%20map.png "Map of stations on Western Line" )
  
Now we are ready to utilise the Foursquare API
  
### Foursquare API call <a name="Foursquare"></a> 
  
This step requires us to supply our client credentials for constructing the API call (these have been censored in the notebook for obious reason). For our purpose, we will explore 100 venues within a 500m radius of the stations.
  >  A point about Foursquare database: Many locations in India have not been mapped comprehensively. As such, not all stations will have 100 venues nearby. Some might just have less than 10 venues. Some don't have any data (only 28 stations have data).

 Once we make the API call and get the data, we convert it onto a presentable dataframe that looks like below
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20foursquare%20call.png "Foursquare venues near stations" )

We can also get a look at the venue categories that are populated in the Foursquare data
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20foursquare%20categories.png "Foursquare venue categories" )
  
Finally, we can create a dataframe that shows 10 most common venues near stations. This dataframe looks like this
  
  ![Alt text](https://github.com/prabhavpratyaksh/Coursera_Capstone/blob/master/Final%20Assignment/Screenshots/SS%20-%20common%20venues.png "Foursquare 10 most common venues" )
  
Now we proceed to make a heatmap that shows the locations of competing restaurants within a 500m radius
  
### Heatmap Visualization <a name="Heatmap"></a>  
  
Since our restaurant will serve only Indian cuisine, Chinese cuisine, and fast foods we will filter our dataframe to only 
