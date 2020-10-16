# Location Clustering for Restaurants in Mumbai City.

<p align="middle"><img src="https://i.imgur.com/69tB8xp.png" title="source: imgur.com" width="920" heigth="600" /></p>
<p align="middle">Gateway of India - Mumbai</p>

## Introduction 
<p align="justify">
Mumbai is the most populated city in the world and fifth most densely populated city. Its is the financial capital of India and its no surprise that Mumbai is also the restaurant capital of India. The restaurant business has flourished with the local food and cuisine as well as multinational franchises. With such over-crowdedness comes cut throat competition. One of the main aspects of starting or expanding a restaurant business is choosing its location. Location of a restaurant decides the amount of traffic in a restaurant which makes it necessary to optimize.
</p>
 
<p align="justify">
A restaurant franchise owner should understand that expanding their business might be limited due to the parent company’s territorial restrictions. Parent companies do not want multiple franchises competing with each other, so spatial and geographic growth might be limited for an owner. Not only is there competition from same franchises but also from already established restaurants. Such restrictions should be considered while setting up a location. Businesses thriving in a certain neighborhood can be expanded easily in similar neighborhoods in a city. Restaurants have a very high risk associated with them while starting out in a new location. If clustering of neighborhood is possible, the restaurant would have lower risk and better chances of survival. Stepping into the highly competitive restaurant industry can be both thrilling and intimidating to new franchise owners. Being able to see the benefits, rewards, and potential failures of a neighborhood, will help prospective owners decide whether or not opening a restaurant franchise is the right decision for them. In this project we will try to find an optimal location for a restaurant. Specifically, this report will be targeted to stakeholders interested in opening an Cafe’s in Mumbai, India. Since there are lots of restaurants in Mumbai we will try to detect locations that are not already crowded with restaurants. We are also particularly interested in areas with no Cafe’s in vicinity. We would also prefer locations as close to city center as possible, assuming that first two conditions are met. 
</p>

## Data
 
<p align="justify">
Data associated with restaurants is collected using the Foursquare API. It is an excellent tool to collect venues at a given co-ordinate.The Foursquare API allows application developers to interact with the Foursquare platform. The API itself is a RESTful set of addresses to which you can send requests, so there's really nothing to download onto your server. To use the Foursquare API, we first need a list of boroughs in Mumbai along with their pin-codes. 
</p>


<p align="middle"><img src="https://i.imgur.com/CiTKbnN.png" title="source: imgur.com" /></p>
<p align="middle">Pincode Locations visualized on a Map of Mumbai</p>

<p align="justify">
After which the latitude and longitude value for the given pin-codes are required. This can be achieved by using a geocoder. We can begin our analysis by getting the details of restaurant venues in 7.5 km radius of the given location, this will ensure major parts of the city are covered without worrying about overlapping locations. Data cleaning is required to get rid of the venues which are not restaurants or venues that are not related to food. Once the resulting data frame is obtained the process of data collection can be considered complete and we can proceed with exploratory data analysis. The data-set has locations of 8500 restaurants in Mumbai along with their name and the category of restaurant.
</p>

<p align="middle"><img src="https://i.imgur.com/4r17MKb.png" title="source: imgur.com"/></p>
<p align="middle">Latitude, Longitude, Venue Information</p>

## Methodology
 
<p align="justify">
Based on definition of our problem, factors that will influence our decisions are:
</p>

- Finding a cluster of similar Neighborhoods.
- Number of existing restaurants in the neighborhood (any type of restaurant).
- Number of and distance to Cafe’s in the neighborhood, if any.
- Accessibility of neighborhood.
 
<p align="justify">
We decided to use regularly spaced grid of locations, centered around city center, to define our neighborhoods.
</p>

Following data sources will be needed to extract/generate the required information:
- Centers of candidate areas will be generated algorithmically and approximate addresses of centers of those areas will be obtained using reverse geocoding
- Number of restaurants and their type and location in every neighborhood will be obtained using Foursquare API
- Coordinates will be obtained using geocoding of well known Borough pin-codes.

## Feature Extraction
 
<p align="justify">
Relevant features have to be extracted from the data, the data-set contains noisy features like sports stadiums, scenic lookouts and monuments. Features with key words restaurant in their category have to be extracted. Extracted variables have to be converted to categorical variables,  where each category will form an attribute with binary values.
</p>

<p align="middle"><img src="https://i.imgur.com/rsGLnAS.png" title="source: imgur.com" /></p>
<p align="middle">One Hot Encoding Venue Category</p>

## Exploratory Data Analysis 
 
<p align="justify">
Exploring the data gives us valuable insights before modelling the data for machine learning. Examining the market share of various restaurants shows that Indian restaurants are the most common restaurant type in Mumbai with about 33% of the market share. People in India are very culturally rooted and prefer having food with family in familiar setting which is the reason for the popularity of Indian restaurants. But the younger generation have more inclination towards Cafe's and Coffee places. These places have trendy ambience and younger people like to hangout there after work and college with their friends. The popularity is in an upward trend with Cafe's and Coffee houses, already having a hefty market share. The market may have been saturated with Indian restaurants but there is still room left for Cafe's and Coffee places for expansion.
</p>

<p align="middle"><img src="https://i.imgur.com/zlCUoeD.png" title="source: imgur.com" /></p>
<p align="middle">Market share of restaurants in Mumbai</p>
 
<p align="justify">
Looking at common venues in each neighborhood also concludes that Indian restaurants are the most common restaurants in Mumbai, but other restaurants are gaining popularity steadily. The closest to Indian restaurants in popularity are the Cafe’s and Coffee places. When combined they cover nearly 23% of the market share. Dessert shops in India are generally sweet/confectionery shops and not restaurant per-say, but are quite popular too. 
</p>


## Modeling 

<p align="justify">
For a clustering problem the attributes with binary data are prepared. The attributes contain information about the type of restaurant in each neighborhood and how common are those restaurant. Agglomerative clustering algorithm is used to get a rough idea about the number of clusters that can be extracted from the data without losing useful information. A distance matrix is created for each point with a randomly assigned cluster centre. An agglomerative cluster can be visualized using a dendrogram. The x-axis on a dendrogram represents the distance between individual clusters. The y-axis is a list of boroughs with coloured lines indicating the cluster which it belongs. The names on the y-axis are arranged in such a manner that similar neighbors are arranged closer to each other. The affinity parameter is set to ‘l1’ and the linkage is set to ‘average’. Average uses the average of the distances of each observation of the two sets. Once we have a rough idea about the number of clusters we can tune our Kmeans model.
</p>



## Agglomerative Hierarchical clustering Technique: 
 
<p align="justify">
In this technique, initially each data point is considered as an individual cluster. At each iteration, the similar clusters merge with other clusters until one cluster or K clusters are formed. The psedocode for Agglomerative is straight forward.
</p>

- Compute the proximity matrix
- Let each data point be a cluster
- Repeat: Merge the two closest clusters and update the proximity matrix until only a single cluster remains.

<p align="middle"><img src="https://i.imgur.com/Ecpqu9d.png" title="source: imgur.com" /></p>
<p align="middle">Dendrogram from Agglomerative Clustering</p>
 
<p align="justify">
A highly co-related neighborhood with virtually zero distance between them in the distance matrix can be seen, the locations being Bazargate, Bandra, Bhawani Shankar Road, Chembur, Cotton Exchange, DM Colony, Ghatkopar, Govandi, Haji Ali, NITIE and Raj Bhavan areas. The number of clusters for Kmeans algorithm can also be optimized using the elbow method and calculating the sum of squared error among clusters and the silhouette scores of the model for different values of k. A minor elbow can be observed at k=5 in an otherwise smooth curve. 
</p>

<p align="middle"><img src="https://i.imgur.com/GJtycYj.png" title="source: imgur.com" /></p>
<p align="middle">Elbow Method to tune K-means Clustering Parameters</p>

<p align="justify">
For k=5 the neighborhoods are clustered in this manner. Even though the model wasn’t trained on any location based data, its not a surprise that closer neighborhoods are more similar to each other, this indicates a good model.
</p>

<p align="middle"><img src="https://i.imgur.com/i1jgpqc.png" title="source: imgur.com" /></p>
<p align="middle">Locations clusters for k=5</p> 
 
<p align="justify">
This group of neighborhoods have a lot in common as both Agglomerative and Kmeans clustering clustered them into the same group. Once we start out at any one of these locations it would be easier to expand in other locations. Here the overall trend is followed, that Indian restaurants are popular, other than that Dessert shops are quite popular too. Dessert shops in India tend to be Sweet shops and confectioneries, they are not a restaurant per-say but are quite popular. Lets focus on the Coffee shops and Cafe's here. The area is not saturated with it but can be seen as quite popular. Lets narrow our search on the Bandra region of the cluster. Bandra is located at the heart of the city with lot of foot traffic around it. The Bandra Kurla Complex in Bandra is considered the financial hub of the city. 
</p>

<p align="middle"><img src="https://i.imgur.com/M1eUlQ6.png" title="source: imgur.com" /></p>
<p align="middle">Neighbourhoods with very high similarity scores</p>  
 
<p align="justify">
Bandra Kurla Complex is a business and residential district in Bandra, Mumbai. It is a prominent commercial hub in India. According to MMRDA, the complex is the first of a series of "growth centers" created to "arrest further concentration" of offices and commercial activities in South Mumbai. It has aided to decongest the CBD in South Mumbai while seeding new areas of planned commercial real estate in the metropolitan region. There are approximately 400,000 people working in various offices throughout the BKC, which makes it ideal to set up a cafe. Considering a radius of around 5kms around the BKC, equidistant grid points are created about 100m apart from each other. These grid points act as potential candidates for setting up the cafe. The market share graph of Bandra indicates that Cafe’s are not as common in this region as they are in the rest of the city. This is a good indication that there is opportunity to expand in this region. Cafe, perfectly complements our chosen location.The main customers of a cafe in ascending order are, employees or Working class(Proximity to BKC),couples (married & unmarried both),youngsters (17–30)(Proximity to Mumbai University).
</p>

<p align="middle"><img src="https://i.imgur.com/ghWK3SS.png" title="source: imgur.com" /></p>
<p align="middle">Market share of restaurants in Bandra</p>   
 
<p align="justify">
The equidistant grid-points can be visualized using a map. The points stretch from Dharavi in the south to the Airport in the north. The locations abundantly cover the centre of the city. This part of the city is one of the most accessible.
</p>

<p align="middle"><img src="https://i.imgur.com/igJay4V.png" title="source: imgur.com" /></p>
<p align="middle">Grid point loactions around BKC</p>    
 
<p align="justify">
The density of  restaurants in a region can be visualized using a heat-map. It can be seen that very less area is left untouched by a restaurant, but the same map for cafe tells a completely different story. It shows that only about 15% of the restaurants are cafes. Further analysis revealed that a Cafe is at a distance of approximately 1km from each grid-point whereas a restaurant is at an average distance of 400m.
</p>

<p align="middle">
 <img src="https://i.imgur.com/hLcJsMK.png" title="source: imgur.com" />
 <img src="https://i.imgur.com/YT5zxoV.png" title="source: imgur.com" /></p>
<p align="middle">(1) Restaurant heatmap (2) Cafe heatmap</p>    

<p align="justify">
Lets further narrow our region to the place just north of BKC, where the region looks fairly empty of Cafes. This region is in the vicinity of Mumbai University. It gives an added advantage to the Cafe business due to the presence of large population of the target demographic.
</p>

<p align="middle"><img src="https://i.imgur.com/tuWt0Jv.png" title="source: imgur.com" /></p>
<p align="middle">Loaclity near Mumbai University</p>    
 
<p align="justify">
The region looks devoid of competitors. The procedure of making grid-points is repeated with slight variation. The grid-points now only cover regions where there are no Cafes in a 400m radius and no more than 2 restaurants in its vicinity. This step will ensure that the business will have little to no competition from its surroundings. The points of interest can be further clustered into regions using the k-means algorithm. The centers of the clustered locations can be considered the final suggestions for setting up a Cafe. We have created 6 addresses representing centers of zones containing locations with low number of restaurants and no Cafe’s nearby, all zones being fairly close to Bandra Kurla Complex. Although zones are shown on map with a circle, their shape is actually very irregular and their centers/addresses should be considered only as a starting point for exploring area neighborhoods in search for potential restaurant locations.
</p>

<p align="middle">
 <img src="https://i.imgur.com/JT0rF2p.png" title="source: imgur.com" />
 <img src="https://i.imgur.com/lAKQ4Yc.png" title="source: imgur.com" /></p>
<p align="middle">(1) Restaurant density heatmap with gridpoints (2) Cluster Centers with least density of restaurants</p>    


## Results and Discussion
 
<p align="justify">
The analysis shows that although there is a great number of restaurants in Mumbai (>8500 in our initial area of interest which was 7.5x7.5km around each pin-code), there are pockets of low restaurant density fairly close to Bandra Kurla Complex. Highest concentration of restaurants was detected west, south from Bandra Kurla Complex, so we focused our attention to areas north, near the Mumbai University, where a number of pockets of low restaurant density was found. After directing our attention to this more narrow area of interest (covering approx. 5x5km south-east from Bandra Kurla Complex) we first created a dense grid of location candidates (spaced 100m apart); those locations were then filtered so that those with more than two restaurants in radius of 250m and those with an Cafe’s closer than 400m were removed.Those location candidates were then clustered to create zones of interest which contain greatest number of location candidates. Addresses of centers of those zones were also generated using reverse geocoding to be used as markers/starting points for more detailed local analysis based on other factors.
</p>
 
<p align="justify">
Result of all this is 6 zones containing largest number of potential new restaurant locations based on number of and distance to existing venues - both restaurants in general and Cafe’s particularly. This, of course, does not imply that those zones are actually optimal locations for a new restaurant! Purpose of this analysis was to only provide info on areas close to Bandra Kurla Complex but not crowded with existing restaurants (particularly Cafe) - it is entirely possible that there is a very good reason for small number of restaurants in any of those areas, reasons which would make them unsuitable for a new restaurant regardless of lack of competition in the area. Recommended zones should therefore be considered only as a starting point for more detailed analysis which could eventually result in location which has not only no nearby competition but also other factors taken into account and all other relevant conditions met.
</p>

## Conclusion
 
<p align="justify">
Purpose of this project was to identify clusters similar neighborhoods in Mumbai with low number of restaurants (particularly Cafe’s) in order to aid stakeholders in narrowing down the search for optimal location for a new Cafe. Clustering Neighborhoods in Mumbai and selecting highly co-related neighborhoods which can be used in future for expansion, by calculating restaurant density distribution from Foursquare data we have first identified general boroughs that justify further analysis (Bandra), and then generated extensive collection of locations which satisfy some basic requirements regarding existing nearby restaurants. Clustering of those locations was then performed in order to create major zones of interest (containing greatest number of potential locations) and addresses of those zone centers were created to be used as starting points for final exploration by stakeholders.
Final decision on optimal restaurant location will be made by stakeholders based on specific characteristics of neighborhoods and locations in every recommended zone, taking into consideration additional factors like attractiveness of each location (proximity to park or water), levels of noise / proximity to major roads, real estate availability, prices, social and economic dynamics of every neighborhood etc.
</p>
