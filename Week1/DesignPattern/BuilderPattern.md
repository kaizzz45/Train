# Builder Pattern

---

## 1. What is Builder Pattern ?

- Builder is a creational design pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

> Builder pattern được tạo ra để xây dựng một đôi tượng phức tạp bằng cách sử dụng các đối tượng đơn giản và sử dụng tiếp cận từng bước, việc xây dựng các đối tượng đôc lập với các đối tượng khác.

## 2. How to implement ?

1.  Define the object to be created and its attributes

```sh
public class Car {
    private String make;
    private String model;
    private int year;
    private String color;
    private String engineType;

    private Car(String make, String model, int year, String color, String engineType) {
        this.make = make;
        this.model = model;
        this.year = year;
        this.color = color;
        this.engineType = engineType;
    }

    // Getters for all attributes
    public String getMake() {
        return make;
    }

    public String getModel() {
        return model;
    }

    public int getYear() {
        return year;
    }

    public String getColor() {
        return color;
    }

    public String getEngineType() {
        return engineType;
    }
}

```

2. Define the builder class with methods to set the object's attributes

```sh

public class CarBuilder {
    private String make;
    private String model;
    private int year;
    private String color;
    private String engineType;

    public CarBuilder setMake(String make) {
        this.make = make;
        return this;
    }

    public CarBuilder setModel(String model) {
        this.model = model;
        return this;
    }

    public CarBuilder setYear(int year) {
        this.year = year;
        return this;
    }

    public CarBuilder setColor(String color) {
        this.color = color;
        return this;
    }

    public CarBuilder setEngineType(String engineType) {
        this.engineType = engineType;
        return this;
    }

    public Car build() {
        return new Car(make, model, year, color, engineType);
    }
}

```

3.  Use the builder to create objects with different configurations

```sh
Car car1 = new CarBuilder()
                .setMake("Toyota")
                .setModel("Camry")
                .setYear(2020)
                .setColor("Blue")
                .setEngineType("Hybrid")
                .build();

Car car2 = new CarBuilder()
                .setMake("Honda")
                .setModel("Civic")
                .setYear(2018)
                .setColor("Red")
                .setEngineType("Gasoline")
                .build();

```

## 3. Pros

✔️ You can construct objects step-by-step, defer construction steps or run steps recursively.

✔️ You can reuse the same construction code when building various representations of products.

✔️ Single Responsibility Principle. You can isolate complex construction code from the business logic of the product.

## 4. Cons

❌ The overall complexity of the code increases since the pattern requires creating multiple new classes.

## 5. Demo

```sh
public class Department {
    private String name;
    private int numOfTeachers;
    private int numOfStudents;

    private Department(String name, int numOfTeachers, int numOfStudents) {
        this.name = name;
        this.numOfTeachers = numOfTeachers;
        this.numOfStudents = numOfStudents;
    }

    public String getName() {
        return name;
    }

    public int getNumOfTeachers() {
        return numOfTeachers;
    }

    public int getNumOfStudents() {
        return numOfStudents;
    }

    public static class Builder {
        private String name;
        private int numOfTeachers;
        private int numOfStudents;

        public Builder() {
        }

        public Builder name(String name) {
            this.name = name;
            return this;
        }

        public Builder numOfTeachers(int numOfTeachers) {
            this.numOfTeachers = numOfTeachers;
            return this;
        }

        public Builder numOfStudents(int numOfStudents) {
            this.numOfStudents = numOfStudents;
            return this;
        }

        public Department build() {
            return new Department(name, numOfTeachers, numOfStudents);
        }
    }
}

```

```sh
public class Teacher {
    private String name;
    private String department;
    private int yearsOfExperience;

    private Teacher(String name, String department, int yearsOfExperience) {
        this.name = name;
        this.department = department;
        this.yearsOfExperience = yearsOfExperience;
    }

    public String getName() {
        return name;
    }

    public String getDepartment() {
        return department;
    }

    public int getYearsOfExperience() {
        return yearsOfExperience;
    }

    public static class Builder {
        private String name;
        private String department;
        private int yearsOfExperience;

        public Builder() {
        }

        public Builder name(String name) {
            this.name = name;
            return this;
        }

        public Builder department(String department) {
            this.department = department;
            return this;
        }

        public Builder yearsOfExperience(int yearsOfExperience) {
            this.yearsOfExperience = yearsOfExperience;
            return this;
        }

        public Teacher build() {
            return new Teacher(name, department, yearsOfExperience);
        }
    }
}

```

Main.java

```sh
Department department = new Department.Builder()
        .name("Mathematics")
        .numOfTeachers(5)
        .numOfStudents(100)
        .build();

Teacher teacher = new Teacher.Builder()
        .name("John Doe")
        .department("Mathematics")
        .yearsOfExperience(10)
        .build();
```
