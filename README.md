# Layer architecture for web apps

* https://medium.com/hackernoon/architecting-single-page-applications-b842ea633c2e

## App requirements

Build an app where a user can signin and add notes. Notes can be categorised.

__App functionality__

* User signin
* User / App settings
* Authentication via a fake api
* CRUD operations of a note (to a fake database) via api
* CRUD operations of a category (to a fake database) via api
* Routing
* Run things in a web worker


## Architecture (layers)

### View

* Uses a framework to display a view
* Component based
  * Dumb and Smart components
* Uses reactive state to display data
* Send new state to the store

### Application Services

* Services related to the application
  * Api services for ajax requests
  * Services for manipulating state for the view (make a users name all uppercase)

### Store

* Holds the state
  * State is immutable
* Reactive

### Domain

* Business logic via services
* Represents the state (structure of the data)
* Consist of entities

## Objectives / Goals

* Try to make the layers Domain, Store & Application Services framework independant


# Other notes:



__Store:__ Ability to add, update, remove from state. Reactive, notify subscribers.

__State:__ The state object or array of objects

__Model:__ Basic template of an entity with state. Methods that help get or set state.

__Service:__ Methods

Domain Layer:
* business logic
* should be agnostic to the view
* consist of entities and domain services.


Model. Entity. Service.

Repository:
* Fetch / Save the data into a source (either API or database)

Models: 
* will usually have data / state
* methods that help to get/set data from the object

Services:
* Methods to perform operations with one or more models



Model: Fields that belong to the object, methods that help to get/set data from the object (a fullname accessor that returns first + last name)

Service: Methods to perform operations with one or more models, see 'unit of work', transactions, etc...

Employee::create should just take a set of data, perform model validation if necessary, and return an Employee Object.

EmployeeService::hireEmployee might create the employee, send them a welcome email, create a mailbox, make them a sandwich, etc... it may return the set of data, or a result code, etc...

This can also affect validation:

Model Validation: Employee must have a id, first and last name, and birthday

Service Validation: Employees for the bartender position must be 21 or over, and approved by a manager.