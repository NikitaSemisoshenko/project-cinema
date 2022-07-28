# project_cinema
Simple application which provides CRUD operations for cinema tickets shop. It supports authentication and authorization.
It supports roles model as well.
# Features
* registration of user and signing in
* view available movie sessions
* adding tickets to the shopping cart
* completing order
* view order history
# Project structure
The project_cinema based on a 3-tier architecture
* controllers for handling requests and responses
* service layer with business logic
* DAO layer that works with database

The project_cinema based on Spring and Hibernate frameworks. All service and dao classes is beans. They are handles
by Spring Framework. All users passwords encrypted with BCrypt algorithm. Hibernate framework responsible for mapping
entities with ORM.

Scheme of entities relations below

![alt text](cinema.png)

# Developed with
* Java 11
* Spring Core, MVC, Security v5
* Hibernate v5
* MySQL v8
* Apache Tomcat v9

# How to run this project locally
* clone this project
* create database locally
* in db.properties file write your credentials - database connectivity driver, database url, username, password
* set up your Tomcat local server configuration
* run the application with Tomcat

# How to test it out

Then the application starts two users are already injects. Here the credentials for them
* login: bob@i.ua. Password: 12345678. Role: admin
* login: alice@i.ua Password: 12345678. Role: user

You can use both of them for testing application API
* `POST /register` for non-authenticated user. It provides registration of user with USER role. DTO fields: email,
  password, repeatPassword.
  **Example**: {"email":"john@i.ua", "password":"qwerty1234","repeatPassword":"qwerty1234"}

* `POST /cinema-halls` for user with admin role. Provides inserting of cinema hall to database. DTO fields: capacity,
  description.
  **Example**: {"capacity":200, "description":"StarCinema hall at Broadway"}

* `GET /cinema-halls` any role. It shows list of available cinema halls.

* `POST /movies` for user with admin role. Provides inserting of movie to database. DTO fields: title, description.
  **Example**: {"title":"Kill Bill", "description":"Awesome film by Quentin Tarantino"

* `GET /movies` any role. It shows list of available movies.

* `POST /movie-sessions` for user with admin role. DTO fields: movieId, cinemaHallId, showTime. Show time must match
  pattern _dd.MM.yyyy_.
  **Example**: {"movieId":"1", "cinemaHallId":1, "showTime":"28.03.2022"

* `GET /movie-sessions/available?movieId={movieId}&date={date]` any role. Shows available movie sessions for movie with
  id {movieId} and date {date}.
  **Example**: http://localhost:8080/movie-sessions/available?movieId=1&date=28.03.2022

* `PUT /movie-sessions/{id}` for user with admin role. Updates movie session with id {id}. DTO fields: movieId,
  cinemaHallId, showTime. Show time must match pattern _dd.MM.yyyy_.
  **Example**: {"movieId":"1", "cinemaHallId":1, "showTime":"28.03.2022"

* `DELETE /movie-sessions/{id}` for user with admin role. Deletes movie session with id {id}.

* `PUT /shopping-carts/movie-sessions/{movieSessionId` for any role. Puts the movie session with id {id} to
  shopping cart of current authenticated user.

* `GET /shopping-carts/by-user` for any role. Shows shopping cart of current authenticated user.

* `GET /users/by-email?email={email}` shows DTO object of user with email {email}.
  **Example**: http://localhost:8080/users/by-email?email=bob@i.ua

* `POST /orders/complete` for any role. Creates an order from movie sessions from shopping cart of current user

* `GET /orders` for any role. Shows order history for current authenticated user.
