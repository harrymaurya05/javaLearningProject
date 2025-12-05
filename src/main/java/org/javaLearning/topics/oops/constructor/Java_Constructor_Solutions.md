# Java Constructor Solutions with Detailed Explanations

## Section 1: Multiple Choice Questions - Solutions

### Beginner Level

**1. Answer: B) A special method used to initialize objects**

**Explanation:**
A constructor is a special method that is automatically called when an object is created. Its primary purpose is to initialize the object's state (instance variables).

Example:
```java
class Car {
    String model;
    int year;
    
    // Constructor to initialize object
    Car(String m, int y) {
        model = m;
        year = y;
    }
}

// Usage
Car myCar = new Car("Tesla", 2024); // Constructor called automatically
```

---

**2. Answer: B) Constructors have the same name as the class**

**Explanation:**
Constructors must have the exact same name as the class name and have no return type (not even void).

Example:
```java
class Student {
    String name;
    
    // Correct: Constructor name matches class name
    Student(String name) {
        this.name = name;
    }
    
    // Wrong: This is a regular method, not a constructor
    void Student(String name) {
        this.name = name;
    }
}
```

---

**3. Answer: B) A constructor provided by the compiler if no constructor is defined**

**Explanation:**
If you don't write any constructor, Java automatically provides a default no-argument constructor that initializes instance variables to default values (0, null, false).

Example:
```java
class Book {
    String title;
    int pages;
}

// Java automatically provides:
// Book() { }

// Usage
Book b = new Book(); // Uses default constructor
System.out.println(b.pages); // Output: 0
```

---

**4. Answer: A) Yes**

**Explanation:**
Constructors can be private. This is useful for:
- Singleton pattern (controlling object creation)
- Factory methods
- Preventing instantiation of utility classes

Example:
```java
class Singleton {
    private static Singleton instance;
    
    // Private constructor prevents external instantiation
    private Singleton() {
        System.out.println("Singleton created");
    }
    
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

// Usage
// Singleton s = new Singleton(); // ERROR: Constructor is private
Singleton s = Singleton.getInstance(); // Correct way
```

---

**5. Answer: C) Multiple (constructor overloading)**

**Explanation:**
A class can have multiple constructors with different parameter lists. This is called constructor overloading.

Example:
```java
class Rectangle {
    int length, width;
    
    // Constructor 1: No parameters
    Rectangle() {
        length = width = 1;
    }
    
    // Constructor 2: One parameter (square)
    Rectangle(int side) {
        length = width = side;
    }
    
    // Constructor 3: Two parameters
    Rectangle(int l, int w) {
        length = l;
        width = w;
    }
}

// Usage
Rectangle r1 = new Rectangle();        // 1x1
Rectangle r2 = new Rectangle(5);       // 5x5
Rectangle r3 = new Rectangle(4, 6);    // 4x6
```

---

**6. Answer: B) Java provides a default no-argument constructor**

**Explanation:**
If no constructor is defined, Java automatically adds a default constructor. However, once you define any constructor, the default constructor is no longer provided.

Example:
```java
// Case 1: No constructor defined
class Test1 {
    int x;
}
Test1 t1 = new Test1(); // Works - default constructor provided

// Case 2: Constructor defined
class Test2 {
    int x;
    Test2(int x) { this.x = x; }
}
// Test2 t2 = new Test2(); // ERROR: No default constructor
Test2 t2 = new Test2(10); // Works
```

---

**7. Answer: B) this()**

**Explanation:**
`this()` is used to call another constructor in the same class. `super()` is used to call the parent class constructor.

Example:
```java
class Employee {
    String name;
    int id;
    double salary;
    
    Employee(String name) {
        this(name, 0); // Calls constructor 2
    }
    
    Employee(String name, int id) {
        this(name, id, 0.0); // Calls constructor 3
    }
    
    Employee(String name, int id, double salary) {
        this.name = name;
        this.id = id;
        this.salary = salary;
    }
}
```

---

### Intermediate Level

**8. Answer: B) Calling one constructor from another constructor**

**Explanation:**
Constructor chaining is the process of calling one constructor from another constructor using `this()` or `super()`. It helps avoid code duplication.

Example:
```java
class Phone {
    String brand;
    String model;
    int price;
    
    Phone(String brand) {
        this(brand, "Unknown", 0); // Chain to 3-param constructor
    }
    
    Phone(String brand, String model) {
        this(brand, model, 0); // Chain to 3-param constructor
    }
    
    Phone(String brand, String model, int price) {
        this.brand = brand;
        this.model = model;
        this.price = price;
    }
}

// Usage
Phone p1 = new Phone("Apple");
Phone p2 = new Phone("Samsung", "S24");
Phone p3 = new Phone("Google", "Pixel", 999);
```

---

**9. Answer: B) Before the child constructor executes**

**Explanation:**
When creating a child class object, the parent constructor is automatically called first (either explicitly with `super()` or implicitly). This ensures proper initialization of inherited members.

Example:
```java
class Animal {
    Animal() {
        System.out.println("1. Animal constructor");
    }
}

class Dog extends Animal {
    Dog() {
        // super() is called implicitly here first
        System.out.println("2. Dog constructor");
    }
}

// Usage
Dog d = new Dog();
// Output:
// 1. Animal constructor
// 2. Dog constructor
```

---

**10. Answer: B) No**

**Explanation:**
Constructors cannot be synchronized because synchronization is needed for methods that can be called by multiple threads on an already created object. A constructor is only called once during object creation.

Example:
```java
class Test {
    // synchronized Test() { } // COMPILATION ERROR
    
    // Instead, synchronize the initialization logic
    private static Test instance;
    
    public static synchronized Test getInstance() {
        if (instance == null) {
            instance = new Test();
        }
        return instance;
    }
}
```

---

**11. Answer: B) Compilation error**

**Explanation:**
You cannot use both `this()` and `super()` in the same constructor because both must be the first statement. You can only have one first statement.

Example:
```java
class Parent {
    Parent(int x) { }
}

class Child extends Parent {
    Child() {
        this(5);    // Must be first
        super(10);  // ERROR: Cannot have two first statements
    }
    
    Child(int x) {
        super(x);
    }
}
```

---

**12. Answer: B) Yes, but it's risky during object construction**

**Explanation:**
You can call instance methods from a constructor, but it's dangerous because:
- The object is not fully constructed yet
- If the method is overridden in a subclass, it might access uninitialized variables

Example:
```java
class Parent {
    int value;
    
    Parent() {
        value = 10;
        display(); // Calls Child's display() if Child object is created
    }
    
    void display() {
        System.out.println("Parent: " + value);
    }
}

class Child extends Parent {
    int childValue = 20;
    
    @Override
    void display() {
        // childValue not initialized yet when called from Parent constructor!
        System.out.println("Child: " + value + ", " + childValue);
    }
}

// Usage
Child c = new Child(); // Output: Child: 10, 0 (childValue not initialized!)
```

---

**13. Answer: B) Constructors must have different parameter lists**

**Explanation:**
Constructor overloading requires different parameters (number, type, or order). The name is always the same as the class name.

Example:
```java
class Account {
    String accountNumber;
    double balance;
    String accountType;
    
    // Overloaded constructors - different parameters
    Account(String accNum) {
        this.accountNumber = accNum;
    }
    
    Account(String accNum, double bal) {
        this.accountNumber = accNum;
        this.balance = bal;
    }
    
    Account(String accNum, double bal, String type) {
        this.accountNumber = accNum;
        this.balance = bal;
        this.accountType = type;
    }
}
```

---

**14. Answer: B) A constructor that creates an object by copying another object**

**Explanation:**
A copy constructor takes an object of the same class as a parameter and copies its values to create a new object. Java doesn't provide this automatically (unlike C++).

Example:
```java
class Point {
    int x, y;
    
    // Regular constructor
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    // Copy constructor
    Point(Point p) {
        this.x = p.x;
        this.y = p.y;
    }
}

// Usage
Point p1 = new Point(10, 20);
Point p2 = new Point(p1); // Copy of p1
p2.x = 30;
System.out.println(p1.x); // 10 (unchanged)
System.out.println(p2.x); // 30
```

---

### Advanced Level

**15. Answer: B) Yes, constructors can throw checked and unchecked exceptions**

**Explanation:**
Constructors can throw exceptions to signal that object creation failed. This is useful for validation.

Example:
```java
class Age {
    int value;
    
    Age(int age) throws IllegalArgumentException {
        if (age < 0 || age > 150) {
            throw new IllegalArgumentException("Invalid age: " + age);
        }
        this.value = age;
    }
}

// Usage
try {
    Age a1 = new Age(25);      // OK
    Age a2 = new Age(-5);      // Throws exception
} catch (IllegalArgumentException e) {
    System.out.println(e.getMessage());
}
```

---

**16. Answer: B) Parent constructor is called first, then child constructor**

**Explanation:**
Object construction follows a top-down hierarchy: parent class constructor executes first, then child class constructor. This ensures inherited members are initialized before child-specific members.

Example:
```java
class GrandParent {
    GrandParent() {
        System.out.println("1. GrandParent");
    }
}

class Parent extends GrandParent {
    Parent() {
        System.out.println("2. Parent");
    }
}

class Child extends Parent {
    Child() {
        System.out.println("3. Child");
    }
}

// Usage
Child c = new Child();
// Output:
// 1. GrandParent
// 2. Parent
// 3. Child
```

---

**17. Answer: C) No, constructors are called only during object creation**

**Explanation:**
Constructors can only be invoked during object creation using the `new` keyword. You cannot call them like regular methods on an existing object.

Example:
```java
class Test {
    int x;
    
    Test(int x) {
        this.x = x;
    }
}

// Usage
Test t = new Test(10);  // Constructor called during creation
// t.Test(20);          // ERROR: Cannot call constructor on existing object
t.x = 20;               // Use setter or direct access instead
```

---

**18. Answer: B) Before constructor execution**

**Explanation:**
Initialization order in Java:
1. Static variables and static blocks (class loading)
2. Instance variables and instance initialization blocks
3. Constructor

Example:
```java
class Demo {
    int x = 10;  // Instance variable initialized first
    
    {
        System.out.println("Instance block: x = " + x); // Second
        x = 20;
    }
    
    Demo() {
        System.out.println("Constructor: x = " + x); // Third
        x = 30;
    }
}

// Usage
Demo d = new Demo();
// Output:
// Instance block: x = 10
// Constructor: x = 20
```

---

**19. Answer: B) To control object creation and ensure only one instance exists**

**Explanation:**
In the Singleton pattern, a private constructor prevents external code from creating multiple instances. A static method controls instance creation.

Example:
```java
class DatabaseConnection {
    private static DatabaseConnection instance;
    private String connectionString;
    
    // Private constructor - cannot create objects externally
    private DatabaseConnection() {
        connectionString = "jdbc:mysql://localhost:3306/mydb";
        System.out.println("Database connection established");
    }
    
    // Controlled access to single instance
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }
    
    public String getConnection() {
        return connectionString;
    }
}

// Usage
// DatabaseConnection db1 = new DatabaseConnection(); // ERROR: private
DatabaseConnection db1 = DatabaseConnection.getInstance();
DatabaseConnection db2 = DatabaseConnection.getInstance();
System.out.println(db1 == db2); // true - same instance
```

---

**20. Answer: B) Yes, and it's called when a subclass is instantiated**

**Explanation:**
Abstract classes can and should have constructors to initialize their own fields. These constructors are called when concrete subclass objects are created.

Example:
```java
abstract class Shape {
    String color;
    
    // Abstract class CAN have constructor
    Shape(String color) {
        this.color = color;
        System.out.println("Shape constructor: " + color);
    }
    
    abstract double getArea();
}

class Circle extends Shape {
    double radius;
    
    Circle(String color, double radius) {
        super(color); // Calls Shape constructor
        this.radius = radius;
        System.out.println("Circle constructor");
    }
    
    double getArea() {
        return Math.PI * radius * radius;
    }
}

// Usage
// Shape s = new Shape("Red"); // ERROR: Cannot instantiate abstract class
Circle c = new Circle("Blue", 5.0);
// Output:
// Shape constructor: Blue
// Circle constructor
```

---

## Section 2: Output-Based Questions - Solutions

### Beginner Level

**21. Output:**
```
Constructor called
```

**Explanation:**
When `new Test()` is executed, the constructor is automatically called, printing "Constructor called".

---

**22. Output:**
```
10
```

**Explanation:**
The parameterized constructor sets `width = 10`, which is then printed.

---

**23. Output:**
```
A
B
```

**Explanation:**
First, `new Demo()` calls the no-arg constructor (prints "A"). Then, `new Demo(5)` calls the parameterized constructor (prints "B").

---

**24. Output:**
```
0
```

**Explanation:**
The default constructor initializes the int variable `x` to its default value of 0.

---

### Intermediate Level

**25. Output:**
```
Parent Constructor
Child Constructor
```

**Explanation:**
When creating a Child object, the Parent constructor is automatically called first (implicit `super()`), then the Child constructor.

Complete example:
```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        // super() is implicitly called here first
        System.out.println("Child Constructor");
    }
    
    public static void main(String[] args) {
        Child c = new Child();
    }
}
```

---

**26. Output:**
```
Parameterized constructor: 10
No-arg constructor
```

**Explanation:**
The no-arg constructor calls `this(10)` first, which executes the parameterized constructor. Then control returns to complete the no-arg constructor.

Complete example:
```java
class Test {
    Test() {
        this(10); // Must be first statement
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

---

**27. Output:**
```
Static block
Instance block
Constructor
```

**Explanation:**
Execution order:
1. Static block - executed once when class is loaded
2. Instance block - executed before constructor for each object
3. Constructor - executed for each object

Complete example:
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

// If we create two objects:
Demo d1 = new Demo();
Demo d2 = new Demo();
// Output:
// Static block (only once)
// Instance block
// Constructor
// Instance block
// Constructor
```

---

### Advanced Level

**28. Output:**
```
Parent: 20
Child
```

**Explanation:**
The Child constructor explicitly calls `super(20)`, which executes the Parent constructor with parameter 20, then the Child constructor continues.

Complete example:
```java
class Parent {
    Parent(int x) {
        System.out.println("Parent: " + x);
    }
}

class Child extends Parent {
    Child() {
        super(20); // Explicit call to Parent constructor
        System.out.println("Child");
    }
    
    public static void main(String[] args) {
        Child c = new Child();
    }
}
```

---

**29. Output:**
```
0
```

**Explanation:**
This is a common mistake! The parameter `x` shadows the instance variable `x`. The statement `x = x` assigns the parameter to itself, not to the instance variable. The instance variable remains 0.

**Fix:**
```java
class Test {
    int x;
    
    Test(int x) {
        this.x = x; // Use 'this' to refer to instance variable
    }
    
    public static void main(String[] args) {
        Test t = new Test(10);
        System.out.println(t.x); // Now prints 10
    }
}
```

---

**30. Output/Error:**
```
Compilation Error: call to super must be first statement in constructor
```

**Explanation:**
You cannot use both `this()` and `super()` in the same constructor, and whichever you use must be the first statement. Here, `super()` comes after `this()`, causing a compilation error.

**Fix Option 1 - Use only this():**
```java
class Demo {
    Demo() {
        this(5);
        System.out.println("Constructor");
    }
    
    Demo(int x) {
        // super() is implicitly called here
        System.out.println("Param: " + x);
    }
}
```

**Fix Option 2 - Use only super():**
```java
class Demo {
    Demo() {
        super(); // Or just remove it (implicit)
        System.out.println("Constructor");
    }
}
```

---

## Section 3: Tricky Coding Questions - Solutions

### Intermediate Level

**31. Solution: Singleton Class with Private Constructor**

```java
class Database {
    // Static variable to hold single instance
    private static Database instance;
    private String connectionString;
    
    // Private constructor prevents external instantiation
    private Database() {
        connectionString = "Connected to database";
        System.out.println("Database instance created");
    }
    
    // Public method to get the single instance
    public static Database getInstance() {
        if (instance == null) {
            instance = new Database();
        }
        return instance;
    }
    
    // Method to connect
    public void connect() {
        System.out.println("Connected to database");
    }
    
    // Main method to test
    public static void main(String[] args) {
        // Database db1 = new Database(); // ERROR: Constructor is private
        
        Database db1 = Database.getInstance();
        Database db2 = Database.getInstance();
        
        System.out.println("db1 == db2: " + (db1 == db2)); // true
        
        db1.connect();
    }
}
```

**Output:**
```
Database instance created
db1 == db2: true
Connected to database
```

**Explanation:**
- Private constructor ensures no one can create objects using `new`
- Static `getInstance()` method controls object creation
- Only one instance exists throughout the application
- All references point to the same object

---

**32. Solution: Constructor Chaining**

```java
class Student {
    private String name;
    private int age;
    private int rollNumber;
    
    // Constructor 1: Only name
    Student(String name) {
        this(name, 18); // Chain to constructor 2
        System.out.println("Constructor 1 called");
    }
    
    // Constructor 2: Name and age
    Student(String name, int age) {
        this(name, age, 0); // Chain to constructor 3
        System.out.println("Constructor 2 called");
    }
    
    // Constructor 3: All parameters
    Student(String name, int age, int rollNumber) {
        this.name = name;
        this.age = age;
        this.rollNumber = rollNumber;
        System.out.println("Constructor 3 called");
    }
    
    // Display method
    public void display() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Roll Number: " + rollNumber);
        System.out.println();
    }
    
    public static void main(String[] args) {
        System.out.println("Creating Student 1:");
        Student s1 = new Student("Alice");
        s1.display();
        
        System.out.println("Creating Student 2:");
        Student s2 = new Student("Bob", 20);
        s2.display();
        
        System.out.println("Creating Student 3:");
        Student s3 = new Student("Charlie", 22, 101);
        s3.display();
    }
}
```

**Output:**
```
Creating Student 1:
Constructor 3 called
Constructor 2 called
Constructor 1 called
Name: Alice
Age: 18
Roll Number: 0

Creating Student 2:
Constructor 3 called
Constructor 2 called
Name: Bob
Age: 20
Roll Number: 0

Creating Student 3:
Constructor 3 called
Name: Charlie
Age: 22
Roll Number: 101
```

**Explanation:**
- Constructor chaining using `this()` avoids code duplication
- Each constructor calls the next one with default values
- The most specific constructor (3) does the actual initialization
- Execution order: Most specific constructor executes first, then backs out

---

### Advanced Level

**33. Solution: Copy Constructor Challenge**

```java
class Employee {
    private int id;
    private String name;
    private double salary;
    
    // Parameterized constructor
    public Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }
    
    // Copy constructor - creates deep copy
    public Employee(Employee emp) {
        this.id = emp.id;
        this.name = emp.name; // String is immutable, so this is safe
        this.salary = emp.salary;
    }
    
    // Setters
    public void setId(int id) {
        this.id = id;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public void setSalary(double salary) {
        this.salary = salary;
    }
    
    // Override toString
    @Override
    public String toString() {
        return "Employee[ID=" + id + ", Name=" + name + ", Salary=$" + salary + "]";
    }
    
    public static void main(String[] args) {
        // Create original employee
        Employee emp1 = new Employee(101, "John Doe", 50000);
        System.out.println("Original: " + emp1);
        
        // Create copy using copy constructor
        Employee emp2 = new Employee(emp1);
        System.out.println("Copy: " + emp2);
        
        // Modify the copy
        emp2.setId(102);
        emp2.setName("Jane Smith");
        emp2.setSalary(60000);
        
        System.out.println("\nAfter modifying copy:");
        System.out.println("Original: " + emp1); // Unchanged
        System.out.println("Copy: " + emp2);     // Changed
    }
}
```

**Output:**
```
Original: Employee[ID=101, Name=John Doe, Salary=$50000.0]
Copy: Employee[ID=101, Name=John Doe, Salary=$50000.0]

After modifying copy:
Original: Employee[ID=101, Name=John Doe, Salary=$50000.0]
Copy: Employee[ID=102, Name=Jane Smith, Salary=$60000.0]
```

**Explanation:**
- Copy constructor creates a new independent object
- Modifying the copy doesn't affect the original
- For objects with reference-type fields (like arrays or other objects), you need deep copy
- Strings are immutable, so copying reference is safe

---

**34. Solution: Constructor Exception Handling**

```java
// Custom exception class
class InvalidAccountException extends Exception {
    public InvalidAccountException(String message) {
        super(message);
    }
}

class BankAccount {
    private String accountNumber;
    private double balance;
    
    // Constructor with validation
    public BankAccount(String accountNumber, double balance) throws InvalidAccountException {
        // Validate account number
        if (accountNumber == null || accountNumber.trim().isEmpty()) {
            throw new InvalidAccountException("Account number cannot be null or empty");
        }
        
        // Validate balance
        if (balance < 0) {
            throw new InvalidAccountException("Balance cannot be negative: " + balance);
        }
        
        this.accountNumber = accountNumber;
        this.balance = balance;
        System.out.println("Account created successfully: " + accountNumber);
    }
    
    // Deposit method
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount + ", New Balance: $" + balance);
        }
    }
    
    // Check balance
    public double getBalance() {
        return balance;
    }
    
    @Override
    public String toString() {
        return "Account[" + accountNumber + ", Balance=$" + balance + "]";
    }
    
    public static void main(String[] args) {
        // Test Case 1: Valid account
        try {
            BankAccount acc1 = new BankAccount("ACC001", 1000);
            System.out.println(acc1);
            acc1.deposit(500);
            System.out.println();
        } catch (InvalidAccountException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Test Case 2: Null account number
        try {
            BankAccount acc2 = new BankAccount(null, 1000);
        } catch (InvalidAccountException e) {
            System.out.println("Error: " + e.getMessage());
            System.out.println();
        }
        
        // Test Case 3: Empty account number
        try {
            BankAccount acc3 = new BankAccount("", 1000);
        } catch (InvalidAccountException e) {
            System.out.println("Error: " + e.getMessage());
            System.out.println();
        }
        
        // Test Case 4: Negative balance
        try {
            BankAccount acc4 = new BankAccount("ACC004", -500);
        } catch (InvalidAccountException e) {
            System.out.println("Error: " + e.getMessage());
            System.out.println();
        }
    }
}
```

**Output:**
```
Account created successfully: ACC001
Account[ACC001, Balance=$1000.0]
Deposited: $500.0, New Balance: $1500.0

Error: Account number cannot be null or empty

Error: Account number cannot be null or empty

Error: Balance cannot be negative: -500.0
```

**Explanation:**
- Custom exception `InvalidAccountException` for specific error handling
- Constructor validates parameters and throws exception if invalid
- Object is NOT created if constructor throws exception
- Caller must handle the exception using try-catch
- This ensures only valid objects are created

---

**35. Solution: Static vs Instance Initialization**

```java
class Counter {
    // Static variable - shared across all objects
    private static int totalObjects = 0;
    
    // Instance variable - unique to each object
    private int objectId;
    
    // Static initialization block - runs once when class is loaded
    static {
        System.out.println("=== Static block executed (runs once) ===");
        System.out.println("Class Counter is being loaded...\n");
    }
    
    // Instance initialization block - runs before each constructor
    {
        totalObjects++;
        objectId = totalObjects;
        System.out.println("Instance block executed for object #" + objectId);
    }
    
    // Constructor
    public Counter() {
        System.out.println("Constructor executed for object #" + objectId);
        System.out.println();
    }
    
    // Method to display object info
    public void display() {
        System.out.println("Object ID: " + objectId);
        System.out.println("Total Objects Created: " + totalObjects);
        System.out.println();
    }
    
    // Static method to get total count
    public static int getTotalObjects() {
        return totalObjects;
    }
    
    public static void main(String[] args) {
        System.out.println("Main method started\n");
        
        System.out.println("--- Creating Object 1 ---");
        Counter c1 = new Counter();
        c1.display();
        
        System.out.println("--- Creating Object 2 ---");
        Counter c2 = new Counter();
        c2.display();
        
        System.out.println("--- Creating Object 3 ---");
        Counter c3 = new Counter();
        c3.display();
        
        System.out.println("=== Summary ===");
        System.out.println("Total objects created: " + Counter.getTotalObjects());
        
        System.out.println("\nIndividual Object IDs:");
        c1.display();
        c2.display();
        c3.display();
    }
}
```

**Output:**
```
=== Static block executed (runs once) ===
Class Counter is being loaded...

Main method started

--- Creating Object 1 ---
Instance block executed for object #1
Constructor executed for object #1

Object ID: 1
Total Objects Created: 1

--- Creating Object 2 ---
Instance block executed for object #2
Constructor executed for object #2

Object ID: 2
Total Objects Created: 2

--- Creating Object 3 ---
Instance block executed for object #3
Constructor executed for object #3

Object ID: 3
Total Objects Created: 3

=== Summary ===
Total objects created: 3

Individual Object IDs:
Object ID: 1
Total Objects Created: 3

Object ID: 2
Total Objects Created: 3

Object ID: 3
Total Objects Created: 3
```

**Execution Order Explanation:**

1. **Static Block** - Executes ONCE when class is first loaded (before any object creation or main method)
2. **Instance Block** - Executes BEFORE each constructor, every time an object is created
3. **Constructor** - Executes after instance block for each object

**Complete Order for Each Object:**
```
Class Loading (once):
  ↓
Static Variables Initialization
  ↓
Static Block
  ↓
Main Method Starts
  ↓
For Each Object:
  ↓
  Instance Variables Initialization
  ↓
  Instance Block
  ↓
  Constructor
```

**Key Points:**
- Static members belong to the class, not objects
- `totalObjects` is shared across all instances
- Each object has its own `objectId`
- Static block runs only once, instance block runs for each object
- This pattern is useful for counting objects, assigning unique IDs, etc.

---

## Summary of Key Concepts

### Constructor Basics
1. Same name as class, no return type
2. Called automatically when object is created
3. Used for initialization
4. Can be overloaded

### Constructor Chaining
- Use `this()` to call another constructor in the same class
- Use `super()` to call parent class constructor
- Must be the first statement
- Cannot use both in same constructor

### Initialization Order
1. Static variables and blocks (once)
2. Instance variables and blocks (per object)
3. Constructor (per object)

### Inheritance
- Parent constructor called before child
- Use `super()` explicitly or it's called implicitly
- Cannot call constructors after object creation

### Best Practices
- Use constructor chaining to avoid duplication
- Validate parameters in constructors
- Throw exceptions for invalid state
- Use `this.` to distinguish parameters from instance variables
- Consider private constructors for Singleton pattern
- Be careful calling overridable methods from constructors

---

**End of Solutions**

