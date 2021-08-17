# Capstone Assignment | Ideal Locations for restaurant in Mumbai
### Prabhav Pratyaksh, August 2021

## Introduction

<div align="justified">Mumbai is India's second largest city and its financial capital, commercial and entertainment capital. The city is home to around 12 million people and continues to attract thousands of migrants from rest of the country, thereby earning the moniker 'City of Dreams'. </div>
<div align="justified">The backbone of the city is indubitably its railway network, called the Mumbai Suburban Railway. The network consists of 6 lines and has an average daily ridership of around 7 million. It would not be wrong to say that the daily lives of the people in Mumbai heavily depends on the functioning of the railway network. As such, the network plays an important role in the economic progress of the country.</div> <br>
<br>

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/4/45/Mumbai_Metropolitan_Railway_Schematic_Map_%28simplified%29.svg/800px-Mumbai_Metropolitan_Railway_Schematic_Map_%28simplified%29.svg.png "Mumbai Suburban Railway Map (Image courtsey: Wikipedia)") <br>

**Fig 1.** Suburban railway network map

## Business Problem

<div align="justified"><p>As mentioned earlier, the daily lives of the people revolves around the functioning of the railway network. This presents multiple business opportunities for entrepreneurs who can look to set up different outlets around the railway stations in order to cater to the millions of commuters that travel daily. We will explore one such instance in this case. </p></div>

<div align="justified"><p> For this case study, we will adopt the perspective of a budding chef who wants to decide on the location of his new restaurant. Like the rest of the people in the city, he is acutely aware of the importance of railways in shuffling the people to and fro throughout the city. As such, he decides that any location that is close enough to the railway station will attract more customers and thereby make his restaurant business profitable.</p> </div>

<div align="justified"><p> However, he is also aware that he is not the only one with this particular idea and thousands, if not millions, of other budding chefs must have also thought about this idea. Therefore, he has to apply some data analytics to hone in on the location of his new restaurant. To do this, he decides on a list of simple criteria that he believes will deliver the most profits. These are: </p> </div>
  <p>1. The restaurant needs to be located near the stations on the Western line of the railway network. This is because of the higher ridership on the line compared to other lines</p>
  <p>2. The restaurnt needs to be located within the Mumbai city only, and not the adjoining suburban regions. For this purpose, he will only consider locations south of Borivali (refer map above)</p>
  <p>3. The restaurant should be within the walkable distance of the station. Therefore, locations within 500m of the station will be considered</p>
  <p>4. The restaurant will serve Indian cuisine, Chinese cuisine, and also provide some fast food snacks</p>
  <p>5. And finally, it would be ideal if the restaurant did not have any competing restaurants nearby, since they would also be vying for the same customers and will drive down his business</p>

<div align="justified"><p> With these criteria in mind, let us look at the data that will be required for the analysis. </p><div align="justified">
  
## Data
  
The data required for this exercise will be pretty trivial. We will use Foursquare data in conjunction with the list of the stations on the Western Line.
  
To obtain the list of the stations we will utilise this [Wikipedia link](https://en.wikipedia.org/wiki/List_of_Mumbai_Suburban_Railway_stations) to get the list of stations. Once we get that, we can use the Foursquare API to request data for different venues around the station within a 500m radius.
  
  

