# Singleton Pattern

---

## 1. What is Singleton Pattern ?

- Singleton is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.
  > **Singleton** là một design pattern thuộc nhóm creational giúp bạn tạo ra một lớp chỉ với một thực thế duy nhất, trong khi cung cấp điểm truy cập toàn cục cho thực thế đấy.

## 2. How to implement ?

1. Create a Singleton Class.

```sh
public class SingleObject {

   //create an object of SingleObject
   private static SingleObject instance = new SingleObject();

   //make the constructor private so that this class cannot be
   //instantiated
   private SingleObject(){}

   //Get the only object available
   public static SingleObject getInstance(){
      return instance;
   }

   public void showMessage(){
      System.out.println("Hello World!");
   }
}

```

2. Get the only object from the singleton class.

```sh
public class SingletonPatternDemo {
   public static void main(String[] args) {

      //illegal construct
      //Compile Time Error: The constructor SingleObject() is not visible
      //SingleObject object = new SingleObject();

      //Get the only object available
      SingleObject object = SingleObject.getInstance();

      //show the message
      object.showMessage();
   }
}
```

3. Verify the output.
   > Hello World!

## 3. Pros

✔️ You can be sure that a class has only a single instance.

✔️You gain a global access point to that instance.

✔️The singleton object is initialized only when it’s requested for the first time.

## 4. Cons

❌ Violates the Single Responsibility Principle. The pattern solves two problems at the time.

❌The Singleton pattern can mask bad design, for instance, when the components of the program know too much about each other.

❌The pattern requires special treatment in a multithreaded environment so that multiple threads won’t create a singleton object several times.

❌It may be difficult to unit test the client code of the Singleton because many test frameworks rely on inheritance when producing mock objects. Since the constructor of the singleton class is private and overriding static methods is impossible in most languages, you will need to think of a creative way to mock the singleton. Or just don’t write the tests. Or don’t use the Singleton pattern.

## 5. Demo

**School.java**

```sh
public class School {
    private static School instance = null;
    private String name;
    private List<Teacher> teachers;
    private List<Department> departments;

    private School(String name) {
        this.name = name;
        this.teachers = new ArrayList<>();
        this.departments = new ArrayList<>();
    }

    public static School getInstance(String name) {
        if (instance == null) {
            instance = new School(name);
        }
        return instance;
    }

    public void addTeacher(Teacher teacher) {
        this.teachers.add(teacher);
    }

    public void addDepartment(Department department) {
        this.departments.add(department);
    }

    public List<Teacher> getTeachers() {
        return this.teachers;
    }

    public List<Department> getDepartments() {
        return this.departments;
    }

    public String getName() {
        return this.name;
    }
}
```

**Department.java**

```sh
public class Department {
    private String name;

    public Department(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}

```

Teacher.java

```sh
public class Teacher {
    private String name;

    public Teacher(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}
```

Main.java

```sh
School mySchool = School.getInstance("ABC School");

Department mathDept = new Department("Mathematics");
Department scienceDept = new Department("Science");

Teacher mathTeacher = new Teacher("John Doe");
Teacher scienceTeacher = new Teacher("Jane Doe");

mathDept.addTeacher(mathTeacher);
scienceDept.addTeacher(scienceTeacher);

mySchool.addDepartment(mathDept);
mySchool.addDepartment(scienceDept);

List<Department> departments = mySchool.getDepartments();

for (Department department : departments) {
    System.out.println("Department Name: " + department.getName());
    List<Teacher> teachers = department.getTeachers();
    for (Teacher teacher : teachers) {
        System.out.println("Teacher Name: " + teacher.getName());
    }
}

```
