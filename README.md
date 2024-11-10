# CPP---Module---07
This module is designed to help you understand Templates in CPP.

***
# TEMPLATES
***

# Table of contents
- [PARAMETRIC MACROS IN C](#parametric-macros-in-c)
- [TEMPLATES IN C++](#templates-in-c++)
    - [Function Templates](#function-templates)
    - [Class Templates](#class-templates)
***
***

# PARAMETRIC MACROS IN C
To introduce templates in C++, let's start by considering a type of macro in C.

**Parametric macros** in C are a type of preprocessor macro that accept arguments, allowing them to act like functions but with the simplicity of macro substitution. They are defined using the **#define** directive and can take parameters to be replaced within the macro body when the macro is invoked.

## How Parametric Macros Work
A parametric macro is defined using the #define preprocessor directive, followed by the macro name and parameters in parentheses. When the macro is called, the preprocessor replaces it with the macro body, substituting the provided arguments.

```C
#define MACRO_NAME(param1, param2) (param1 + param2)
```

Example
```C
#define SQUARE(x) ((x) * (x))

int main() {
    int num = 5;
    int result = SQUARE(num);
    printf("The square of %d is %d\n", num, result);
    return 0;
}
```

## Key Characteristics
1. **Text Replacement**: The macro is expanded by simple text substitution. In the example above, SQUARE(num) is replaced by ((num) * (num)) before the code is compiled.

2. **No Type Safety**: Parametric macros do not perform type checking, unlike functions. This can sometimes lead to unexpected results if not used carefully.

3. **Evaluation Pitfalls**: Arguments passed to macros can be evaluated multiple times, which may lead to side effects if those arguments include expressions with side effects (e.g., SQUARE(i++)).

4. **Performance**: Macros can be faster than functions because they avoid the overhead of function calls, as they are expanded inline.

Example of Pitfall:
```C
#define DOUBLE(x) (x + x)

int main() {
    int i = 3;
    printf("Result: %d\n", DOUBLE(i++)); // Expanded to: (i++ + i++)
    return 0;
}
```
This can result in i being incremented twice within the macro expansion.

***

# TEMPLATES IN C++
Templates in C++ are powerful features that allow functions and classes to operate 
with generic types. This capability enables you to create flexible and reusable code. 
Here's a breakdown of how templates work and why they are useful:

### What Are Templates
Templates are blueprints or formulae for creating a family of classes or functions. 
They allow you to write a single function or class definition that can work with any data type
without rewriting the code for each type.

For example, a software company may need to sort() for different data types. 
Rather than writing and maintaining multiple codes, we can write one sort() and 
pass the datatype as a parameter. 

C++ adds two new keywords to support templates: **template** and **typename**. 
The second keyword can always be replaced by the keyword **class**.

### How Do Templates Work
Templates are expanded at compiler time. This is like macros. The difference is, 
that the compiler does type-checking before template expansion. The idea is simple, 
source code contains only function/class, but compiled code may contain multiple 
copies of the same function/class. 

## Function Templates
A **function template** enables the creation of functions that can work with any data type. 
The template is defined using the **template keyword**, followed by template parameters 
in angle brackets (< >).

### Syntax Example:
```C++
template <typename T>
T add(T a, T b) {
    return a + b;
}
```
- **typename T**: **T** is a placeholder for a data type, can be any identifier. The keyword **typename** can 
also be replaced by class in this context, as they mean the same in templates.

- This function can now be used for any data type that supports the + operator:

```C++
int main() {
    int x = add(5, 10);         // Works with int
    double y = add(3.5, 2.5);   // Works with double
    return 0;
}
```

## Class Templates
A class template allows you to create classes that work with different data types using a single definition.

### Syntax Example:
```C++
template <typename T>
class Box {
private:
    T _value;
public:
    Box(T value) : _value(value) {}
    T getValue() const { return _value; }
};
```

- When you instantiate a Box object, you specify the type
   ```C++
   int main() {
    Box<int> intBox(123);       // Box with int type
    Box<std::string> strBox("Hello"); // Box with std::string type
    
    std::cout << intBox.getValue() << std::endl;
    std::cout << strBox.getValue() << std::endl;
    return 0;
    }
   ```
    - Box<int>: Creates a Box object where T is int.
    - Box<std::string>: Creates a Box object where T is std::string.