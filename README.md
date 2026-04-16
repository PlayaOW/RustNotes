## Chapter 2
- Unless specified rust defualts to i32 type number.
- Variable shadowing occurs in rust when you declare new variable with the same name of another variable declared prior. This allows devs to change the type of the variable to reuse the variable instead of creating another variable.
- The trim() method on a String instance will remove any white spaces at the beginning and the end. If we were to convert a string to integer, this is something that must be done. Or else how would the program interpret any white space within the string..
- in ```std::io::stdin().read_line(&var)``` upon coming to this of program user would be instructed to enter a value. The value will only be passed to the progra after the user presses enter upon entering the value. That is how the method read_line() works. This pressing of enter adds a newline(\n) char at the end of the string typed. So in the case of trim() method, this also eliminates the newline characters at the end of the string.
- Thus when user enters the value 5, the read_line() store 5\n, but after using trim() method the value would be 5 no newline chars.
- the parse() method on rust converts a string to another type. Also in this case we have to explicitly tell rust what number type we wish this string to be converted to, which is u32. This is done in this part of the code ```let guess: u32```. This time guess does not have to be mutable since while the program is running we do not have to write to guess again. It has already been done.
- Also when we compare these two values, since guess is now u32, rust will assume correct should also be u32 in which case it is automatically set to u32 so that both the number can be compared against each other.
- **NOTE** The parse method can only work on characters that can logically be converted to number. Any emojis or special that cannot be translated to number would throw an error. And also parse method returns a result type. And for result type returns you would also have to include an expect(Statement) right alongside.
- The ```loop``` keyword creates an infinite loop.
- The ```break``` keyword is used to break from a loop. such as this:
```rs
    loop {
        println!("Please enter your guess: ");
        let mut guess = String::new();

        io::stdin().read_line(&mut guess).expect("Please enter a number!!");
        println!("Your Guess: {guess}");

        let guess: u32 = guess.trim().parse().expect("Please enter an integer!!");

        match guess.cmp(&correct){
            Ordering::Less => println!("Too low! Try again"),
            Ordering::Greater => println!("To big, Try again"),
            Ordering::Equal => {
                println!("Congrats you won!!");
                break;
            }
        }
```
- Often time with Result returned methods such as purse() or read-_line(), instead of using expect() to crash the program gracefully, we can instead go into using match statements to handle the errors. Such as:
```rs
let guess: u32 = guess.trim().parse(){
    Ok(num) => num,
    Err(_) => continue,
};
```
- As we know parse() returns a Result type, and Result is an enum that has variants of Ok and Err. The underscore in Err(_) is a catch-all, we are saying we will catch all type of error regardless of what it is.

## Chapter 3
- A variable is immutable when data added to that variable cannot be altered.
- By default, Rust variables are immutable. But variables can be made mutable by using the keyword ```mut``` in front of the variable name such as:
```rs
let mut result = 3;
result = 4
// ANd this shoudl be ok since result is mutable..
```
- Difference between let and const in rust is that, let creates a variable that is immutable by default. const defines a compile-time constants ( an alias for a value ) that must be explicitly typed (such that :u32 or :i64) and also cannot be changed.
- const requires type annotation where ```let``` lets the compiler infur the type of the variable automatically.
### Rust: `const` vs. `let`

| Feature | `let` (Variable) | `const` (Constant) |
| :--- | :--- | :--- |
| **Mutability** | Immutable by default; can be made mutable with `mut`. | **Always** immutable. `mut` is not allowed. |
| **Type Annotation** | Optional (usually inferred by the compiler). | **Required** (e.g., `const NAME: type = value;`). |
| **Evaluation** | **Run-time**: Calculated when the program runs. | **Compile-time**: Calculated when the code is built. |
| **Scope** | Local to the block/function where it is defined. | Can be defined in any scope, including **global**. |
| **Value Requirement** | Can hold results of any function or user input. | Must be a **constant expression** (predictable values). |
| **Memory** | Exists on the stack (or heap if specified). | Inlined directly into the binary wherever used. |

---

### 1. Defining `const`
Constants are for values that are fixed for the entire life of the program. They are useful for global configuration or magic numbers.

```rust
// Must have a type, usually written in SCREAMING_SNAKE_CASE
const MAX_POINTS: u32 = 100_000;
```
### What "Known at compile time means??"
- For a value to be used in ```const```, the compiler must be able to resolve its value before the program even runs.
- Analogy:

<ol>
<li> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Setting the price of the menu before the restaurant even opens.</li>
<li> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Cashing out a customer which depends on their purchase which may &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;increase or decrease.</li>
</ol> 
-  


