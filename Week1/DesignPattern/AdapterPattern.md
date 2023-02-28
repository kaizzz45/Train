# Adapter Pattern

---

## 1.What is Adapter Pattern ?

- **Adapter** is a structural design pattern that allows objects with incompatible interfaces to collaborate.

> **Adapter** is alà một design pattern thuộc nhóm structural cho phép các đối tượng có interface không tương thích cộng tác với nhau.

## 2. How to implement ?

1. Create a class on which Criteria is to be applied.
2. Create an interface for Criteria.
3. Create concrete classes implementing the Criteria interface.
4. Use different Criteria and their combination to filter out persons.
5. Verify the output

## 3. Pros

✔️ Single Responsibility Principle. You can separate the interface or data conversion code from the primary business logic of the program.

✔️ Open/Closed Principle. You can introduce new types of adapters into the program without breaking the existing client code, as long as they work with the adapters through the client interface.

## 4. Cons

❌ The overall complexity of the code increases because you need to introduce a set of new interfaces and classes. Sometimes it’s simpler just to change the service class so that it matches the rest of your code.

## 5.Demo

```sh

public class Department {
    private String name;
    private List<Student> students;

    public Department(String name, List<Student> students) {
        this.name = name;
        this.students = students;
    }

    public String getName() {
        return name;
    }

    public List<Student> getStudents() {
        return students;
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public void removeStudent(Student student) {
        students.remove(student);
    }
}
```

```sh
public interface Teacher {
    void teach();
    void gradePapers();
}
```

```sh
public class DepartmentAdapter implements Teacher {
    private Department department;

    public DepartmentAdapter(Department department) {
        this.department = department;
    }

    public void teach() {
        List<Student> students = department.getStudents();
        for (Student student : students) {
            student.learn();
        }
    }

    public void gradePapers() {
        List<Student> students = department.getStudents();
        for (Student student : students) {
            student.doHomework();
        }
    }
}

```

```sh
public class Student {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    public void learn() {
        System.out.println(name + " is learning.");
    }

    public void doHomework() {
        System.out.println(name + " is doing homework.");
    }
}
```

```sh
public class Main {
    public static void main(String[] args) {

        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice"));
        students.add(new Student("Bob"));
        students.add(new Student("Charlie"));
        Department department = new Department("Mathematics", students);


        Teacher teacher = new DepartmentAdapter(department);
teach and grade papers
        teacher.teach();
        teacher.gradePapers();
    }
}
```
