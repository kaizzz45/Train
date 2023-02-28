# Prototype Pattern

---

## 1. What is Prototype Pattern ?

- **Prototype** is a creational design pattern that lets you copy existing objects without making your code dependent on their classes.
  > Prototype là một design pattern thuộc nhóm creational, giúp bạn sao chép một đối tượng mà code của bạn sẽ không phụ thuộc vào lớp của đối tượng đó.

## 2. How to implement ?

1.  Create the prototype class

```sh
public class Person implements Cloneable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public Person clone() {
        try {
            return (Person) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```

2.  Clone the prototype object

```sh
Person john = new Person("John", 30);
Person clone = john.clone();

```

3. Modify the cloned object

```sh
clone.setName("Jane");
clone.setAge(25);

System.out.println(john.getName() + " " + john.getAge());   // Output: John 30
System.out.println(clone.getName() + " " + clone.getAge()); // Output: Jane 25
```

## 3. Pros

✔️ You can clone objects without coupling to their concrete classes.

✔️ You can get rid of repeated initialization code in favor of cloning pre-built prototypes.

✔️ You can produce complex objects more conveniently.

✔️ You get an alternative to inheritance when dealing with configuration presets for complex objects.

## 4. Cons

❌ Cloning complex objects that have circular references might be very tricky.

## 5. Demo

```sh
public abstract class Department implements Cloneable {
    private String name;

    public Department(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

```sh
public class Teacher implements Cloneable {
    private String name;

    public Teacher(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

```sh
public class MathDepartment extends Department {
    private List<Teacher> teachers;

    public MathDepartment(String name, List<Teacher> teachers) {
        super(name);
        this.teachers = teachers;
    }

    public List<Teacher> getTeachers() {
        return this.teachers;
    }

    public void setTeachers(List<Teacher> teachers) {
        this.teachers = teachers;
    }

    @Override
    public Object clone() throws CloneNotSupportedException {
        List<Teacher> clonedTeachers = new ArrayList<>();
        for (Teacher teacher : this.getTeachers()) {
            clonedTeachers.add((Teacher) teacher.clone());
        }

        MathDepartment clonedDepartment = new MathDepartment(this.getName(), clonedTeachers);
        return clonedDepartment;
    }
}

```

```sh

public class ScienceDepartment extends Department {
    private List<Teacher> teachers;

    public ScienceDepartment(String name, List<Teacher> teachers) {
        super(name);
        this.teachers = teachers;
    }

    public List<Teacher> getTeachers() {
        return this.teachers;
    }

    public void setTeachers(List<Teacher> teachers) {
        this.teachers = teachers;
    }

    @Override
    public Object clone() throws CloneNotSupportedException {
        List<Teacher> clonedTeachers = new ArrayList<>();
        for (Teacher teacher : this.getTeachers()) {
            clonedTeachers.add((Teacher) teacher.clone());
        }

        ScienceDepartment clonedDepartment = new ScienceDepartment(this.getName(), clonedTeachers);
        return clonedDepartment;
    }
}

```

```sh
public static void main(String[] args) {
   List<Teacher> mathTeachers = new ArrayList<>();
    mathTeachers.add(new Teacher("John Doe"));
    mathTeachers.add(new Teacher("Jane Doe"));

    Department mathDepartment = new MathDepartment("Mathematics", mathTeachers);

    try {
        Department clonedDepartment = (Department) mathDepartment.clone();
        System.out.println("Original Department: " + mathDepartment.getName());
        System.out.println("Cloned Department: " + clonedDepartment.getName());
        System.out.println("Original Teachers: " + mathDepartment.getTeachers());
        System.out.println("Cloned Teachers: " + clonedDepartment.getTeachers());
    } catch (CloneNotSupportedException e) {
        e.printStackTrace();
    }
}
```
