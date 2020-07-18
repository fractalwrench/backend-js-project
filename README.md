# backend-js-project

An approach on how to build a first backend project using JavaScript, along with a React example app to test it out. You should develop both in tandem if possible.

## Studying

Start out by reading the following. There's a lot of prerequisite knowledge which will make the project easier to complete.

1. Cover the [brief Codecademy primer](https://www.codecademy.com/learn/learn-node-js) on NodeJS.
2. Go through the [Codecademy tutorial for ExpressJS](https://www.codecademy.com/learn/learn-express) which is a NodeJS framework which helps build backends
3. Be sure to spend some time thoroughly going through these articles, as they cover essential concepts that can be applied to any programming language:
    1. [What is a backend architecture](https://www.codecademy.com/articles/back-end-architecture)
    2. [What is a HTTP request](https://www.codecademy.com/articles/http-requests)
    3. [What is a RESTful API](https://www.codecademy.com/articles/what-is-rest)

If you need a break from studying at any point you should work on the movie search app and attempt to fix any bugs left over/improve the general look and feel of the application.

## Setup

Install [Postman](https://www.postman.com/downloads/) which will be useful for testing REST applications.

# Cat API

Create a REST API using ExpressJS which allows users to query information about cats.

All JSON responses should return a JSON object, not an array. Where necessary a wrapper object should be used to avoid returning a JSON array, e.g.:

```js
{
  data: [
    // 
  ]
}
```

## Data models

The following classes should be created which model API responses. You should write unit tests for these requirements wherever possible.

It is strongly advised that you should create a separate PR for each section below, as this will ease review and traceability in the Git history.

### Cat summary object

A cat summary object should represent important, summarized information about a cat:

```js
{
  id: "15fa095c"
  name: "Mr Fluffykins"
}
```

`id` - a unique identifier which is autogenerated whenever a new cat resource is created
`name` - a non-empty, non-null string <512 chars which represents the name of the cat

### Cat detail object

A cat detail object should represent all information about a cat:

```js
{
  id: "15fa095c"
  name: "Mr Fluffykins",
  ageInYears: 5,
  favouriteToy: "ball of string",
  breedId: "f0abc241"
}
```

- `id` - a unique identifier which is autogenerated whenever a new cat resource is created. This can be null in incoming requests
- `name` - a non-empty, non-null string <512 chars which represents the name of the cat
- `ageInYears` - a non-null positive integer within the range 0-99
- `favouriteToy` - a nullable string which is validated as <512 chars
- `breedId` - a non-null unique identifier which corresponds to the breed resource ID.

### Breed object

A breed object should represent information about a particular pedigree of cat:

```js
{
  id: "f0abc241"
  name: "tabby",
  description: "A tabby cat is a common house cat."
}
```

- `id` - a unique identifier which is autogenerated whenever a new breed resource is created
- `name` - a non-empty, non-null string <512 chars which represents the name of the breed
- `description` - a non-empty, non-null description <512 chars which gives descriptive info about the breed

## Data repository

This project won't use a database but you should use the [repository pattern](https://blog.kylegalbraith.com/2018/03/06/getting-familiar-with-the-awesome-repository-pattern/) to make it easier to change the implementation to use one in future. You should write unit tests for these requirements wherever possible.

It is strongly advised that you should create a separate PR for each section below, as this will ease review and traceability in the Git history.

You should declare the following data repositories:

### CatRepository

Stores cats. 🐱

```js
class CatRepository {
   function List<Cat> getCats();
   function Cat getCatById(String id);
   function void addCat(Cat cat);
   function void updateCat(Cat cat);
   function void deleteCat(Cat cat);
}
```

The repository should be pre-populated with some representative information about cats.

If there are no cats `getCats()` should return an empty list. If `getCatById()` does not exist it should return null.

Cats should only be updated if the object contains a valid ID matching an existing cat, and should only be added if the object does not contain an ID. If this is not the case [an error should be thrown](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw) and calling code should handle the error.

### BreedRepository

```js
class BreedRepository {
   function List<Breed> getBreeds();
   function Breed getBreedById(String id);
}
```

The repository should be pre-populated with some representative information about breeds.

If there are no breeds `getBreeds()` should return an empty list. If `getBreedById()` does not exist it should return null.

## Supported HTTP calls

The following REST endpoints are available for a user to call. You should write unit + integration tests for these requirements wherever possible. All HTTP calls should return an appropriate status code and this should be validated.

It is strongly advised that you should create a separate PR for each section below, as this will ease review and traceability in the Git history.

### GET /cats

Returns a list of cat summary objects. If no cats exist, an empty list should be returned instead.

### GET /cats/{catId}

Returns a single cat summary detail object. If no cat exists with this ID the HTTP call should return an appropriate status code.

### POST /cats

Allows a user to add a single cat detail object to the backend. The call should validate that the request payload is valid JSON that matches a single cat detail object. The cat detail object should be returned as a response.

The `id` parameter should be null. If the request is not successful for whatever reason an appropriate status code should be returned.

### PUT /cats/{catId}

Allows a user to update a single cat detail object that already exists on the backend. The call should validate that the request payload is valid JSON that matches a single existing cat detail object. The cat detail object should be returned as a response.

The `id` parameter should not be null. If the request is not successful for whatever reason an appropriate status code should be returned.

### DELETE /cats/{catId}

Allows a user to delete a single cat detail object that already exists on the backend. The call should validate that the request payload is valid JSON that matches a single existing cat detail object.

The `id` parameter should not be null. If the request is not successful for whatever reason an appropriate status code should be returned.

### GET /breeds

Returns a list of cat breed objects. If no breeds exist, an empty list should be returned instead.

### GET /breeds/{breedId}

Returns a single breed object. If no breed exists with this ID the HTTP call should return an appropriate status code.

## Documentation

You should write documentation in the README of your repository that explains your REST API, and the requirements for calling each endpoint. Another developer should be able to construct successful API calls from the documentation you have given.

## Example app

You should create a React App which makes use of the API.

### Display list of cats

The app should display a list of existing cats on screen. Clicking on an individual cat should display its full details at the top of the screen, and visually indicate on the list item that it has been selected. If no cats exist a simple message stating this should be displayed.

### Add cat
The app should have a single button to add a cat. Clicking this should show a HTML form which allows users to add a new cat, which should then be displayed in the list and automatically selected.

### Delete cat

The app should have a button on each list item to delete the cat. Clicking this should delete the cat and reset the selected item to the top cat (if any).

### Update cat
The app should have a button on each list item to edit the cat. Clicking this should show a HTML form which allows users to update the cat. Once they have submitted this, the new cat information should be displayed in the list.

