---
layout: post
title:      "Rails Portfolio Project: Having a Zoo of a Time "
date:       2018-02-28 22:05:29 +0000
permalink:  rails_portfolio_project_having_a_zoo_of_a_time
---


For my last Ruby portfolio project, I decided to create a website for hosting a user's zoos, with pages for zoo keepers and animals within these zoos.

Rails, while very similar to Sinatra, was a very challenging process for me (I feel like I say something like this before every project!). When starting out with the gem, I felt myself picking it up fairly quickly. The basic outline for creating an application with Rails is the same (if not quicker) as in Sinatra.  In Rails, it is as simple as installing the gem and typing `rails new <filename>` to create a template with everything necessary for a rails application. 

After creating my basic project, I decided to focus on what I wanted to do with my application. I started off thinking I should go from the perspective of one zoo, with tables for animals, keepers, tickets, equipment, etc. However, where in the past I would have automatically started coding everything out and getting overwhelmed, I decided to talk with other people about my ideas. This contact and talk-through with others was crucial for me, and a step I hope to take advantage of for the future. It allowed me to realize how much I was overthinking the process, and that I needed to start with a simpler approach. For my CLI Gem and Sinatra portfolio projects, I had to re-write everything after getting overwhelmed. Not this time (hey, I must be learning!).

After laying out a more structured approach, my next step was to set up the migrations. Staying in line with the requirements for the project, I knew that I needed to start with a User table. I then added Animal, Keeper, and Zoo tables. I made the Zoo table a join table, including the foreign keys from the animal, keeper, and user tables. To create these tables, I used `rails g(generate) model <table_name> <col1:col1_type> <col2:col2_type> <etc>` to create the models as well as migrations for each table in terminal. 

Next, after figuring out the different associations between the tables (`zoo has_many :animals`, `animal belongs_to :zoo`), I ran `rails g controller <table_name>` in terminal for each table. This action created the full CRUD routes, by putting `resources :zoos`, `resources :users`, etc. in `config/routes.rb`, as well as creating: controller files, view folders, helper files, and css/javascript files for each item. I also created a `static` controller, route, and view home page, which would be the root page for my application. Finally, I added the simple `Hello World` text in my static controller, ran `rails db:migrate`, `rails s(erver)`, and went to `localhost:3000` on my browser to find that I had set everything up correctly.

After successfully connecting to the rails server, I started creating the index and show pages for each model, as well as the forms for creating and editing new animals and keepers. I used partials for these view pages, making my code more DRY, by adding the ```_form.html.erb``` to the new and edit pages, with ```<%= render 'form' %>```. I also needed to add local variables and actions based on what the form would do, as I had decided on nesting all other controller actions under my user resource.

I had already started manually adding a sign in/sign up controllers and views within my ```User``` model, but I felt like I wasn't getting everything I wanted from it. Therefore, I decided on using the ```Devise``` and ```Omniauth``` gems for user authentication and to allow third-party access to my application. I knew this was going to be a challenge from the start, as when I went through the labs for these gems, especially Devise, I felt completely lost and out of my element. However, I felt like this would be a great test of my resolve and motivation in what I have learned.

I ran ```rails g devise:install``` and  ```rails g devise User``` to get devise started with migrations, initializers, models, and routes. Later on, I also generated the views and controllers with devise from the command line. This is a great feature, as it allows for synonymous forms and formatting, while allowing a developer to manipulate things as they see fit. Devise also has a ton of notes within each file to help guide what each controller does. 

For my omniauth third-party provider, I decided on using Facebook. As we had a lab going through the steps to easily prepare this feature, I wanted to make it as quick and painless as possible. It was amazing for me to find out that anyone can have a Facebook Developer account, and that with a bit of research, being able to link an app for login was achieveable.

A last step for my Zoo database was to allow a User to have many Zoos. Initially, I had it set up where a ```zoo belongs_to :user``` and ```user has_one :zoo```, but after talking it over in a one-on-one session, allowing for users to have many zoos made more sense from a growth position of the application.

One of the most difficult parts of this project was creating the authentication routes for my models. At first, I had basic CRUD routes for each model, but I ended up nesting zoos, animals, and keepers within the user resource route, to create ```user_modelName_path```s. This way, whenever a create, edit, or destroy action was called upon a specific table, the application checked to make sure the current_user had access to manipulate each zoo's data. In addition, this action meant I had to update every link and form used to account for these user paths. 

My favorite coding action of this lab is the nested scoping within the routes file. Being able to run the rails console, call ```current_user.zoo.animals``` from two completely different models, and get an output of all animals in a specific zoo brought pride to myself and what I have learned for the past several months.

### Future plans for project:

Features I would like to add to this project include: 
* animal last-fed and animal last-cleaned, with date-time references to notify the user when these actions need to be taken 
* putting specific keepers to specific animals, to add more information for keepers
* possibly adding different levels of users (using ```cancancan``` gem), so keepers can log in as well as admins of zoos
* update the formatting of the pages for a more user-friendly experience with navigating pages (and maybe pictures of animals!).

My project can be found [here](https://github.com/bblkmn5/zoo_rails_project).
