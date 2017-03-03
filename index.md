# Introduction

The content of this web page is about my experience using the Spotify API and the guide with it. Focusing on certain areas, I found some areas that needed further explanation. Furthermore, I talk about my use of the API in my own web application.

# Getting Started

For the purposes of my guide you need to follow these steps to start using the Spotify API.

1. Create a Spotify account
1. Create a new app from their developer site
1. Set redirect URI
1. Acquire your API key under your application's details; Spotify named it "Client Secret"

# Applying the APIs

### IDs
One of the things that seems important to retrieve information is "ID"s. Their are Spotify API that uses these IDs to specify search for things such as artist, albums, and playlists. The guide on the API site explains how to use these IDs pretty well, however I had a hard time finding out how to acquire these ID. To solve this problem, in my own application, I used the "GET An Artist" API and analysed the information sent back.

### GET Artist

    var apiKey = null;
    var api_url = 'http://api.spotify.com';

    document.getElementById('artist_name_button').addEventListener('click', function(event) {
        
        var req = new XMLHttpRequest();
        var artist_name = document.getElementById('artist_name').value;

         req.open("GET", api_url + "/v1/search?q=" + artist_name + "&type=artist&market=US" , true);
         req.send(null);

         req.addEventListener('load', function(){
                if(req.status >= 200 && req.status < 400){
                        var response = {};
                        response = JSON.parse(req.responseText);
                        console.log(JSON.parse(req.responseText));
                        var id = response.artists.items[0].id;
                        artist_albums(id);
                        event.preventDefault();
                 }else{
                        console.log('Error in network request');
                 };
          });
    });

In this snippet I took the input from an html page and used it to retrieve an aritist's Spotify detials, including their Spotify ID. From this I found the ID within the object for the artist given under object.artists.items[0].id . With this ID I was able to do more things that related to the specific artist in question.

### GET Albums

    req.open("GET", api_url + "/v1/artists/" + id + "/albums", true);

By using the artist's ID, I was able to retrieve all the albums the artist released. When examining the album API I noticed a few things with the object sent back. One of the first things was that to find the albums list, you had to go object.items and to get the name of the album, object.items.name . However, this array holds 20 objects for each artist. So, I found that there is a number of repeated albums and that made it difficult to simply go through the array and print out the albums for the artist. 

To solve this issue I made a new array that would go through the one from the object and ignore any repeated items and any albums that were just singles from the artist.

    var albums = [];
    for(var i =0;i < response.items.length-1; i++){
        for(var k=0; i<response.items.length-1;){

             if(albums.length == 0 || ((albums[k] != response.items[i].name) && (response.items[i].album_type == 'album')){
                 if(albums.length != 0){k+=1};
                 albums.push(response.items[i].name);
             } else {i+=1};
         }
    };

### Authorization Code

       GET https://accounts.spotify.com/authorize

The authorization code is how the user gives the API permission to modify data. With this we can do something like make a new playlist and populate it with tracks. A lot of the POST methods with Spotify have to use an authorization code since most of the time we are trying to manipulate someone's else's profile.

### User ID

To do things like make a new playlist, you need to have an authorization and the user's Spotify's ID number. This is a specific number for each user's profile. With the you can also add tracks to a playlest, delete tracks, follow and unfollow. Anything that changes the user's profile requires the user's ID.

### POSTS

POSTS with this API recquire one or both the authorization code and the user ID. For example a POST to add a new playlist would look like this after gaining authorization.

     req.open('POST', 'https://api.spotify.com/v1/users/' + user_id + '/playlists', true);
     
### My Application

![my-api](/api.png)


