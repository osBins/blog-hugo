+++
title = 'DAO Design Pattern with Spring Boot'
date = 2024-05-26T04:04:08+05:30
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

## DAO Design Pattern (with Spring Boot)
There is a great importance given clean, modular, maintainable code in the industry. For this reason, I was introduced to the **Data Access Object (DAO)** design pattern. It was painful writing code following the structural constraints of the DAO design pattern, but once I got the hang of it, and had started making amendments to the code, I was struck by the impact it had on simplifying my daily living.  
The code I've written consists of 4 main layers:
1. **Controller Layer** - Entrypoint of all requests made to the API.
2. **Service Layer** - Contains business logic and is blissfully unaware of the inner workings of the data retrieval and manipulation process.
3. **Data Access Layer** - Interacts with the database and handles data mapping, query execution to get the service layer whatit needs.
4. **Data Layer** - My use case involved a layer of DTOs for reduced coupling and data validation. The validation is possible through Java's strongly typed nature, enforcing type checking during compile time.  

### A short DAO principle example
The service I'm developing has an entity called `experiment` and for every experiment, there exists a computable `result`.  
If we expand on the flow of data to get the result of a defined experiment; let's say I give the API an experiment number for which I want to get the result. `/experiment/123/result`.

The `Result` object from its data class will be called.
```java
@Accessors
public class Result {
    long controlExposed;
    long controlCount;
    double controlPercentage;

    long variationExposed;
    long variationCount;
    double variationPercentage;

    String winner;
}
```

The DAO layer will then fetch the entities needed for computing the result for the given experiment. This is achieved through the entities and repositories defined in the DAO layer.

```java
@Service
public class ExperimentDaoImpl implements ExperimentDao {
    @Autowired
    private ExperimentRepository experimentRepository;
    public Long getGoalId(Long id) {
        return experimentRepository.findById(id).get().getGoalId();
    }

}
```
Here I'm returning the goal ID, through which we will fetch the goal. The goal object contains the data needed for computing result. After the DAO layer is done doing the heavy-lifting for fetching data, it is passed to the service layer for the ✨ magic ✨.

```java
@Service
public class ExperimentServiceImpl implements ExperimentService {
    @Autowired
    ResultSQLService resultSQLService;

    @Autowired
    private ExperimentDao experimentDao;
    
    @Autowired
    private GoalDaoImpl goalDaoImpl;

    @Override
    public Result getResult(Long expId) {
        Long goalId = experimentDao.getGoalId(expId);
        GoalEntity goal = goalDaoImpl.getGoal(goalId);
        String source = goal.getDataSource();
        return resultSQLService.getResult(goal);
    }
```
Skipping the intricate and non-essential (for the scope of this discussion) calculations performed by the `resultSQLService` class, the result object is return by this service layer to the controller layer, where the request had originated from.

```java
@RestController
public class ExperimentController {
    @Autowired
    private final ExperimentService experimentService;
    @GetMapping("/experiment/{expId}/result")
    public ResponseEntity<Result> getResult(@PathVariable Long expId) {
        return ResponseEntity.status(HttpStatus.OK).body(experimentService.getResult(expId));
    }
}
```
![DAO](https://github.com/osBins/blog-hugo/assets/70942982/e0c04ff4-17b0-45d3-97d6-308fc3ab6ed4#small "Data flow for the different layers in a DAO approach")
