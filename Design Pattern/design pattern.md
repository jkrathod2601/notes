**A design pattern is a general reusable solution to a common problem that occurs in software design. It’s not code itself, but a template or blueprint for how to solve a problem in a particular context.**

| Category       | Purpose                                 | Examples                             |
| -------------- | --------------------------------------- | ------------------------------------ |
| **Creational** | How objects are created                 | Singleton, Factory, Abstract Factory |
| **Structural** | How classes/objects are composed        | Adapter, Decorator, Facade, Proxy    |
| **Behavioral** | How objects communicate with each other | Observer, Strategy, Command, State   |

#### **Top Design Patterns to Focus On**

##### **Creational Patterns**

| Pattern              | Description                                          | Real-World Example                      |
| -------------------- | ---------------------------------------------------- | --------------------------------------- |
| **Singleton**        | One instance of a class                              | Logger, Configuration manager           |
| **Factory**          | Creates objects without exposing instantiation logic | `DocumentFactory.create("pdf")`         |
| **Abstract Factory** | Creates families of related objects                  | UI Toolkit (WindowsFactory, MacFactory) |
| **Builder**          | Constructs complex objects step-by-step              | Building a SQL query using a builder    |
| **Prototype**        | Cloning objects                                      | Game object cloning                     |
##### **Structural Patterns**

|Pattern|Description|Real-World Example|
|---|---|---|
|**Adapter**|Converts one interface to another|Power plug adapter|
|**Decorator**|Add responsibilities dynamically|Adding scrollbars to a window|
|**Facade**|Simplifies a complex subsystem|`Spring Facade` to many subsystems|
|**Proxy**|Surrogate for another object|API gateway, Lazy loading|
|**Composite**|Treat groups and individual objects uniformly|File system (folder and file)|

#### **Behavioral Patterns**

|Pattern|Description|Real-World Example|
|---|---|---|
|**Observer**|Notifies all dependents when state changes|UI Event Listeners, Pub/Sub systems|
|**Strategy**|Selects algorithm at runtime|Payment strategy (UPI, Credit Card)|
|**Command**|Encapsulate requests as objects|Undo/Redo functionality|
|**State**|Change behavior based on internal state|Media player (play/pause)|
|**Mediator**|Central object for communication|Chat room mediator between users|

