# RestfulQueries [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/apavlidi/RestfulQueries/wiki/How-to-contribute) [![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.apavlidi/restfulQueries/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.github.apavlidi/restfulQueries)

Develop true restful APIs by supporting pagination, filtering, selection, sorting, and searching. This project helps you add these features to your REST Controller easily without developing custom solutions.
The project is currently only compatible with Spring Data MongoDB applications.
There is a blog post [here](https://dev.to/apavlidi/how-to-support-filters-to-your-restful-apis-with-spring-data-mongodb-355a), where I describe step-by-step the implementation of this library.

## Getting Started
For Maven-based projects, add the following to your pom.xml file. This dependency is available from the Maven Central repository.

```xml
<dependency>
    <groupId>com.github.apavlidi</groupId>
    <artifactId>restfulQueries</artifactId>
    <version>0.0.1</version>
</dependency>
```

## Usage
 1. Add a RequestParam of type Map to your Rest Controller.
 ```java
   @GetMapping("/profile")
    private List<Profile> getAllProfiles(@RequestParam Map <String, String> filters) {
        ....
    }
  ```
 
 2. Call the <b>collectRestApiParams()</b> inside your controller and pass the RequestParam map.
 ```java
    Map<String, String> restApiQueries = collectRestApiParams(filters);
```

 3. Pass the filters to your service/repository and before calling the Spring Data MongoDB API, call <b>applyRestApiQueries()</b> and pass your query variable.
```java
  @Override
  public List<Profile> getAllProfilesDemo(Map<String, String> filters) {
      Query query = new Query();
      applyRestApiQueries(query, restApiQueries);
      return mongoTemplate.find(query, Profile.class);
  }
```
Navigate to API Documentation for [more](https://github.com/apavlidi/RestfulQueries/wiki/API-Documentation)

## Documentation

RestfulQueries documentation is available [here](https://github.com/apavlidi/RestfulQueries/wiki/API-Documentation).  

## Contributing

The main purpose of this repository is provide an easy way of implementing truly restful apis by supporting the features of pagination, selection, filtering, and sorting to the developers. Development of RestfulQueries happens here on GitHub, and we are grateful to the community for contributing bugfixes and improvements.

### Contributing Guide

Read the [contributing guide](https://github.com/apavlidi/RestfulQueries/wiki/How-to-contribute) to learn about the development process, how to propose bugfixes and improvements, and how to build and test your changes to RestfulQueries.

### Good First Issues

To help you get your feet wet and get you familiar with the contribution process, check the issues for [good first issues](https://github.com/apavlidi/RestfulQueries/issues) that contain bugs or enhancements with relatively limited scope. This is a great place to get started.

### Feedback

Suggestions and/or improvements are welcome!

### Licensing
This project is licensed under the [MIT License](https://github.com/apavlidi/RestfulQueries/blob/master/LICENSE)

