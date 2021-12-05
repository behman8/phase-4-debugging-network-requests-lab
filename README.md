# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged: I opened up my console and then submitted a new toy to be added. The error I got in the console was a 500 (Internal Server Error). As I have learned if there is a 500 status code there is an error on the server. So I looked in the server logs. It gave a NameError (uninitialized constant ToysController::Toys). It also gave me where to find the uninitialized error. I found in the code that it was saying Toys.create instead of Toy.create. After changing that I submitted the toy again and it worked. 

- Update the number of likes for a toy

  - How I debugged: With the console open I clicked like on a toy and got a Uncaught (in promise) SyntaxError: Unexpected end of JSON input at ToyForm.js:21. It expects the server to return a string of JSON-formatted data, but you get this error when it is not returning any content. So I know I need to return JSON data in the response from the update controller action. When I went to the update controller action I noticed that it was not rendering json at the end. I added that to the action and went to like a toy and it increased a like for it.

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged: I clicked the donate to goodwill button with the console open. It gave a 404 (not found) error. I then checked the network tab to get more info about it. Noticed it was a ActionController::RoutingError (No route matches [DELETE] "/toys/7"). So I went to check my routes and found where the problem was. There was no destroy action defined as a route. So I added it and clicked the donate to goodwill button again and it deleted the toy from the database.
