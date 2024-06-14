# 1 Introduction
The goal with this project is to create a media server/service to which users/clients can upload and download different types of
multimedia (such as videos, audio or pictures). This would take the form of a backend written in rust using the tokio library to perform and handle network
requests. Since need to store all the resources on the server we also need to implement some sort of database. The idea then is that the user through
either a TUI or GUI will be able to play e.g. a video or listen to an audio track. The most interesting part about this project is the versatility, modularization
and feature-potential. It's a good base to expand upon, the plan is to write the frontend in rust as well, therefore sharing of modules between the server and the client
will make development easier and also implementation of shared functionality.
We chose this project among the others since it was well-thought-out, and because of the modularization it will be easier to distribute the workload in a group of 7.
As a team we hope to explore the wonders of rust, and why it's become so popular in such a short period of time. We also want to learn more about networking, databases, concurrency, parallelism and distributed systems.
## 1.1 Desired project features

### 1.1.1 Concurrency
It is a requirement to make use of concurrency in this project. Therefore, we plan to implement it through a server. In our experience, concurrency is mainly used in either large computation or in servers. Since our project does not contain any large computations, we plan to implement concurrency through a server.
### 1.1.2 Modularity
Since we are a relatively large group we want to prioritize modularity in order that we can work efficiently in parallel. If the work is easy This will also make implementeing concurrency easier since functionality and state will be clearly demarcated. 
### 1.1.3 Applicable knowledge
When choosing an idea to implement, we want the different parts of the system to not be specific to this system. We want to 
learn things that can be applicable in most systems so that we can re-use the knowledge that we acquire during this project in future
projects. Therefore, we want to avoid things like graphics programming and similar. Sure, knowing how to program graphics can be 
useful when developing games but that is just on part of the computer industry, compared to knowing how to manage a database, which is a part of almost all systems nowadays.
### 1.1.4 Distributed
Software that is highly concurrent is in our experience either used for high performance computing or is distributed. Since we don't have experience in high performance computing and due to its complexity, we would rather learn how distributed systems work and implement one.
### 1.1.5 CPU and IO intensive
We would like to have the opportunity to learn the characteristics and constraints of concurrency for both IO bound and CPU intensive operations.
### 1.1.6 Parallelism
In case we have to handle a large amount of data which can be processed more efficiently by using parallelism, we need to use operations relevant
to parallelism instead of concurrency when it is needed.
### 1.1.7 Extensibility
In order to avoid a situation in which the project is too ambitious, and we can't finish on time, or too simple, we want the project to have a flexible scope. A core set of functionality should be easy to implement after which further functionality should be easy to implement.
Since we are a relatively large group we want to prioritize modularity in order that we can work efficiently in 
parallel. Different parts of the group won't have to discuss every design decision with the entire group which will 
save time. This also means that everyone can focus on their specific part and not have to know all the details of the 
entire system. This will also make implementing concurrency easier since functionality and state will be clearly demarcated.

### 1.1.8 Usability
We want the system that we choose to implement to be at least somewhat useful to us in the future. This increases the motivation
to continue developing the system. If the system is not going to be used, it feels like it does not really matter if it is good
or not. But if the system is going to be used, the motivation to add extra features and similar increases a lot. Choosing to 
implement a system that is going to be used also makes more sense compared to implementing a system that is not going to be used 
because if the system is going to be used it means that the functionality of the system is not commonly available in some other 
system that already exists.

## 1.2 Alternative project ideas

The alternative idea we discussed the most was to make a game or chat application, or a combination of both.
For the game, we considered different things that could be made efficient with the help of concurrency.
Gameplay-wise, there could be a lot of enemies similar to tower defence games or games with swarms of enemies (For example Vampire Survivors).
Or it could be a multiplayer game, with or without a chat function. 

We concluded that the pros of making a game that used networking for chat or multiplayer would be that we would be working with client-server communication, which was something many of us wanted to do.
And it also would allow for some creativity, which would be fun. The cons were that getting into graphical programming is a very big threshold and separating the project into modules would be more difficult.
So we decided on going with the media server because we agreed it seemed a better option for this group project in the end.

## 1.3 Why others should care

What we want to develop is a usable system that can be applied in many different ways. 

## Learning Goals
### Rust
We wish to learn the Rust programming language; which models of concurrency are supported and how to implement those, as well as how the cargo packet manager works and how testing works. 

### Networking
Most modern day systems incorporate some sort of server-side interactions, such as cloud storage and multiplayer games. Because of this, our second goal is to learn how to create, and communicate between, server side and client side in a larger server/client system. 

### Databases
We also hope to learn about databases, as most applications are built on top some sort of database, including the one we are building in this project.
## Challenges
Aside from concurrency, a lot of what we will be working on in this project is new to some of us and thus difficult to plan around. We have a poor idea of what we will find difficult and what we will breeze through, and we lack an accurate assessment of the size of the different modules. Because of this we won't be starting off with a strict division of work and groups.
### Rust
One challenge will be to learn a new and relatively difficult programming language. This is because of its unique syntax and innovative concepts, such as: ownership, lifetimes, Rust error handling, and support for both functional and imperative programming.
### Database 
Because we're creating a media server we will also have to learn about databases and networking, as well as the challenges they bring. The most notable being database synchronization, which means that the clients should receive the same update to their local database as is being deployed to the server's database. 
### Networking
Networking usually includes a lot of side effects which need to be accounted for in development. Most members of our group also don't know much about networking from before which adds to the list of unfamiliar concepts that need to be learnt.

# 2 Concurrency models and programming languages
## 2.1 Concurrency models
### 2.1.1 Tokio
Tokio is the main runtime for Rust and provides an asynchronous model for writing concurrent systems. Tokio is perfect to explore 
and use in our project because the purpose of it is to handle many connections in a network. Because tokio is an asynchronous model,
it is used for I/O bound operations, or in our case network requests and is fit to make our project plus if we need help with Tokio,
it is the main runtime for Rust and should already have documentation online for us to take help from.
In Tokio, it also has many rust libraries built on top off it which we can integrate with our project. We're also going to have use of most of the submodules in tokio for the project:
1. tokio::net - provides asynchronous networking primitives for building networking applications. By this we can make our network applications
handle many concurrent connections.
2. tokio::io - allows us to read and write data asynchronously, which means that the difference between Asyncwrite and Asyncread from
normal read and write is that other tasks can run while waiting on IO.
3. tokio::time - allows us to make code execute after a set interval of time.
4. tokio::sync - allows independent tasks to communicate to each other via message passing.

Including these submodules, we may use Actix which is built on top off tokio to make http requests and has excellent performance.

### 2.1.2 Rayon
In case we have to introduce parallelism in our project, we have to use the rayon library to divide tasks into parallel tasks.

## 2.2 Why Rust
Our choice of programming language for this project is rust. Rust is a language which focuses on safety and performance. Rust doesn't use a garbage collector and instead uses ownership. This lets the compiler check the code for memory issues using the borrow checker and once the code compiles we can be sure that the code has no memory bugs. We don't have to spend time debugging weird memory issues at runtime, the compiler simply wont let us compile if the code isn't memory safe.
Another reason to why we chose Rust is that it's strict type system makes it very easy to see what another programmer is trying to accomplish. For example, if a function might fail in some way we can wrap it's return value in a `Result<>`. If we don't handle the error we get a compile time warning. In a language like C we could accomplish the same thing by returning special values when something fails, for example returning `NULL`. But we are not forced to handle this error by the compiler. It is not clear in the function specification that this might occur, we need to document it clearly. This helps us in our project because we are so many people, we need the different modules to have clear APIs.
The last reason for choosing Rust is that it is well suited for concurrent programs 
The last reason for choosing Rust is that it is well suited for concurrent programs due to it's focus on safety. The ownership and borrowing system allows for safe management of resources inside concurrent programs. This system ensures that there is only one owner of a resource at a time which prevents data races. The Rust compiler also enforces thread safety by ensuring that data acessed across threads is properly synchronized.
# 3 System architecture
## 3.1 Server Client
The system will use a client server model in which the database is distributed so that all clients can read locally but writes will be sent to the server, which establishes consensus and writes the changes to all client.
## 3.2 Layers
The system will be divided into a number of Rust crates and who will be divided into several layers.
### 3.2.1 Presentation layer
Crates in this layer will allow a user to interact with the system. This layer will be responsible for handling user input and output. It won't have any functionality on its own but instead rely on the application layer. This will make it easy to add new types of interfaces.
### 3.2.2 Application 
Crates in this layer will handle all the business logic and serve as the interface between the presentation layer and the model layer.
### 3.2.3 Model Layer
This layer will interface with the database wrappers and provide data and state to the application layer.
### 3.2.4 IO Layer
This layer will abstract away file and network IO so that it can be used in a platform and implementation agnostic way.
### 3.2.5 Database wrappers
This layer will abstract away specific database types and provide a unified interface for the model layer to use. All sql queries will be defined in this layer so that they can be reused for different database implementations.
## 3.3 Database
For local only databases such as for saving user configuration, local libraries and a list of libraries, SQLite will be used. For libraries that are shared between clients, a distributed version of SQLite, DQLite will be used.

# 4 Development tools

## 4.1 Source code editor
We don't have a specific editor that we are going to use, each person uses what they want, but most will use Clion and it will be used for pair programming. Clion offers excellent integration with the Rust compiler and linter tools such as Clippy. 

## 4.2 Version control software
Git is the most popular version control software, and it is the one we are most familiar with. We are going to host the code on GitHub.

## 4.3 Build tool
Cargo. We chose cargo because it is the built in build tool.

## 4.4 Testing
### 4.4.1 Unit testing
We are going to use the built in method of writing tests i

### 4.4.2 Integration testing
Integration testing will be implemented, for now its hard to say how these will look like since it depends on how we implement the functions.

## 4.5 Documentation generation
Function comments will be written in the Rust doc format. Which is then generated by rustdoc to html. Module and file documentation will be written in markdown in a separate "doc" Folder. And with the help of a tool called pandoc we can then generate the markdown files into LaTeX. 

## 4.6 Communication
We plan to use Discord for informal and urgent communication because it is what we are most familiar with. Communication about the development will be carried out through GitHub issues, pull requests, code reviews and milestones. We will also add a GitHub bot for our Discord channel, so we can get a better understanding and feel for when people are working in the repo. And by enabling Discord notifications on your phone or smartwatch you can always stay up-to date.

# 5 Conclusion