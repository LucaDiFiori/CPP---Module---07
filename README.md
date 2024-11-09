# CPP---Module---07
This module is designed to help you understand Templates in CPP.

***
# TEMPLATES
***

# Table of contents
- [PARAMETRIC MACROS IN C](#parametric-macros-in-c)

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