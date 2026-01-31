---
layout: page
title: Open API Activity
nav_exclude: true
---

## Introduction

This project illustrates how to setup executable specifications for
a REST web service using Open API, Swagger, and JSDocs. 

## Setup 

download the [starter code]({{ site.baseurl }}{% link Activities/module11-rest-with-openapi.zip %})

Run the following command to install all depedencies from the project root.

`$ npm install`

Run the server using the command:

`$ npm run dev`

This should start the server at port 3000. Open the page http://localhost:3000/api-docs in a browser. This page should show the 
specifications of the web service's endpoints.

Study the specifications by expanding each endpoint option. 
You can run an endpoint by selecting the "Try it out" option for 
an endpoint and providing the appropriate inputs. Enter invalid inputs
and verify the expected response.

## Structure

The project uses Swagger UI to render the executable api specifications. 
To this end, Swagger needs to be configured with a specification outlining shape of the date the services work with. You will find 
this configured as `swaggerOptions` in `src/app.ts`. This is the entry point of the server. The files in `src/routes` define the endpoints but more importantly they also have detailed js doc comments. These comments are used by Swagger UI to generate the documentation you see in the _api-docs_ endpoint.

The data types for this service are defined in `src/models`. The
directory `src/data` has sample test data which is loaded in memory
when the server starts. We are using an in-memory data store for 
this project for simplicity.

## For You To Do

The existing services for authors, books, bookCopies, and genres
allow a client to delete an author, a book, a copy, or a genre. The implementation for them also exists. However, they are not documented as executable specs in Open API. Complete this task by doing the following:

1. Add the appropriate route for the delete operation in `routes`
2. Add JSDoc comments for the added routes so that they show up in `localhost:3000/api-docs`, the existing endpoint for rendering the Swagger UI.

You can use the existing implementation details to create the Open API spec for the delete route.

Submit a zip archive containing only the `routes` directory and nothing else. See Canvas instructions for section-specific instructions.

## Grading

- Full credit. The Swagger UI shows routes as per the implementation for delete operations for each existing route.
- Partial credit. The Swagger UI shows routes as per the implementation for delete operations for at least two existing routes. 
- No credit. The Swagger UI does not show the requested documentation.

# Resources

- [Open API](https://www.openapis.org/)
- [Swagger UI](https://swagger.io/tools/swagger-ui/)
- [Swagger JS Docs](https://www.npmjs.com/package/swagger-jsdoc)
