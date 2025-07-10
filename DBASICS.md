## Dlang Fundamentals: Basic Logic & Modularity

Dlang is a powerful and flexible language. For us "tech artisans," understanding its fundamental logic and how it supports modularity is key to writing clean, efficient, and maintainable code.

### 1\. Basic Logic in Dlang

Dlang provides all the essential logical constructs you need. Here are the most basic ones:

#### a. Variables and Data Types

Dlang is **statically typed**, so you declare the data type of a variable. However, it also supports **type inference** using `auto` for quicker coding.

```d
import std.stdio;

void main() {
    int number = 10;
    string name = "Arctian";
    bool isActive = true;

    auto price = 15000;
    auto message = "Welcome!";
    auto pi = 3.14;

    writeln("Number: ", number);
    writeln("Name: ", name);
    writeln("Is Active: ", isActive);
    writeln("Price: ", price);
    writeln("Message: ", message);
    writeln("Pi: ", pi);
}
```

#### b. Operators

Dlang operators are similar to C/C++ or Java. You have arithmetic, comparison, logical, and other operators.

```d
import std.stdio;

void main() {
    int a = 10;
    int b = 5;

    writeln("a + b = ", a + b);
    writeln("a - b = ", a - b);
    writeln("a * b = ", a * b);
    writeln("a / b = ", a / b);
    writeln("a % b = ", a % b);

    writeln("a > b: ", a > b);
    writeln("a == b: ", a == b);

    bool x = true;
    bool y = false;
    writeln("x && y: ", x && y);
    writeln("x || y: ", x || y);
    writeln("!x: ", !x);
}
```

#### c. Control Structures (Conditionals)

To make your program make decisions, Dlang uses `if-else` and `switch`.

**`if-else`:**

```d
import std.stdio;

void main() {
    int score = 75;

    if (score >= 90) {
        writeln("Grade A");
    } else if (score >= 80) {
        writeln("Grade B");
    } else if (score >= 70) {
        writeln("Grade C");
    } else {
        writeln("Fail");
    }
}
```

**`switch`:**

```d
import std.stdio;

void main() {
    string day = "Monday";

    switch (day) {
        case "Monday":
            writeln("First workday!");
            break;
        case "Friday":
            writeln("Almost weekend!");
            break;
        default:
            writeln("Regular day.");
    }
}
```

**Important:** In Dlang, `switch` statements have "fall-through" behavior by default unless you use `break`, `return`, `goto`, or `throw`.

#### d. Control Structures (Loops)

To repeat actions, Dlang has `for` and `while`/`do-while` loops.

**`for` loop:**

```d
import std.stdio;

void main() {
    for (int i = 0; i < 5; i++) {
        writeln("Iteration: ", i);
    }
}
```

**`while` loop:**

```d
import std.stdio;

void main() {
    int count = 0;
    while (count < 3) {
        writeln("Count: ", count);
        count++;
    }
}
```

**`do-while` loop:**

```d
import std.stdio;

void main() {
    int i = 0;
    do {
        writeln("This will run at least once: ", i);
        i++;
    } while (i < 0);
}
```

-----

### 2\. Modularity in Dlang

Modular code is crucial for scalable and manageable projects. Dlang supports modularity through **modules** and **packages**.

#### a. What is a Module?

In Dlang, every source file (`.d`) is a **module**. The module's name typically matches the filename (without the extension). A module acts as a container for related functions, variables, classes, or structs.

#### b. Using Modules (Import)

To use code from another module, you use the `import` keyword.

Let's say you have two files:

**`math_operations.d`:**

```d
module math_operations;

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}
```

**`main_app.d`:**

```d
import std.stdio;
import math_operations;

void main() {
    int sum = math_operations.add(10, 5);
    int difference = math_operations.subtract(10, 5);

    writeln("Sum: ", sum);
    writeln("Difference: ", difference);
}
```

To compile and run `main_app.d`, ensure both files are in the same directory, then:

```bash
dmd main_app.d math_operations.d
./main_app
```

#### c. Module Declaration (`module` keyword)

Every `.d` file *should* have a `module` declaration on the first line. While optional for `main` modules or those not part of a package, it's highly recommended for consistency and clarity, especially as your projects grow.

```d
module my_module;

// ... your code here ...
```

#### d. Packages

Packages in Dlang are a way to organize related modules into a hierarchical directory structure, similar to namespaces in other languages. Package names correspond to directory names.

Example directory structure:

```
my_project/
├── dub.json
└── source/
    ├── app.d
    └── helpers/
        └── string_utils.d
        └── numeric_utils.d
```

**`source/helpers/string_utils.d`:**

```d
module helpers.string_utils;

string capitalize(string text) {
    if (text.length == 0) return "";
    return text[0].toUpper ~ text[1..$];
}
```

**`source/helpers/numeric_utils.d`:**

```d
module helpers.numeric_utils;

int square(int number) {
    return number * number;
}
```

**`source/app.d`:**

```d
import std.stdio;
import helpers.string_utils;
import helpers.numeric_utils;

void main() {
    string greeting = helpers.string_utils.capitalize("hello world");
    int squaredResult = helpers.numeric_utils.square(7);

    writeln("Greeting: ", greeting);
    writeln("Squared 7: ", squaredResult);
}
```

When importing, you can use `import helpers.string_utils;` to import the entire module. If you only want to import specific functions and use them directly without the full module prefix, you can do `import helpers.string_utils : capitalize;`.

-----

### 3\. Functions in Dlang

**Functions** are like "building blocks" in our code, grouping instructions to perform specific tasks. With functions, code becomes more organized, reusable, and easier to maintain.

#### a. Basic Function Declaration

Dlang has clear syntax for function declarations, similar to other languages like C/C++ or Java. You need to specify the return type (if any), the function name, and parameters (if any).

```d
import std.stdio;

void sayHello() {
    writeln("Hello, tech artisan!");
}

void greetUser(string name) {
    writeln("Hi, ", name, "! Welcome to the world of Dlang.");
}

int addNumbers(int a, int b) {
    return a + b;
}

auto getMinMax(int[] numbers) {
    if (numbers.length == 0) {
        return tuple(int.min, int.max);
    }
    int minVal = numbers[0];
    int maxVal = numbers[0];
    foreach (num; numbers) {
        if (num < minVal) {
            minVal = num;
        }
        if (num > maxVal) {
            maxVal = num;
        }
    }
    return tuple(minVal, maxVal);
}

void main() {
    sayHello();
    greetUser("Arctian");

    int result = addNumbers(20, 15);
    writeln("Addition result: ", result);

    int[] data = [5, 1, 9, 3, 7];
    auto minMax = getMinMax(data);
    writeln("Minimum value: ", minMax[0]);
    writeln("Maximum value: ", minMax[1]);
}
```

#### b. Function Overloading

Dlang allows you to have multiple functions with the same name but different signatures (parameter types and count). This is called **Function Overloading**.

```d
import std.stdio;

int sum(int a, int b) {
    return a + b;
}

int sum(int a, int b, int c) {
    return a + b + c;
}

string sum(string s1, string s2) {
    return s1 ~ s2;
}

void main() {
    writeln("Sum int (2 params): ", sum(5, 3));
    writeln("Sum int (3 params): ", sum(1, 2, 3));
    writeln("Sum string: ", sum("Hello, ", "Dlang!"));
}
```

-----

### 4\. Object-Oriented Programming (OOP) in Dlang

As programmers familiar with various environments, you're definitely acquainted with **OOP** concepts. Dlang fully supports the OOP paradigm with **classes**, **objects**, **inheritance**, **polymorphism**, and **encapsulation**. This is crucial for building complex yet structured applications.

#### a. Classes and Objects

  * A **Class** is a blueprint for objects. It defines properties (data, called **fields** or **members**) and behaviors (functions, called **methods**).
  * An **Object** is an instance of a class.

<!-- end list -->

```d
import std.stdio;

class Car {
    string brand;
    string model;
    int year;

    this(string brand, string model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        writeln("A ", brand, " ", model, " car is created.");
    }

    void displayInfo() {
        writeln("Brand: ", brand);
        writeln("Model: ", model);
        writeln("Year: ", year);
    }

    void startEngine() {
        writeln("The ", brand, " ", model, " engine starts. Vroom!");
    }
}

void main() {
    Car myCar = new Car("Toyota", "Camry", 2022);
    Car anotherCar = new Car("Honda", "Civic", 2023);

    writeln("\n--- First Car Info ---");
    myCar.displayInfo();
    myCar.startEngine();

    writeln("\n--- Second Car Info ---");
    anotherCar.displayInfo();
}
```

#### b. Inheritance

**Inheritance** is a concept where one class can inherit properties and methods from another class. The inheriting class is called a **derived class** or **subclass**, and the class being inherited from is called a **base class** or **superclass**. This promotes *code reusability*.

```d
import std.stdio;

class Vehicle {
    string type;

    this(string type) {
        this.type = type;
        writeln("A ", type, " is created.");
    }

    void honk() {
        writeln("Beep beep!");
    }
}

class Bicycle : Vehicle {
    int numGears;

    this(string type, int numGears) {
        super(type);
        this.numGears = numGears;
        writeln("A bicycle with ", numGears, " gears is created.");
    }

    void ringBell() {
        writeln("Kling kling!");
    }

    override void honk() {
        writeln("Bicycles don't honk, they ring!");
    }
}

void main() {
    Vehicle generalVehicle = new Vehicle("General Vehicle");
    generalVehicle.honk();

    writeln("\n--- Bicycle Info ---");
    Bicycle myBicycle = new Bicycle("Mountain Bike", 21);
    myBicycle.ringBell();
    myBicycle.honk();
    writeln("Bicycle vehicle type: ", myBicycle.type);
}
```

#### c. Polymorphism

**Polymorphism** means "many forms." In OOP, it allows objects of different classes to be treated as objects of a common base class, as long as they share a common interface. This is often achieved through *method overriding* and *abstract classes* or *interfaces*.

```d
import std.stdio;

abstract class Shape {
    abstract double getArea();

    void describe() {
        writeln("This is a geometric shape.");
    }
}

class Circle : Shape {
    double radius;
    this(double radius) {
        this.radius = radius;
    }
    override double getArea() {
        return 3.14159 * radius * radius;
    }
}

class Rectangle : Shape {
    double width;
    double height;
    this(double width, double height) {
        this.width = width;
        this.height = height;
    }
    override double getArea() {
        return width * height;
    }
}

void main() {
    Shape myCircle = new Circle(5.0);
    Shape myRectangle = new Rectangle(4.0, 6.0);

    writeln("Circle Area: ", myCircle.getArea());
    writeln("Rectangle Area: ", myRectangle.getArea());
    
    myCircle.describe();
    myRectangle.describe();
}
```

-----

