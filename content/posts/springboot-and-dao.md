+++
title = 'DAO Design Pattern with Spring Boot'
date = 2024-05-24T21:04:08+05:30
draft = true
+++
It has been a couple of months to me developing a backend driven service for the organization where I'm interning. From hating the J of Java (irrationally) to easily writing complex controller classes and services with Spring Boot, this project has given me my first hands-on experience with Java, Spring Boot, and the DAO design pattern.

## Spring Boot
Spring Boot is a framework based on Java which is used to build web apps and microservices. Built on top of the Spring framework, it is used to quickly build new applications through a convention over configuration based approach to speed up development. The main Spring Boot components are:
* **Spring Boot Starters** - Simplifies dependency management by grouping them for easier management of the dependencies which are related to a specific task.
* **Spring Boot `@AutoConfigurator`** - The auto configurator provides a convention based refinement on the Spring framework to prevent manual custom configuration of loads of application components. This is achieved mainly through annotations.
* **Spring Boot CLI** - 
```
usage: spring [--help] [--version] <command> [<args>]

Available commands are:
  ...
  init       Initialize a new project in the specified directory.
  install    Install an executable script for the Spring CLI.
  run        Run a Spring Groovy script.
  test       Run tests for a Spring application.
  ...
```
* **Spring Boot Actuator** - This provides an entire suite of application health and metrics monitoring features to the Spring application. For example, the health check at the `/health` endpoint for a Spring Boot application with the actuator configured returns the application status:
```json
{
  "status": "UP"
}
```
Safely assuming that the application^^ is up and running. This is one of the many production-grade features the actuator provides.

## DAO Design Pattern
There is a great importance given clean, modular, maintainable code in the industry. For this reason, I was introduced to the **Data Access Object (DAO)** design pattern.
