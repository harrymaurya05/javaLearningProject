# Java Constructor Questions

## Section 1: Multiple Choice Questions (20 Questions)

### Beginner Level (Questions 1-7)

**1. What is a constructor in Java?**
- A) A method that returns a value
- B) A special method used to initialize objects
- C) A method that destroys objects
- D) A static method

**2. Which of the following is true about constructors?**
- A) Constructors must have a return type
- B) Constructors have the same name as the class
- C) Constructors cannot be overloaded
- D) Constructors are inherited

**3. What is the default constructor?**
- A) A constructor with parameters
- B) A constructor provided by the compiler if no constructor is defined
- C) A constructor that returns null
- D) A static constructor

**4. Can a constructor be private?**
- A) Yes
- B) No
- C) Only in abstract classes
- D) Only in final classes

**5. How many constructors can a class have?**
- A) Only one
- B) Maximum two
- C) Multiple (constructor overloading)
- D) None

**6. What happens if you don't define any constructor in a class?**
- A) Compilation error
- B) Java provides a default no-argument constructor
- C) The class cannot be instantiated
- D) Runtime error

**7. Which keyword is used to call one constructor from another in the same class?**
- A) super()
- B) this()
- C) new
- D) call()

### Intermediate Level (Questions 8-14)

**8. What is constructor chaining?**
- A) Calling multiple constructors in sequence
- B) Calling one constructor from another constructor
- C) Inheriting constructors from parent class
- D) Creating multiple objects

**9. When is the super() constructor called?**
- A) At the end of the child constructor
- B) Before the child constructor executes
- C) Only when explicitly called
- D) Never automatically

**10. Can constructors be synchronized?**
- A) Yes
- B) No
- C) Only default constructors
- D) Only parameterized constructors

**11. What will happen if both this() and super() are used in a constructor?**
- A) Both will execute successfully
- B) Compilation error
- C) Runtime error
- D) super() will be ignored

**12. Can a constructor call an instance method?**
- A) No, never
- B) Yes, but it's risky during object construction
- C) Only static methods can be called
- D) Only final methods can be called

**13. Which statement is true about constructor overloading?**
- A) Constructors must have different names
- B) Constructors must have different parameter lists
- C) Constructors must have different return types
- D) Constructors cannot be overloaded

**14. What is a copy constructor?**
- A) A constructor that copies the class definition
- B) A constructor that creates an object by copying another object
- C) A constructor that duplicates the class
- D) Java's default constructor

### Advanced Level (Questions 15-20)

**15. Can a constructor throw an exception?**
- A) No, constructors cannot throw exceptions
- B) Yes, constructors can throw checked and unchecked exceptions
- C) Only unchecked exceptions
- D) Only checked exceptions

**16. What happens when you create an object of a child class?**
- A) Only child constructor is called
- B) Parent constructor is called first, then child constructor
- C) Child constructor is called first, then parent constructor
- D) No constructor is called

**17. Can you call a constructor explicitly after object creation?**
- A) Yes, using the new keyword
- B) Yes, using object.Constructor()
- C) No, constructors are called only during object creation
- D) Yes, using super()

**18. In what order are instance variables initialized?**
- A) After constructor execution
- B) Before constructor execution
- C) During constructor execution
- D) Random order

**19. What is the purpose of a private constructor in the Singleton pattern?**
- A) To prevent object creation
- B) To control object creation and ensure only one instance exists
- C) To improve performance
- D) To make the class abstract

**20. Can an abstract class have a constructor?**
- A) No, abstract classes cannot have constructors
- B) Yes, and it's called when a subclass is instantiated
- C) Only if it has no abstract methods
- D) Only default constructors are allowed

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

## Section 3: Tricky Coding Questions (5 Questions)

### Intermediate Level (Questions 31-32)

**31. Create a Singleton class with a private constructor**

Write a class `Database` that:
- Has a private constructor
- Provides only one instance throughout the application
- Has a method `getInstance()` to get the single instance
- Has a method `connect()` that prints "Connected to database"

**32. Implement Constructor Chaining**

Create a class `Student` with:
- Three instance variables: name, age, rollNumber
- Constructor 1: Takes only name (sets age=18, rollNumber=0)
- Constructor 2: Takes name and age (sets rollNumber=0)
- Constructor 3: Takes name, age, and rollNumber
- Use constructor chaining with this()
- A display() method to print all details

### Advanced Level (Questions 33-35)

**33. Copy Constructor Challenge**

Create a class `Employee` with:
- Instance variables: id, name, salary
- A parameterized constructor
- A copy constructor that creates a deep copy
- Override the toString() method
- Demonstrate that modifying the copied object doesn't affect the original

**34. Constructor Exception Handling**

Create a class `BankAccount` with:
- Instance variables: accountNumber, balance
- A constructor that throws a custom exception `InvalidAccountException` if:
  - accountNumber is null or empty
  - balance is negative
- Proper exception handling in the main method
- Methods to deposit and check balance

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

**End of Questions**

