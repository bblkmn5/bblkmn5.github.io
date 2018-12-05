---
layout: post
title:      "React/Redux: IT Support App"
date:       2018-12-05 17:05:35 +0000
permalink:  react_redux_it_support_app
---


For my final Flatiron School Portfolio Project, I created a React & Redux frontend with Rails backend application to keep track of IT support service requests. I chose this topic because my first job in high school was a Computer Services Assistant position, and having a database of service requests would have made a world of difference.


## What I did
The first step was to figure out how to format the project. As I needed two different parts (backend Rails API and frontend React), I decided to split up my project into two different repositories. Within the terminal, I used `create-react-app it-support-client` to create my boilerplate frontend, and `rails new it-support-api --api` for my backend API. Next, I linked both folders to my Github account, allowing for seamless version control.

With everything set up for commiting changes, it was time to code. I decided to start with my frontend code, laying out how I wanted the code to look after being connected to the API. In this fashion, I could focus more on the user interface first, while worrying about the fetching and database afterwards. I loaded up the react server in my terminal with `yarn start`. After making sure that worked, I decided to break up the file tree of my project into different component folders. By creating a `Layout` folder and file, I could import it to my `App.js` file and add it into the presentational function like so:

```
import React from 'react;
import Layout from './components/Layout/Layout';

const App = () => {
 return (
  <div>
   <Layout />
  </div>
 )
}

export default App;
 ```
 
This cleaned up my code a lot, and allowed me to set all of my other components within my `Layout.js` file, such as my About page and Navigation bar.

After setting up my `OrdersContainer` file with the `react-bootstrap` library to include a bootstrapped table, it was time to connect to my backend. In the terminal, I ran `rails g migration create_orders service:string device:string location:string notes:string` to set up the database, set up the controller for CRUD capability, routed orders, and finally created some seed data. On the react side, within a `.env` file, I created a variable `REACT_APP_API_URL` that pointed to the server port of 3001, allowing me to have both react and rails servers running simultaneously. As I knew I would be implementing redux, I decided to create an actions folder with an order_actions file. I used the `isomorphic-fetch` library to request the database from the API with `fetch`. 

To add redux, a few steps were required. First, I had to add the react-redux library to my app. Next, I had to set up the store within the index page, by importing `{ createStore, applyMiddleware, compose } from 'redux' `, and wrapping the entire App function in the Provider function. Then, within my `OrdersContainer` and `OrderForm` files, I connected each class to the action props for the state, allowing for seamless integration with a full redux application state and my API backend. In addition, by linking these classes, I was able to allow for order: creation, state update/deletion, and page navigation without an apparent refresh on the user side. Faster user interaction and lower loading pages equals happier users!

Once this was successfully set up, it was time to create the order form. I imported the `react-modal` library, to allow for the form to overlay over the current order table, and close on submit of the form. In addition, I added a `showModal` variable to state, allowing for seamless state change and Modal open/close by clicking specific buttons.

Finally, after writing and implementing order create and destroy actions and reducers, I added `Technicians` to my API. This added another level of complexity to each order, by choosing specific technicians based on the type of device that a user wanted serviced. 


## Conclusion
One of the coolest parts of coding this project was refactoring. With redux, being able to see the state update on every changed input of the order form:

```
handleOnChange = event => {
  const { name, value } = event.target;
  this.setState({
      [name]: value
  })
}
```

Another part of refactoring that I enjoyed was breaking up the components into their own files, allowing for more precise information for each component to hold, rather than one big file of code.

Two of the hardest parts for me were getting my ideas organized and stopping myself from looking at the big picture for too long. There were so many things I wanted to add, like more order categories and edit capability within the table, that I became too focused on those rather than only worrying about the requirements needed. Talking to other peers and friends really helped me condense my thought process and ultimately allowed me to finish this project.  
 

