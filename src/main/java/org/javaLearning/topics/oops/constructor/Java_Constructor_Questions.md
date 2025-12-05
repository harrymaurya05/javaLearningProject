# Java Constructor Questions

## Section 1: Multiple Choice Questions (20 Questions)

### Beginner Level (Questions 1-7)

**1. What is a constructor in Java?**
- A) A method that returns a value
- B) A special method used to initialize objects
- C) A method that destroys objects
- D) A static method


    Ans : B


**2. Which of the following is true about constructors?**
- A) Constructors must have a return type
- B) Constructors have the same name as the class
- C) Constructors cannot be overloaded
- D) Constructors are inherited


    Ans : B


**3. What is the default constructor?**
- A) A constructor with parameters
- B) A constructor provided by the compiler if no constructor is defined
- C) A constructor that returns null
- D) A static constructor


    Ans : B



**4. Can a constructor be private?**
- A) Yes
- B) No
- C) Only in abstract classes
- D) Only in final classes


    Ans : A


**5. How many constructors can a class have?**
- A) Only one
- B) Maximum two
- C) Multiple (constructor overloading)
- D) None


    Ans : c


**6. What happens if you don't define any constructor in a class?**
- A) Compilation error
- B) Java provides a default no-argument constructor
- C) The class cannot be instantiated
- D) Runtime error


    Ans : B


**7. Which keyword is used to call one constructor from another in the same class?**
- A) super()
- B) this()
- C) new
- D) call()


    Ans : B


### Intermediate Level (Questions 8-14)

**8. What is constructor chaining?**
- A) Calling multiple constructors in sequence
- B) Calling one constructor from another constructor
- C) Inheriting constructors from parent class
- D) Creating multiple objects


    Ans : B


**9. When is the super() constructor called?**
- A) At the end of the child constructor
- B) Before the child constructor executes
- C) Only when explicitly called
- D) Never automatically


    Ans : B


**10. Can constructors be synchronized?**
- A) Yes
- B) No
- C) Only default constructors
- D) Only parameterized constructors


    Ans : 


**11. What will happen if both this() and super() are used in a constructor?**
- A) Both will execute successfully
- B) Compilation error
- C) Runtime error
- D) super() will be ignored


    Ans : B   
    Explaintion :- error: call to super must be first statement in constructor
        super();


**12. Can a constructor call an instance method?**
- A) No, never
- B) Yes, but it's risky during object construction
- C) Only static methods can be called
- D) Only final methods can be called


    Ans : B


**13. Which statement is true about constructor overloading?**
- A) Constructors must have different names
- B) Constructors must have different parameter lists
- C) Constructors must have different return types
- D) Constructors cannot be overloaded


    Ans : B


**14. What is a copy constructor?**
- A) A constructor that copies the class definition
- B) A constructor that creates an object by copying another object
- C) A constructor that duplicates the class
- D) Java's default constructor


    Ans : B


### Advanced Level (Questions 15-20)

**15. Can a constructor throw an exception?**
- A) No, constructors cannot throw exceptions
- B) Yes, constructors can throw checked and unchecked exceptions
- C) Only unchecked exceptions
- D) Only checked exceptions


    Ans : B


**16. What happens when you create an object of a child class?**
- A) Only child constructor is called
- B) Parent constructor is called first, then child constructor
- C) Child constructor is called first, then parent constructor
- D) No constructor is called


    Ans : B


**17. Can you call a constructor explicitly after object creation?**
- A) Yes, using the new keyword
- B) Yes, using object.Constructor()
- C) No, constructors are called only during object creation
- D) Yes, using super()


    Ans : 


**18. In what order are instance variables initialized?**
- A) After constructor execution
- B) Before constructor execution
- C) During constructor execution
- D) Random order


    Ans : B


**19. What is the purpose of a private constructor in the Singleton pattern?**
- A) To prevent object creation
- B) To control object creation and ensure only one instance exists
- C) To improve performance
- D) To make the class abstract


    Ans : B


**20. Can an abstract class have a constructor?**
- A) No, abstract classes cannot have constructors
- B) Yes, and it's called when a subclass is instantiated
- C) Only if it has no abstract methods
- D) Only default constructors are allowed


    Ans : B


---

## Section 2: Output-Based Questions (10 Questions)

### Beginner Level (Questions 21-24)

**21. What will be the output?**
```java
class Test {
    Test() {
        System.out.println("Constructor called");
    }
    
    public static void main(String[] args) {
        Test t = new Test();
    }
}
```


    Ans : Constructor called


**22. What will be the output?**
```java
class Box {
    int width;
    
    Box(int w) {
        width = w;
    }
    
    public static void main(String[] args) {
        Box b = new Box(10);
        System.out.println(b.width);
    }
}
```


    Ans : 10


**23. What will be the output?**
```java
class Demo {
    Demo() {
        System.out.println("A");
    }
    
    Demo(int x) {
        System.out.println("B");
    }
    
    public static void main(String[] args) {
        Demo d1 = new Demo();
        Demo d2 = new Demo(5);
    }
}
```


    Ans :   A
            B


**24. What will be the output?**
```java
class Test {
    int x;
    
    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.x);
    }
}
```


    Ans : 0 (because (int x = 0 ) instance variables automatically initialized default values)


### Intermediate Level (Questions 25-27)

**25. What will be the output?**
```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        System.out.println("Child Constructor");
    }
    
    public static void main(String[] args) {
        Child c = new Child();
    }
}
```


    Ans :   Parent Constructor
            Child Constructor

    Because Parent constructor always executes before child constructor. 
    java automatically inserts super()


**26. What will be the output?**
```java
class Test {
    Test() {
        this(10);
        System.out.println("No-arg constructor");
    }
    
    Test(int x) {
        System.out.println("Parameterized constructor: " + x);
    }
    
    public static void main(String[] args) {
        Test t = new Test();
    }
}
```


    Ans :   Parameterized constructor: 10
            No-arg constructor

    because of this keyword (first statement in a constructor)


**27. What will be the output?**
```java
class Demo {
    static {
        System.out.println("Static block");
    }
    
    {
        System.out.println("Instance block");
    }
    
    Demo() {
        System.out.println("Constructor");
    }
    
    public static void main(String[] args) {
        Demo d = new Demo();
    }
}
```


    Ans : 


### Advanced Level (Questions 28-30)

**28. What will be the output?**
```java
class Parent {
    Parent(int x) {
        System.out.println("Parent: " + x);
    }
}

class Child extends Parent {
    Child() {
        super(20);
        System.out.println("Child");
    }
    
    public static void main(String[] args) {
        Child c = new Child();
    }
}
```


    Ans :   Parent: 20
            Child


**29. What will be the output?**
```java
class Test {
    int x;
    
    Test(int x) {
        x = x;
    }
    
    public static void main(String[] args) {
        Test t = new Test(10);
        System.out.println(t.x);
    }
}
```


    Ans : 0
        because in instance variable (this.x) is not initialized,it keeps its default value 0


**30. What will be the output or error?**
```java
class Demo {
    Demo() {
        this(5);
        super();
        System.out.println("Constructor");
    }
    
    Demo(int x) {
        System.out.println("Param: " + x);
    }
    
    public static void main(String[] args) {
        Demo d = new Demo();
    }
}
```

---


    Ans : compilation failed
    because Either this() or super() can be used as the first statement in a constructor.
    You cannot use both in the same constructor.


## Section 3: Tricky Coding Questions (5 Questions)

### Intermediate Level (Questions 31-32)

**31. Create a Singleton class with a private constructor**

Write a class `Database` that:
- Has a private constructor
- Provides only one instance throughout the application
- Has a method `getInstance()` to get the single instance
- Has a method `connect()` that prints "Connected to database"


    Ans : 
```java



```

---


**32. Implement Constructor Chaining**

Create a class `Student` with:
- Three instance variables: name, age, rollNumber
- Constructor 1: Takes only name (sets age=18, rollNumber=0)
- Constructor 2: Takes name and age (sets rollNumber=0)
- Constructor 3: Takes name, age, and rollNumber
- Use constructor chaining with this()
- A display() method to print all details


    Ans : 

```java
class Student{
    String name;
    int age;
    int rollNumber;
    // First Constructor : only name
    Student(String name) {
        this(name, 18, 0); // calls Constructor 3
    }

    //  Second Constructor : name and age
    Student(String name, int age) {
        this(name, age, 0); // calls Constructor 3
    }

    // Third Constructor : name, age, rollNumber
    Student(String name, int age, int rollNumber) {
        this.name = name;
        this.age = age;
        this.rollNumber = rollNumber;
    }
    
    void display(){
        System.out.println("Name : " + name);
        System.out.println("age : " + age);
        System.out.println("rollNumber : " + rollNumber);
    }
    

    public static void main(String[] args) {
        Student s1 = new Student("Kiran");   // calling First Constructor 
        s1.display();

        Student s2 = new Student("Harry", 20);  // calling Second Constructor
        s2.display();

        Student s3 = new Student("Anu", 19, 2025);// calling third Constructor 
        s3.display();
    } 
}
```

---

### Advanced Level (Questions 33-35)

**33. Copy Constructor Challenge**

Create a class `Employee` with:
- Instance variables: id, name, salary
- A parameterized constructor
- A copy constructor that creates a deep copy
- Override the toString() method
- Demonstrate that modifying the copied object doesn't affect the original


    Ans : 
```java

class Employee{
    int id;
    String name;
    int salary;
    // Parameterized constructor
    Employee( int id,String name, int salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    // Copy constructor (deep copy)
    public Employee(Employee other ) {
        this.id = other.id;
        this.name = new String(other.name);
        this.salary = other.salary;
    }

    // Override toString()
    @Override
    public String toString() {
        return "Employee Name: " + name + "\n" +
                "Employee Id: " + id + "\n" +
                "Employee Salary: " + salary;
    }

    public static void main(String[] args) {
        Employee emp1 = new Employee(23, "Kiran", 5000);
        System.out.println("------> Original Employee <------");
        System.out.println(emp1);

        // Create a copy
        System.out.println("------> Copy Employee and Modified <------");
        Employee emp2 = new Employee(emp1);
        emp2.name = "Hariom";
        emp2.salary = 8000;
        System.out.println(emp2);
        System.out.println("------> Original Employee after modifying copy <------ ");
        System.out.println(emp1);
    }
}

```

---

**34. Constructor Exception Handling**

Create a class `BankAccount` with:
- Instance variables: accountNumber, balance
- A constructor that throws a custom exception `InvalidAccountException` if:
  - accountNumber is null or empty
  - balance is negative
- Proper exception handling in the main method
- Methods to deposit and check balance


    Ans : 
```java



```

---



**35. Static vs Instance Initialization**

Create a class `Counter` that demonstrates:
- A static variable to count total objects created
- An instance variable for object ID
- A static initialization block
- An instance initialization block
- A constructor
- Show the execution order when creating multiple objects
- Print the total count and individual object IDs

---


    Ans : 
```java



```

---



**End of Questions**

