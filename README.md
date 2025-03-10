Apollo
======

[![Circle Status](https://circleci.com/gh/spotify/apollo.svg?style=shield&circle-token=5a9eb086ae3cec87e62fc8b6cdeb783cb318e3b9)](https://circleci.com/gh/spotify/apollo)
[![Codecov](https://img.shields.io/codecov/c/github/spotify/apollo.svg)](https://codecov.io/gh/spotify/apollo)
[![Maven Central](https://img.shields.io/maven-central/v/com.spotify/apollo-parent.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.spotify%22%20apollo*)
[![License](https://img.shields.io/github/license/spotify/apollo.svg)](LICENSE.txt)

## Status: Bug-fix only

Apollo is heavily used within Spotify but most if its development is currently done internally leveraging Apollo's module system. We want to signal this current state to the community by putting the project in maintenance mode.   
This project will no longer have new features or accept PRs for new features. We will continue to accept bug fixes and update dependencies. 


Apollo is a set of Java libraries that we use at Spotify when writing microservices. Apollo includes modules such as an HTTP server and a URI routing system, making it trivial to implement restful API services. 

Apollo has been used in production at Spotify for a long time. As a part of the work to release version 1.0.0 we moved the development of Apollo into the open.

There are three main libraries in Apollo:

* [apollo-http-service](apollo-http-service)
* [apollo-api](apollo-api)
* [apollo-core](apollo-core)

### Apollo HTTP Service
The [apollo-http-service](apollo-http-service) library is a standardized assembly of Apollo
modules. It incorporates both apollo-api and apollo-core and ties them together with other
modules to get a standard api service using http for incoming and outgoing communication.

### Apollo API
The [apollo-api](apollo-api) library is the Apollo library you are most likely to interact with.
It gives you the tools you need to define your service routes and your request/reply handlers.

Here, for example, we define that our service will respond to a GET request on the path `/` with
the string `"hello world"`:
```java
public static void init(Environment environment) {
  environment.routingEngine()
      .registerAutoRoute(Route.sync("GET", "/", requestContext -> "hello world"));
}
```

> Note that, for an Apollo-based service, you can see the routes defined for a service by querying
[`/_meta/0/endpoints`](apollo-api-impl/src/main/java/com/spotify/apollo/meta/model).

The apollo-api library provides several ways to help you define your request/reply handlers.
You can specify how responses should be serialized (such as JSON). Read more about
this library in the [Apollo API Readme](apollo-api).

### Apollo Core
The [apollo-core](apollo-core) library manages the lifecycle (loading, starting, and stopping) of
your service. You do not usually need to interact directly with apollo-core; think of it merely 
as "plumbing". For more information about this library, see the [Apollo Core Readme](apollo-core).

### Apollo Test
In addition to the three main Apollo libraries listed above, to help you write tests for your
service we have an additional library called [apollo-test](apollo-test). It has helpers to set up
a service for testing, and to mock outgoing request responses.

### Getting Started with Apollo
Apollo will be distributed as a set of Maven artifacts, which makes it easy to get started no matter the build tool; Maven, Ant + Ivy or Gradle. Below is a very simple but functional service — more extensive examples are available in the [examples](examples) directory. Until these are released, you can build and install Apollo from source by running `mvn install`.

```java
public final class App {

    public static void main(String... args) throws LoadingException {
        HttpService.boot(App::init, "my-app", args);
    }

    static void init(Environment environment) {
        environment.routingEngine()
            .registerAutoRoute(Route.sync("GET", "/", rc -> "hello world"));
    }
 }
```

### Links

[Introduction Website](https://spotify.github.io/apollo)<br />
[JavaDocs](https://spotify.github.io/apollo/maven/apidocs)<br />
[Maven site](https://spotify.github.io/apollo/maven)

### Diagrams

[![Apollo set-up](https://cdn.rawgit.com/spotify/apollo/master/website/source/set-up.svg)](website/source/set-up.svg)

[![Apollo in runtime](https://cdn.rawgit.com/spotify/apollo/master/website/source/runtime.svg)](website/source/runtime.svg)

## Code of conduct
This project adheres to the [Open Code of Conduct][code-of-conduct]. By participating, you are expected to honor this code.

[code-of-conduct]: https://github.com/spotify/code-of-conduct/blob/master/code-of-conduct.md
