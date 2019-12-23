# Layer architecture for web apps

* https://medium.com/hackernoon/architecting-single-page-applications-b842ea633c2e
* https://medium.com/@bojzi/anatomy-of-a-large-angular-application-f098e5e36994
* https://blog.strongbrew.io/A-scalable-angular2-architecture/
* 

## App requirements

Build an app where a user can signin and add notes. Notes can be categorised.

__App functionality__

* User signin
* User / App settings
  * Change settings (maybe light / dark theme)
* Authentication via a fake api
* CRUD operations of a note (to a fake database) via api
* CRUD operations of a category (to a fake database) via api
* Some users will only have read access, others will have read & write
* Routing
* Search all notes
  * Use web worker so not to block UI thread

__Most common features / functionality in apps__

_Below is a list of common features / functionality and what layer it will be
located in._

* Data models, Model services & business logic __(Domain)__
* User permissions to access resources / features of the app __(Domain)__
* User authentication / authorization __(Application services)__
* Ajax requests __(Application services)__
  * https://rxjs-dev.firebaseapp.com/api/ajax/ajax
* Utility functions __(Application services)__
* Routing __(App / View)__
* Shared UI components (design system) __(App / View)__
* View, templates & components __(App / View)__


## Architecture (layers)

### App / View Layer

* Uses a framework to display a view
* Component based
  * Dumb and Smart components
* Uses reactive state to display data
* Send new state to the store

### Application Services Layer

* Services related to the application
  * Api services for ajax requests
  * Services for manipulating state for the view (make a users name all uppercase)

### Domain & Store Layer

* Business logic via services
* Represents the state (structure of the data)
* Consist of entities
* Holds the state
  * State is immutable
* Reactive

## Objectives / Goals / Advantages

* Try to make the layers Domain & Store & Application Services framework independant

__Advantages:__

* Multiple developers can easily work on different features / sections of the app
with minimal conflicts
* Easier to migrate the app to a new view library / framework or update it to a new version
* The separation of concern and decoupling makes it easier to maintain & test.


__Disadvantages:__

* Takes more time to develop the app, but you should save time in the future when you need to add features, maintain the app or update its dependencies.


# Other notes:



__Store:__ Ability to add, update, remove from state. Reactive, notify subscribers.

__State:__ The state object or array of objects

__Model:__ Basic template of an entity with state. Methods that help get or set state.

__Model Service:__ Methods to perform operations with one or more models. Can be adding a model, deleting a model, editing a model??


__Vertical separation:__ Separate the app into features. Each feature could theoretical be its own app (but you would have to have a base app to handle routing between the apps)

__Horizontal separation:__ Separate your code into layers



__Features require:__

* Ajax requests
* User authentication / authorization
  * Save token in cookie
* View components (template, binding) (Angular, React or Vue)
* Routing (switching between views)
* Shared custom UI components (design system for that app)


Do we need a facade, where does it sit in?

Domain Layer:
* business logic
* should be detached from the view
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