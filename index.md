# Introduction

The content of this web page is about my experience using the Spotify API and the guide with it. Focusing on fetching data, I found some areas that needed further explanation. 

In addition, I talk about my use of the API in my own web application.

# Getting Started

For the purposes of my guide you need to follow these steps to start using the Spotify API.

1. Create a Spotify account
1. Create a new app from their developer site
1. Set redirect URI
1. Acquire your API key under your application's details; Spotify named it "Client Secret"

# Applying the APIs

### IDs (Artists, albums, etc)
One of the things that seems important to retrieve information is "ID"s. Their are Spotify API that uses these IDs to specify search for things such as artist, albums, and playlists. The guide on the API site explains how to use these IDs pretty well, however I had a hard time finding out how to acquire these ID. 

To solve this problem, in my own application, I took an input of an artist name and retrieved the data from Spotify using the "GET An Artist" API. From this I found the ID within the object for the artist given. With this ID I was able to do more things that related to the specific artist in question.
--> Pic <--

### GET Artist

Objects from calling the artist.
Using this ID I then retrieved the albums of the artist. 

--> Pics of example <--

### GET Albums
When examining the album API I noticed a few things with the object retrieved. One of the first things was that to find the albums list, you had to go ----. However, this array holds 20 objects no matter the number of albums. I found that there is a number of repeated albums and that made it difficult to simply print out the albums for each artist. 

