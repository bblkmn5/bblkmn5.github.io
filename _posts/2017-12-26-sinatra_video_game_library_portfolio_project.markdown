---
layout: post
title:      "Sinatra Video Game Library Portfolio Project"
date:       2017-12-26 19:52:33 +0000
permalink:  sinatra_video_game_library_portfolio_project
---


Sinatra. The section after my enjoyable time in SQL and basic ActiveRecord. Time to get more complex!

For my Sinatra Portfolio Project, I wanted to create a database for a video game library. As a person who owns multiple gaming consoles, I wanted a place where I could see every game for every console that I own, without having to pull them off of the shelf.

For my first steps,  I initially layed out four table migrations (users, consoles, games, and console_games), with a join table of the console and game table IDs. However, after looking further in what I wanted to do (and how difficult I wanted to make it), I decided it was better to have the console table be the middle-ground for the other two controllers. Therefore, I added the ```user_id``` column to my consoles table, and the ```console_id``` column to my games table. This allowed me to use ActiveRecord's ```has_many```, ```belongs_to```, and ```has_many, :through``` associations: A user ```has_many :consoles```, a console ```has_many :games``` and ```belongs_to :user```, and a game ```belongs_to :console```.

After figuring out which controllers I wanted, I created the barebones file structure of my project, with all of the controllers, views, and models in place. For the users table, I wanted a login and create_user view, as well as a view to show all of the current user's consoles owned. For the consoles and games views, I included basic create, edit, index, and show pages. I also layed out, in plain text, what would show up on each page before creating the routes. In previous labs for the Sinatra section, I focused on creating all of the routes before the views, adding a lot more stress for me. Spending more time on the setup was a great step forward for me, allowing more work done on the routes, rather than formulating on the fly how I wanted the pages to look. 

For each controller, before writing the code, I made sure that the route linked successfully to its corresponding viewpage. This way, I had a starting point from which to revert back to if errors arose.

After running through the program a few times and feeling satisfied that everything worked as intended, I started adding my own layout preferences, such as giving the user a message when they had no consoles.

One of the most challenging parts of the project for me was with the ```delete``` routes for consoles and games. For some reason, my ```if...else``` iteration was not being run. I ran some ```pry```s within my ```consoles/new``` and ```users/signup``` routes, so I could see what the values of ```current_user``` and ```console.user_id``` were. Eventually,  I realized that when a console was created, it was not saving the ```current_user.id``` in its  ```console.user_id``` column. As a result, my ```if``` statement was always returning false. By setting the value after ```Console.create(params)```, with ```current_user.id == @console.user_id```, and then using ```@console.save```, I ensured that the value was set when created at the corresponding ```post``` route of my consoles controller. This fixed the ```delete``` routes for both my consoles and games controllers, showing the power of ```binding.pry``` and how important it is to be able to pause a program and check its current state.

The final step in my project was adding error messages for the user, rather than just redirecting to the same page if an error was reached. This allowed my program to be more user-friendly, and give more direction. 
 
After finishing this project, there are a few things I would like to include in the future. These include: a user wishlist of consoles/games, more characteristics of games (like genres and notes), user characteristics (such as user age and favorite genres), and better readability and formatting for view pages. 

In conclusion, I am very happy with my Sinatra Portfolio Project. I have learned a lot since my CLI Project Assessment, and I am excited to be moving forward with software development and creating projects with real-world use. My video game library can be found [here](https://github.com/bblkmn5/video-game-library).
