---
layout: post
title:      "Rails jQuery Portfolio Project"
date:       2018-05-31 16:05:22 +0000
permalink:  rails_jquery_portfolio_project
---

For my Rails w/ jQuery Project, I decided to build off of my Zoo Owner App that I created for my Rails project. This project used the Devise and OAuth gems for user authentication and authorization. As I had a difficult time creating the Rails project, I was reserved in thinking I would be able to complete this by myself. I planned on going to more study groups to further my understanding of jQuery (another topic that I did not feel 100% about). 

My first step was to create a new branch for my jquery integration. This was as easy as, within the project directory, typing ```git checkout -b jquery``` into the terminal. I spent a fair amount of time familiarizing myself with the code I had created before, then started formulating a game plan to fulfill the project requirements.  

## Requirements
The next step was for me to go over the requirements for the project:

* #### Use jQuery for implementing new requirements
To fulfill this requirement, I added two gems to allow for jQuery implementation: ```jquery-rails``` and ```active_model_serializers```. The first gem provided jquery integration with the rails backend I had already administered, while the second gem allowed me to render JSON objects of each Model, along with the Active Record associates created within each Model.
				 
				 
* #### Include a show resource rendered using jQuery and an Active Model Serialization JSON backend.
On my Zoo's Show page, I included a button to show all of the animals within that specific zoo. However, this is only rendered using jQuery, and does not include a JSON backend. Therefore, I created another show rendering on my Animal Show page, which renders a Comment create form.
 
 
* #### Include an index resource rendered using jQuery and an Active Model Serialization JSON backend.
On my Animal Index page, I created my own route for all animals belonging to a user within my ```routes.rb``` file. This is organized by Zoo. The page initially shows every name of each animal within each individual zoo, while displaying a "more info" button underneath. After clicking the button, a jQuery GET request is made to the individual Animal's show page, grabs the necessary JSON data, and returns it to the page. The most difficult part of this requirement was also rendering the comments belonging to each individual animal, as I had to iterate over the comment's array.


* #### Include at least one has_many relationship in information rendered via JSON and appended to the DOM.
I have a ```has_many``` relationship between my join table (Zoo) and each Model (Animals and Keepers), as well as between an Animal and it's comments. This information is rendered via JSON and appended to the Zoo and Animal Show pages, respectively.

   
* #### Use your Rails API and a form to create a resource and render the response without a page refresh.
As mentioned before, I rendered a Comment's create form on my Animal's show page. When submitted, the new Comment is rendered into the list above the form. I also added a ```delete``` link to the new list item, allowing for instantaneous creating and destroying of a new entry without a page refresh. In addition, I created another form able to submit without a page refresh on my Zoo Show page, allowing for the creation of a new Keeper. 
 
 
* #### Translate JSON responses into js model objects.
 To fulfill this requirement, within a GET request, I converted the action url with JSON (ex. ``` `/users/${user_id}/animals/${id}.json` ```. This turned the requested AJAX request into a JSON object.
 
 
* #### At least one of the js model objects must have at least one method added by your code to the prototype.
For this final requirement, on my Animal model I have ```Animal.prototype.renderAnimalTraits```. This prototype simply cleans up my ```showMoreTraits``` method by returning simple HTML and Javascript interpolation (```${this.name} the ${this.species}```. I also have a prototype on my Comment model to render HTML as well.


## Difficulties
Many of the difficulties I encounted for this project had to do with my nested resources, and creating the correct routes. As every resource was nested underneath Users, I had to send a lot of extra data through every jQuery ```GET``` request (such as ```current_user.id, zoo.id, ``` and ```animal.id```). In this regard, I spent a lot more time and energy working these out than necessary. 

The other main difficulty for me was project importance. I was very focused on specific feratures I wanted to add (such as an ajax delete request from a just-created comment without a page refresh) that I did not take a step back and focus on requirements first. As a result, this project took a lot longer than it should have to complete. Towards the end, after talking it over with a few colleagues, I was able to realize this mistake and move forward much quicker. 

## Favorite Parts
What I enjoyed most about this project was increasing my willingness to look up things on Google. As I have found out (personally from this project and talking to others in their careers), a lot of on-the-job hours are spent looking up how to do things, and not being expected to know everything about everything. Therefore, being able to know when to use Google versus racking your brain for the answer (or knowing when to ask for help!), is a crucial skill as a software developer.

## Conclusion

Finally, some potential future features include: favorite animal species category for each zoo keeper; add jQuery for each form; add image upload option for new animals, keepers, and zoos; and spend more time on CSS and HTML formatting.

You can find my Zoo Owner App on Github [here](https://github.com/bblkmn5/zoo_rails_project/tree/jquery).
