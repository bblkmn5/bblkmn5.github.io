---
layout: post
title:      "CLI Gem Walkthrough"
date:       2017-11-10 00:16:31 -0500
permalink:  cli_gem_walkthrough
---


I had a lot of difficulty figuring out where to start with my CLI Data Gem Portfolio Project. At first, I thought it would be cool to scrape data from the WeWorks website, and even started a project for it, but I ultimately decided on the city of Santa Cruz's events webpage.

I watched a lot of the videos posted on Learn, seeing where people started and how their projects began to take shape. It was very helpful for me to be able to watch Avi's beginning steps for the now-playing and deals cli apps. The videos really showed me how crucial it is to break down a big project into smaller pieces, as well as why it is important to start writing rather than try to make it perfect initially.

I started my project by using the Bundler gem to install my gem, using  `bundle gem events_today` on the command line.  This created a template for the gem, allowing me to get started with my project quickly. 

Next, I typed out the basic output that I wanted the user to see when interacting with my gem. I went to the Santa Cruz events website and looked at the information that was given, decided what I wanted to scrape in the future, and put that text as a placeholder in my gem. I definitely spent more time on this than I should have at this point in the project, but I wanted to make sure it looked good for what I wanted.

After writing put my psuedocode, I started looking into creating different classes for the major parts of the project. I know I wanted a class for my cli interface, one for scraping all of the data from the website, and one for taking that scraped data and putting it into an object, allowing me to slowly replace my hard-coded information. 

After planning out what I wanted my program to do, I created an `Event` class, put all of my hardcoded information into it that I wanted to be called by the CLI class, and made sure that my program would still run as expected, with `ruby ./bin/events-today`. I knew that I would eventually need to create variables for the information I wanted, so I added these as `attr_accessor`'s for future use.

Next, on to the scraping! First, I had to require the `Nokogiri` and `open-uri` gems to allow for scraping the HTML of the events website. To help with this, I also added the `pry` gem, so I could go within the processes I created and see exactly what was going on. Being able to inspect the HTML on the website was very helpful, as it allowed me to pinpoint precisely the information I needed for each attribute.

Initially, I was getting very frustrated with the scope I wanted for my project. I spent hours scouring the internet to figure out how to scrape data from an outside website, connected by a link in the HTML of the events page. Though I eventually found a crude way of getting it to work, I realized I would have to change a somewhat major portion of my code. In the end, I decided to omit it from this version. It was a load of stress off of my back, and I am very happy with my decision. After all, this is my first Ruby gem made from scratch!

One of the final pieces of my project was to figure out how to only get the first few featured events, rather than all of the featured events from the webpage. For some reason, the page had almost the exact same CSS classes for all of the featured events, even though they were grouped within different boxes and tags within the code. A trip to the [ruby-gems.org](http://) database provided me with a quick fix to my array, by using `[0..5]` to only grab the first 6 events of the scraped data.

Finally, I created the gem by building it locally with my gemspec file, and pushing the final result to the ruby gems website for public use.

In conclusion, I had a difficult time creating this gem (which is good!). I learned a lot from this experience, and will definitely go about future projects with more structure and a smaller-format mind-set. I am very excited that I was able to complete it, even with all of the frustrations along the way. On to more coding!

Future features I am interested in for my gem include: grabbing the time of and event age group attributes to provide to user, allowing for splitting of multiple genres for each event, scraping a full description within more info, and adding a saved checkout "cart" list for what events a user is interested in. 

My gem can be found at: [https://rubygems.org/gems/events-today-cli-app](http://)






