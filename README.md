# Building-basic-RESTful-CRUD-with-Golang-MySQL
Building basic RESTful (CRUD) with Golang &amp; MySQL


# Introduction

We would be developing an application that exposes a basic REST-API server for CRUD operations for managing Persons (id,firstName,lastName, age)
Before we start, lets us make a check that the reader might have basic knowledge of SQL and Golang.

```
mkdir rest-go-demo && cd rest-go-example
```

This will create a folder named “rest-go-demo”.
Now, let’s start with initializing and adding the go-modules required for our application

```
go mod init
go get github.com/gorilla/mux
go get github.com/jinzhu/gorm
go get github.com/go-sql-driver/mysql
```

We will be utilizing the dependency management provided by Golang in form of go-modules.
“go mod init” is used to initialize the root application and dependencies can be tracked with the go.mod created after the execution of the above command.
We would need certain packages to help with our journey:
1. gorilla/mux:= For creating routes and HTTP handlers for our endpoints
2. jinzhu/gorm:= An ORM tool for MySQL.
3. go-sql-driver/mysql:= MYSQL driver.

# Setting MySQL:

As we would be using MySQL as our backing database to persist our user data.
let’s start with creating a database specific to our needs.

```
CREATE DATABASE learning;
```

Let’s create a struct for managing our database configuration which would be utilized to create a connection to the database.

Now, let’s create a client to manage and create connections to our Database

Let’s test whether our client can connect with our database or not!!

```
vishal@vishal:~/go/src/rest-go-demo$ go run main.go 
2021/02/14 16:56:34 Connection was successful!!
vishal@vishal:~/go/src/rest-go-demo$
```

Now, let’s create our simple Person struct which would be our object in reference.

```
type Person struct {
ID        string `json:"id"`
FirstName string `json:"firstName"`
LastName  string `json:"lastName"`
Age       string `json:"age"`
}
```

# Create a Simple HTTP Server

We would be using “gorilla/mux” to create a simple server for handling our HTTP requests.


An HTTP server, operating on port 8090 will be initiated for our usage.
Now let’s add our REST endpoint’s and move further in our journey
POST / CREATE endpoint
We will start by adding a route “/create/” to our router to serve an endpoint which will create a new person whenever triggered

```
router.HandleFunc("/create",createPerson).Methods("POST")
```

Let’s create a respective createPerson(), the function that will take the POST request data and create a new person entry in DB.
We will do the same by first Unmarsahlling the JSON data retrieved from the body into our Person struct created above and later insert the data by creating a new record.


GET / SELECT endpoint
Similarly, we added handler and respective function for POST, we will all “/get/{id}” to our router to retrieve data

```
router.HandleFunc("/get/{id}", getPersonByID).Methods("GET")
```

Let’s add the respective getPersonByID() function, which will utilize the request parameter “id” to retrieve the respective data and return a JSON response.
Here we would be reversing the procedure we did while creating POST endpoint, we would be Marshalling the person struct retrieved from the database to JSON and create an HTTP response.

PUT / UPDATE endpoint
Now I might assume you might have guessed what comes next in our router and respective functions

```
router.HandleFunc("/update/{id}", updatePersonByID).Methods("PUT")
```

updatePersonByID() will take up the POST request data, Unmarshall the JSON to person struct, and update respectively

DELETE / DELETE endpoint

```
router.HandleFunc("/delete/{id}", deletPersonByID).Methods("DELETE")
```

deletePersonByID() will delete the “id” passed in the request parameter and deletes the respective record from the database.
Now, as all our endpoints are in place let's integrate all of them and test out our CRUD operations.
We will do this by executing the below commands

```
go mod tidy
go build
./rest-go-demo
```

