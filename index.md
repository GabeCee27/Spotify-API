# Introduction

The content of this web page is about my experience using the Spotify API and the guide with it. Focusing on fetching data, I found some areas that needed further explanation. 

In addition, I talk about my use of the API in my own web application.

# Getting Started

For the purposes of my guide you need to follow these steps to start using the Spotify API.

1. Create a Spotify account
1. Create a new app from their developer site
1. Set redirect URI
1. Acquire your API key under your applications "Client Secret"

# Applying the APIs

## IDs (Artists, albums, etc)
One of the aspects that seems that is importants to retrieve information is IDs. For Spotif uses these IDs to specify things such as artist, album, and playlists. The guide on the API explains fairly how to use these IDs.

--> Pic of Example <--

However, I had a hard to finding out how to get this ID. In my own application, I took an input of an artist name and retrieved the data from Spotify. From this I found the ID within the object for the artist given. 
--> Pic <--

## GET Artist

Objects from calling the artist.
Using this ID I then retrieved the albums of the artist. 

--> Pics of example <--

## GET Albums
When examining the album API I noticed a few things with the object retrieved. One of the first things was that to find the albums list, you had to go ----. However, this array holds 20 objects no matter the number of albums. I found that there is a number of repeated albums and that made it difficult to simply print out the albums for each artist. 

