# Day 2 (25 minutes)
- First Rust Program:
```Rust
fn main(){
    println!("STring!!");
}
```
- The main function in rust is always the one that runs first on an executable.
- fn denotes start of a function.
- Rust style is to indent with 4 spaces not tab.
- the statement inside of the function "println!" calls a Rust macro not a fucntion. Macros still need to be discussed and will be discussed later down. For now, anytime adding ! along a statement or function such as println would mean a Rust macro is being called not function.
- After compiling a source code in this case main.rs using ``` rustc main.rs``` would create a binary executable like C or C++ does.
- Rust is an ahead of time compiled language. This means after compiling the source code and generating the executable, you can send the executable to someone else they would b able to run it without even having rust installed.
- Cargo is Rust's build system and package manager. Cargo does a lot of jobs for devs, such as building your code, downloading dependencies, adding libraries and building those libraries.
- Cargo upon execution creates an entire file structure that typically would have everything needed for traditional projects such as .git, src dir, .gitignore file, and a Cargo.toml file.
```shell
cargo new hello_cargo
# This cmd creates a new project dir named hello_cargo.
ls -la ../hello_cargo/
drwxr-xr-x  - playaow 25 Mar 18:42  .
drwxr-xr-x  - playaow 25 Mar 18:42  ..
drwxr-xr-x  - playaow 25 Mar 18:42  .git
drwxr-xr-x  - playaow 25 Mar 18:42 󰣞 src
.rw-r--r--  8 playaow 25 Mar 18:42 󰊢 .gitignore
.rw-r--r-- 82 playaow 25 Mar 18:42  Cargo.toml
```
- This command creates a parent dir and two child dir named .git and src. The Dir src would have the main.rs file.
- This is what the project called hello_cargo conf looks like written in TOML:
```TOML
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["YourName <yourname@example.com"]

[dependencies]
```
- TOMS (Tom's Obvious Minimal Language)
- The first line [package], is a section heading that indicates the following statements are configuring a package. 
- Within the [dependencies], under that you should list out the dependencies required for your project. In Rust, packages of code are referred to as crates. For a simple propject like this we do not need any dependencies. 
- Upon creating a Cargo project, cargo expects you to put all of your source codes inside of the src dir, the root level dir is used for README, configurations and license.
- In order to build project using cargo, go inside of the root dir of your cargo project and execute ```shell cargo build``` on the terminal.
```shell
cargo build
Compiling hello_cargo v0.1.0 (/home/playaow/Documents/Rust/hello_cargo)
Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.15s

```
- Running this command creates another dir dedicated for executables, it creates a dir called target/debug, and inside of target your should see the binary exe.
```shell
ls -la ./target/debug/
drwxr-xr-x    - playaow 25 Mar 18:55  .
drwxr-xr-x    - playaow 25 Mar 18:55  ..
drwxr-xr-x    - playaow 25 Mar 18:55  .fingerprint
drwxr-xr-x    - playaow 25 Mar 18:55 󱧼 build
drwxr-xr-x    - playaow 25 Mar 18:55  deps
drwxr-xr-x    - playaow 25 Mar 18:55  examples
drwxr-xr-x    - playaow 25 Mar 18:55  incremental
.rw-r--r--    0 playaow 25 Mar 18:55  .cargo-lock
.rwxr-xr-x 4.0M playaow 25 Mar 18:55 󰡯 hello_cargo
.rw-r--r--  120 playaow 25 Mar 18:55  hello_cargo.d
```
- This command "cargo build" also creates another file called Cargo.lock on the root level of the project.
- To directly build and run the project command "cargo run" can be used. This compiles and executes the resulting binary exe for us.
- Before building the project, you can also execute command "cargo check" to check whether your code has any error before even compiles making sure it compiles but does not produce an executables.
- The command "cargo build --release" is used when you are completety done with your project and testing are done and ready for release. Using this command would create an executable inside of test/release instead of test/debug. This also compiles the code with optimization. This helps to run your rust code fast. 

- Guessing game src code.
```rust
use std::io

fn main(){
    println!("Guess the number!");
    println!("Please input your guess: ");
    let mut guess = String::new();

    io::stdin().read_line(&mut guess)
        .expect("Failed to read line");
    println!("You guessed: {}", guess);
```
- In order to obtain user input and output that input provided we have to include input/output library within the src code. Hence using ```use std::io``` is declared at the top of the program. This means let the script use functions and variables found within the io lib.
- By default Rust does not bring all types of functions into the scope of the program and only bring most common and most used types into scope which is set by prelude. Reason why we had to manually bring ```std::io``` into the program. ```std::io``` is not part of the Rust prelude.
- In Rust, let statement is used to set a variable. Such as ```let bar=foo;```
- By defualt in Rust, variable declared using let such as ```let x = 5; ``` are immutable. Meaning these variables cannot be changed unless you explicitly allow it. 
```rs
fn main(){
    let x = 5;
    x = 10; //This will throw an error
    // Because of immutability of Rust
}
```
- Now in order to make a variable mutable, we would have to use the keyword ```mut``` along with ```let``` such as ```let mut x = 5;```
```rs
fn main(){
    let mut x = 5;
    x = 10; //This is ok!
    //since mut was included meaning
    // This varibale is mutable.
}
```
- ```String::new();``` calls the associated function new defined for the String type. The :: operator is used to access functions or items that belong to a type or module. Because new is an associated function, it does not require an existing String instance. This is similar to a static method in other programming languages.
- Associated function are functions that belongs to a class or type that does not require an existing instance. Typically to access associated function of a type we use :: path seprator. In this case new() is an associated function of type String.
- Bottomline, the statement ```let mut guess = String::new();``` essentially assigns a new String instance to the mutable variable named guess.
```rs
io::stdin().read_line(&mut guess)
    .expect("Failed to read line!!");
```
- In this code snippet, we are calling function stdin() from the module io. The ```.read_line(&mut guess)``` calls the read_line method on the standard input handle to get input from the user.
- The job of read_line is to take whatever the user types into the stdin (such as keyboard) and place that into a string, so it takes that string as an arg. Reason why the variable guess had to be mutable so that it can take user input and feed it into the variable without having the compiler complain about it.
- The & just like C, means reference. Adding ```&mut guess``` means we are pushing a ref as an argument to the function read_line. Reference lets user use data in multiple parts of their program without having to copy the data into memory everytime the data is called for work. This reduces the load on memory and optimizes performace for the program.
- Just like variables in rust references are immutable by default as well. Reason why we had to add mut after & sign. Making the reference mutable as well.
- A crate is a collection of Rust source code files.
- The rand crate is a library crate which contains code that is intended for other to be used.
- In the dependencies section of Cargo.toml, you provide information such as name and version number of rust external crates your source code depends on. In order to create a random number guessing game you would need the rand library crate which can be added in the dependencies section in this manner:
```toml
[dependencies]

crate_name = "version_number"
rand = "0.3.14"
```
- in cargo.toml, a section header is denoted using [], everything that follows that section header is considered part of that header until it comes across another header which would mean that is the end of the current header section. such as:
```toml
[package]
name = "guessing game"
version = "0.0.32"
edition = "2024"

[dependencies]

rand = "0.3.14"

# Here name, version, and edition are part of section header package and rand is part of seciton header dependencies.
```
- When you run "cargo build" you may also see other library carts being downloaded or added to your project. That is not necessarily a problem, because some dependencies may require other dependent library crates to be able to function properly. Such as in this case:
```shell
cargo build
Updating crates.io index
Locking 10 packages to latest Rust 1.94.0 compatible versions
Adding fuchsia-cprng v0.1.1
Adding libc v0.2.184
Adding rand v0.3.23 (available: v0.10.0)
Adding rand v0.4.6
Adding rand_core v0.3.1
Adding rand_core v0.4.2
Adding rdrand v0.4.0
Adding winapi v0.3.9
Adding winapi-i686-pc-windows-gnu v0.4.0
Adding winapi-x86_64-pc-windows-gnu v0.4.0
Downloaded rand v0.3.23
Downloaded rand v0.4.6
Downloaded 2 crates (85.7KiB) in 0.12s
Compiling libc v0.2.184
Compiling rand v0.4.6
Compiling rand v0.3.23
Compiling guessing_game v0.1.0 (/home/playaow/Documents/Rust/guessing_game)
Finished `dev` profile [unoptimized + debuginfo] target(s) in 1.56s
# We see lib crate like libc also being called because rand depends on libc. So Cargo
# automatically adds dependent library for crates that are dependencies of your project
```
- The Cargo.lock file allows user to manually upgrade or not upgrade their dependencies.
- Now if user do want to upgrade to a newer crate version, they can do so using cargo update which ignores versions indicated in cargo.lock file and figures out the newest version of crate that works with your project and downloads them. Then Cargo also updates the Cargo.lock file.
- Also cargo update will only update versions from 0.x.x to 0.x+0.99.x. Lets say if your current rand crate is 0.3.x, it will update it till 0.3.99 but not 0.4.0 if one is available. To be able to upgrade to a 0.4.0 version you would have to change the cargo.toml file.
- Adding these two lines of rand source code to the guessing game:
```rs
use rand::Rng
let secret_number = rand::thread_rng().gen_range(1,101);
println!("The secret number is: {}", secret_number)
```
- use rand::Rng, the Rng trait defines methods that random number generators implement.
- The rand::thread_rng gives us a random number generator that is local to the current thread of execution and seeded by the os. Running thread_rng allows one thread to generate random number for the proram instead of multiple thread trying to generate numbers. Since we know a program can run on multiple therad. By using this thread_rng fn, we minimize the possibility of thread collision.
- The statement "Seeded by the operating system" A random number generator needs a starting value called a seed from which it starts to generate it sequence of random number. If the program always starts from the same seed, it will generate the same number always making it not random in this context. By using the OS as seed source, the OS provides something truly unpredictable (like hardware timing or system noise) so the numbers are genuinely hard to predict.
-

