# Domain-Driver Applications

#### Goals

Build a web application that is driven by the domain / business logic that is independant of the view framework (Angular, React, Vue). We can try and accomplish this using [Domain Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) and a layered architecture.

#### Useful links:

* https://medium.com/hackernoon/architecting-single-page-applications-b842ea633c2e
* https://medium.com/@bojzi/anatomy-of-a-large-angular-application-f098e5e36994
* https://blog.strongbrew.io/A-scalable-angular2-architecture/
* https://medium.com/the-coding-matrix/ddd-101-the-5-minute-tour-7a3037cf53b8
* __Courses:__
  * https://www.pluralsight.com/courses/refactoring-anemic-domain-model


## Glossary

`DDD` - [Domain Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design)

`Business Logic` - Business rules that determine how data can be created, stored and updated

`Domain` - A sphere of knowledge or activity

`Entity` - The actual instance of the object

`Model (Value object)` - Template of an entity. Methods that set / get data. Also includes business logic that relates to the object only. DDD refers to a model as a value object. _Some design patterns state that models should have no business logic, however, DDD (Domain Driven Design) finds this an anti-pattern, and states the model should have business logic if it relates to that object. [Anemic_domain_model](https://en.wikipedia.org/wiki/Anemic_domain_model)_

`Aggregate` - Collection of objects that are bound together by a root entity. I like to use composition to accomplish this.

`Service` - When an operation does not conceptually belong to a single object, you will use services to perform that operation / logic. Methods to perform operations with one or more models.

`Store` - Ability to add, update, remove from state. Reactive, notify subscribers

`State` - The state object or array of objects. The actual data of the entity

`Factory` - Create a domain object / model

`Repository` - The storage where objects are stored

`Vertical separation` - Separate the app into features

`Horizontal separation` - Separate your code into layers

### DDD summary

You model your business using Entities (the ID matters) and Value Objects (the values matter). You use Repositories to retrieve and store them. You create them with the help of Factories. If an object is too complex for a single class, you’ll create Aggregates that will bind Entities & Value Objects under the same root. If a business logic doesn’t belong to a given object, you’ll define Services that will manipulate the involved elements. Eventually, when the state of the business changes (a change that matters to business experts), you’ll publish Domain Events to communicate the change.

__DDD's rule of thumb__ - Bind data and intelligence together and set boundaries to keep them apart (Bounded context, like vertical separation).

## Architecture (layers)

We will use three layers for our horizontal separation of our code.

### App / View Layer

* Uses a framework to display a view _(Angular, React, Vue)_
* Component based _(Dumb and Smart components)_
* Uses reactive state to display data
* Send new state to the store

### Application Services Layer

* Services related to the application
  * Api services for ajax requests
  * Services for manipulating state for the view (make a users name all uppercase)
* Utility functions

### Domain & Store Layer

* Business logic via services & models
* Represents the state (structure of the data)
* Consist of entities & models / value objects _(DDD)_
* Holds the state _(State is immutable and reactive)_

## Common web application functionality

_Below is a list of common features / functionality and what layer it will be
located in._

* Domain models, Domain services & business logic __(Domain)__
* User permissions to access resources / features of the app __(Domain)__
* User authentication / authorization __(Application services)__
* Ajax requests __(Application services)__
* Utility functions __(Application services)__
* Routing __(App / View)__
* Shared UI components (design system) __(App / View)__
* Views, templates & components __(App / View)__

# Our example app

To demonstrate this architecture, we will build an app, it will be a simple app where a user can signin and add notes. The notes can be categoriesed.

### App requirements

__App functionality__

* User signin
* User / App settings
  * Change settings of the app (maybe light / dark theme)
* Authentication via a fake api
* CRUD operations of a note (to a fake database) via api
* CRUD operations of a category (to a fake database) via api
* Some users will only have read access, others will have read & write
* Routing (different pages in the app)
* Search all notes
  * Use web worker so not to block UI thread