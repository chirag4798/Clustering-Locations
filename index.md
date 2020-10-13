## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/chirag4798/ClusteringLocations/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
## Introduction

Mumbai is the most populated city in the world and fifth most densely populated city. Its is the financial capital of India and its no surprise that Mumbai is also the restaurant capital of India. The restaurant business has flourished with the local food and cuisine as well as multinational franchises. With such over-crowdedness comes cut throat competition. One of the main aspects of starting or expanding a restaurant business is choosing its location. Location of a restaurant decides the amount of traffic in a restaurant which makes it necessary to optimize.

A restaurant franchise owner should understand that expanding their business might be limited due to the parent company’s territorial restrictions. Parent companies do not want multiple franchises competing with each other, so spatial and geographic growth might be limited for an owner. Not only is there competition from same franchises but also from already established restaurants. Such restrictions should be considered while setting up a location. Businesses thriving in a certain neighborhood can be expanded easily in similar neighborhoods in a city. Restaurants have a very high risk associated with them while starting out in a new location. If clustering of neighborhood is possible, the restaurant would have lower risk and better chances of survival. Stepping into the highly competitive restaurant industry can be both thrilling and intimidating to new franchise owners. Being able to see the benefits, rewards, and potential failures of a neighborhood, will help prospective owners decide whether or not opening a restaurant franchise is the right decision for them. In this project we will try to find an optimal location for a restaurant. Specifically, this report will be targeted to stakeholders interested in opening an Cafe’s in Mumbai, India. Since there are lots of restaurants in Mumbai we will try to detect locations that are not already crowded with restaurants. We are also particularly interested in areas with no Cafe’s in vicinity. We would also prefer locations as close to city center as possible, assuming that first two conditions are met.


## Data

Data associated with restaurants is collected using the Foursquare API. It is an excellent tool to collect venues at a given co-ordinate.The Foursquare API allows application developers to interact with the Foursquare platform. The API itself is a RESTful set of addresses to which you can send requests, so there's really nothing to download onto your server. To use the Foursquare API, we first need a list of boroughs in Mumbai along with their pin-codes. 

[Pincode Locations](https://i.imgur.com/CiTKbnN.png)

After which the latitude and longitude value for the given pin-codes are required. This can be achieved by using a geocoder. We can begin our analysis by getting the details of restaurant venues in 7.5 km radius of the given location, this will ensure major parts of the city are covered without worrying about overlapping locations. Data cleaning is required to get rid of the venues which are not restaurants or venues that are not related to food. Once the resulting data frame is obtained the process of data collection can be considered complete and we can proceed with exploratory data analysis. The data-set has locations of 8500 restaurants in Mumbai along with their name and the category of restaurant.

[Geo Data](https://i.imgur.com/4r17MKb.png)


## Methodology

Based on definition of our problem, factors that will influence our decisions are:

- Finding a cluster of similar Neighborhoods.
- Number of existing restaurants in the neighborhood (any type of restaurant).
- Number of and distance to Cafe’s in the neighborhood, if any.
- Accessibility of neighborhood.

We decided to use regularly spaced grid of locations, centered around city center, to define our neighborhoods.

Following data sources will be needed to extract/generate the required information:
- Centers of candidate areas will be generated algorithmically and approximate addresses of centers of those areas will be obtained using reverse geocoding
- Number of restaurants and their type and location in every neighborhood will be obtained using Foursquare API
- Coordinates will be obtained using geocoding of well known Borough pin-codes.

## Feature Extraction

Relevant features have to be extracted from the data, the data-set contains noisy features like sports stadiums, scenic lookouts and monuments. Features with key words restaurant in their category have to be extracted. Extracted variables have to be converted to categorical variables,  where each category will form an attribute with binary values.

[Features](https://i.imgur.com/rsGLnAS.png)

## Exploratory Data Analysis 

Exploring the data gives us valuable insights before modelling the data for machine learning. Examining the market share of various restaurants shows that Indian restaurants are the most common restaurant type in Mumbai with about 33% of the market share. People in India are very culturally rooted and prefer having food with family in familiar setting which is the reason for the popularity of Indian restaurants. But the younger generation have more inclination towards Cafe's and Coffee places. These places have trendy ambience and younger people like to hangout there after work and college with their friends. The popularity is in an upward trend with Cafe's and Coffee houses, already having a hefty market share. The market may have been saturated with Indian restaurants but there is still room left for Cafe's and Coffee places for expansion.

[Restaurant Market Share](https://i.imgur.com/zlCUoeD.png)

Looking at common venues in each neighborhood also concludes that Indian restaurants are the most common restaurants in Mumbai, but other restaurants are gaining popularity steadily. The closest to Indian restaurants in popularity are the Cafe’s and Coffee places. When combined they cover nearly 23% of the market share. Dessert shops in India are generally sweet/confectionery shops and not restaurant per-say, but are quite popular too. 

[Img1](https://i.imgur.com/BEVSbCQ.png)
[Img2](https://i.imgur.com/P73835K.png)


## Modelling
For a clustering problem the attributes with binary data are prepared. The attributes contain information about the type of restaurant in each neighborhood and how common are those restaurant. Agglomerative clustering algorithm is used to get a rough idea about the number of clusters that can be extracted from the data without losing useful information. A distance matrix is created for each point with a randomly assigned cluster centre. An agglomerative cluster can be visualized using a dendrogram. The x-axis on a dendrogram represents the distance between individual clusters. The y-axis is a list of boroughs with coloured lines indicating the cluster which it belongs. The names on the y-axis are arranged in such a manner that similar neighbors are arranged closer to each other. The affinity parameter is set to ‘l1’ and the linkage is set to ‘average’. Average uses the average of the distances of each observation of the two sets. Once we have a rough idea about the number of clusters we can tune our Kmeans model.



## Agglomerative Hierarchical clustering Technique: 

In this technique, initially each data point is considered as an individual cluster. At each iteration, the similar clusters merge with other clusters until one cluster or K clusters are formed.
The psedocode for Agglomerative is straight forward.
- Compute the proximity matrix
- Let each data point be a cluster
- Repeat: Merge the two closest clusters and update the proximity matrix until only a single cluster remains.

[Agglomerative Clusters](https://i.imgur.com/Ecpqu9d.png)

A highly co-related neighborhood with virtually zero distance between them in the distance matrix can be seen, the locations being Bazargate, Bandra, Bhawani Shankar Road, Chembur, Cotton Exchange, DM Colony, Ghatkopar, Govandi, Haji Ali, NITIE and Raj Bhavan areas. The number of clusters for Kmeans algorithm can also be optimized using the elbow method and calculating the sum of squared error among clusters and the silhouette scores of the model for different values of k. A minor elbow can be observed at k=5 in an otherwise smooth curve. 

[Elbow Method](https://i.imgur.com/GJtycYj.png)























