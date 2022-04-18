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
