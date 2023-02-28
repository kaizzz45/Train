# Factory Pattern

---

## 1. What is Factory Pattern ?

- Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.
  > Factory method là một design pattern thuộc nhóm Creational, nó cung cấp một interface để tạo đối tượng cho lớp cha (superclass), nhưng cũng cho phép các lớp con (subclass) thay đổi đối tượng sẽ được tạo.

## 2. How to implement ?

1. Create interface

   Shape.java

   ```sh
   public interface Shape {
   void draw();
   }
   ```

2. Create concrete classes implementing the same interface

Rectangle.java

```sh
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Rectangle::draw() method.");
   }
}
```

Square.java

```sh
public class Square implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Square::draw() method.");
   }
}
```

Circle.java

```sh
public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Inside Circle::draw() method.");
   }
}
```

3. Create Factory to generate object of concrete class based on given information

```sh
public class ShapeFactory {

   //use getShape method to get object of type shape
   public Shape getShape(String shapeType){
      if(shapeType == null){
         return null;
      }
      if(shapeType.equalsIgnoreCase("CIRCLE")){
         return new Circle();

      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
         return new Rectangle();

      } else if(shapeType.equalsIgnoreCase("SQUARE")){
         return new Square();
      }

      return null;
   }
}

```

4. Use the factory to get object of concrete class by passing an information such as type

```sh
public class FactoryPatternDemo {

   public static void main(String[] args) {
      ShapeFactory shapeFactory = new ShapeFactory();

      //get an object of Circle and call its draw method.
      Shape shape1 = shapeFactory.getShape("CIRCLE");

      //call draw method of Circle
      shape1.draw();

      //get an object of Rectangle and call its draw method.
      Shape shape2 = shapeFactory.getShape("RECTANGLE");

      //call draw method of Rectangle
      shape2.draw();

      //get an object of Square and call its draw method.
      Shape shape3 = shapeFactory.getShape("SQUARE");

      //call draw method of square
      shape3.draw();
   }
}
```

5. Verify output .

## 3. Pros

✔️ You avoid tight coupling between the creator and the concrete products.

✔️ Single Responsibility Principle. You can move the product creation code into one place in the program, making the code easier to support.

✔️ Open/Closed Principle. You can introduce new types of products into the program without breaking existing client code.

## 4. Cons

❌ The code may become more complicated since you need to introduce a lot of new subclasses to implement the pattern. The best case scenario is when you’re introducing the pattern into an existing hierarchy of creator classes.

## 5. Demo

```sh

public abstract class SchoolMember {
    private String name;

    public SchoolMember(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }

    public abstract void introduce();
}

```

```sh

public class Department extends SchoolMember {
    public Department(String name) {
        super(name);
    }

    @Override
    public void introduce() {
        System.out.println("I am a department named " + this.getName());
    }
}
```

```sh

public class Teacher extends SchoolMember {
    public Teacher(String name) {
        super(name);
    }

    @Override
    public void introduce() {
        System.out.println("I am a teacher named " + this.getName());
    }
}
```

```sh
public class Student extends SchoolMember {
    private int grade;

    public Student(String name, int grade) {
        super(name);
        this.grade = grade;
    }

    public int getGrade() {
        return this.grade;
    }

    public void setGrade(int grade) {
        this.grade = grade;
    }

    @Override
    public void introduce() {
        System.out.println("I am a student named " + this.getName() + ", in grade " + this.getGrade());
    }
}
```

```sh
public class SchoolMemberFactory {
    public static SchoolMember createSchoolMember(String type, String name, int grade) {
        switch (type) {
            case "department":
                return new Department(name);
            case "teacher":
                return new Teacher(name);
            case "student":
                return new Student(name, grade);
            default:
                throw new IllegalArgumentException("Invalid type: " + type);
        }
    }
}

```

Main.java

```sh
public static void main(String[] args) {
   SchoolMember mathDepartment = SchoolMemberFactory.createSchoolMember("department", "Mathematics Department", 0);
   SchoolMember johnDoe = SchoolMemberFactory.createSchoolMember("teacher", "John Doe", 0);
   SchoolMember janeDoe = SchoolMemberFactory.createSchoolMember("student", "Jane Doe", 10);

   mathDepartment.introduce();
   johnDoe.introduce();
   janeDoe.introduce();
}
```

Result

> I am a department named Mathematics Department
> I am a teacher named John Doe
> I am a student named Jane Doe, in grade 10
