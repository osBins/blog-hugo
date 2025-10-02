+++
title = "Questions that will probably come back"
date = 2025-10-03T02:06:53+05:30
description = "Practice makes perfect."
draft = false
+++

### 1. Get distinct employee names in a company using Java 8 Streams API
**Requirements**  
1. Company class
2. Employee class  

Company can have multiple employees.

**Objective**  
Return a list of the names of distinct employees in the company which have an ID greater than a given numeric ID.

```java
public class Employee implements EmployeeInterface {
    private String id;
    private String name;

    public Employee(String id, String name) {
        this.id = id;
        this.name = name;
    }

    public String getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}

```

```java
public class Company implements CompanyInterface {
    private List<Employee> employees;

    public Company(List<Employee> employees) {
        this.employees = employees;
    }

    public List<Employee> getEmployees() {
        return employees;
    }

    // originally implemented using Set
    // and .toSet() but this is better:
    public List<String> getEmployeesBasedOnEmployeeId(String idThreshold) {
        int threshold = Integer.parseInt(idThreshold);

        return employees.stream()
            .filter(employee -> Integer.parseInt(employee.getId()) > threshold)
            .map(employee -> employee.getName())
            .distinct()
            .collect(Collectors.toList());
    }
}
```

### 2. Maximum sub-array sum (Kadane's algorithm)
```
--- loop ---
1. maximum = Math.max(maximum + arr[i], arr[i]);
2. ans = Math.max(ans, maximum);
```
1. Include current element in `maximum` sum OR start `maximum` from current element (will happen when maximum till last element < 0).
2. Update `ans`
  
Hint on doing this for a circular list: minimising the sub-array sum.

### 3. Finding elements with a key present in MongoDB
```sql
db.collection.find(
    { "key": { $exists: true } 
})
```



