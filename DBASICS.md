
-----

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

Using DUB (Dlang Universal Build system) is generally easier for projects:

```bash
mkdir my_modular_project
cd my_modular_project
dub init
# (Then edit source/app.d and create source/math_operations.d)
dub run
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

