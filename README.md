
**Creating a Project with Cargo**

     $ cargo new hello_cargo --bin // ‘--lib’ for library


> **NOTE** : You can change cargo new to use a different version control system or no version control system by using the `--vcs` flag.

**TOML** (Tom’s Obvious, Minimal Language) format, which is Cargo’s configuration format.


**Cargo.lock.** This file keeps track of the exact versions of dependencies in your project.

  

Cargo also provides a command called `cargo check`. This command quickly checks your code to make sure it compiles but doesn’t produce an executable

**Building for Release**

When your project is finally ready for release, you can use `cargo build --release` to compile it with optimizations. This command will create an executable in *target/release* instead of *target/debug*. The optimizations make your Rust code run faster, but turning them on lengthens the time it takes for your program to compile. 

This is why there are two different profiles: one for development, when you want to rebuild quickly and often, and another for building the final program you’ll give to a user that won’t be rebuilt repeatedly and that will run as fast as possible. If you’re bench-marking your code’s running time, be sure to run `cargo build –release` and benchmark with the executable in *target/release.*
  
    _let mut guess = String::new();

The **`::`** syntax in the `::new` line indicates that new is an *associated function* of the String type. An associated function is implemented on a type, in this case String, rather than on a particular instance of a String. Some languages call this a **static method.**
> The **//** syntax starts a comment that continues until the end of the line.

**Updating a Crate to Get a New Version**

When you do want to update a crate, Cargo provides another command, update, which will ignore the `Cargo.lock` file and figure out all the latest versions that fit your specifications in `Cargo.toml`. If that works, Cargo will write those versions to the `Cargo.lock` file. But by default, Cargo will only look for versions larger than `0.3.0` and smaller than `0.4.0`. If the `rand` crate has released two new versions, `0.3.15` and `0.4.0`, you would see the following if you ran cargo update.

  

> Another neat feature of Cargo is that you can run the `cargo doc --open`command, which will build documentation provided by all of your dependencies locally and open it in your browser.

## Keywords Currently in Use

The following is a list of keywords currently in use, with their functionality described.

-   `as` - perform primitive casting, disambiguate the specific trait containing an item, or rename items in `use` statements
    
-   `async` - return a `Future` instead of blocking the current thread
    
-   `await` - suspend execution until the result of a `Future` is ready
    
-   `break` - exit a loop immediately
    
-   `const` - define constant items or constant raw pointers
    
-   `continue` - continue to the next loop iteration
    
-   `crate` - in a module path, refers to the crate root
    
-   `dyn` - dynamic dispatch to a trait object
    
-   `else` - fallback for `if` and `if let` control flow constructs
    
-   `enum` - define an enumeration
    
-   `extern` - link an external function or variable
    
-   `false` - Boolean false literal
    
-   `fn` - define a function or the function pointer type
    
-   `for` - loop over items from an iterator, implement a trait, or specify a higher-ranked lifetime
    
-   `if` - branch based on the result of a conditional expression
    
-   `impl` - implement inherent or trait functionality
    
-   `in` - part of `for` loop syntax
    
-   `let` - bind a variable
    
-   `loop` - loop unconditionally
    
-   `match` - match a value to patterns
    
-   `mod` - define a module
    
-   `move` - make a closure take ownership of all its captures
    
-   `mut` - denote mutability in references, raw pointers, or pattern bindings
    
-   `pub` - denote public visibility in struct fields, `impl` blocks, or modules
    
-   `ref` - bind by reference
    
-   `return` - return from function
    
-   `Self` - a type alias for the type we are defining or implementing
    
-   `self` - method subject or current module
    
-   `static` - global variable or lifetime lasting the entire program execution
    
-   `struct` - define a structure
    
-   `super` - parent module of the current module
    
-   `trait` - define a trait
    
-   `true` - Boolean true literal
    
-   `type` - define a type alias or associated type
    
-   `union` - define a [union](https://doc.rust-lang.org/reference/items/unions.html); is only a keyword when used in a union declaration
    
-   `unsafe` - denote unsafe code, functions, traits, or implementations
    
-   `use` - bring symbols into scope
    
-   `where` - denote clauses that constrain a type
    
-   `while` - loop conditionally based on the result of an expression
    

## Keywords Reserved for Future Use

The following keywords do not yet have any functionality but are reserved by Rust for potential future use.

-   `abstract`
    
-   `become`
    
-   `box`
    
-   `do`
    
-   `final`
    
-   `macro`
    
-   `override`
    
-   `priv`
    
-   `try`
    
-   `typeof`
    
-   `unsized`
    
-   `virtual`
    
-   `yield`

> _Raw identifiers_ are the syntax that lets you use keywords where they wouldn’t normally be allowed. You use a raw identifier by prefixing a  keyword with `r#`.

**Constants**

First, you aren’t allowed to use `mut` with constants. Constants aren’t just immutable by default they’re always immutable. You declare constants using the `const` keyword instead of the `let` keyword, and the type of the value *must be annotated*.

       const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;

The last diﬀerence is that constants may be set only to a *constant expression*, not the result of a value that could only be computed at runtime.

> Constants are valid for the entire time a program runs, within the
> scope they were declared in.

**Shadowing**
You can declare a new variable with the same name as a previous variable. **Rustaceans** say that the ﬁrst variable is *shadowed* by the second, which means that the second variable is what the compiler will see when you use the name of the variable. In eﬀect, the second variable overshadows the ﬁrst, taking any uses of the variable name to itself until either it itself is shadowed or the scope ends. We can shadow a variable by using the same variable’s name and repeating the use of the `let` keyword as follows:

    fn main() {
	    let x = 5;
	    let x = x + 1;
	    {
		    let x = x * 2;
		    println!("The value of x in the inner scope is: {x}");
	    }
	    println!("The value of x is: {x}");
    }

Shadowing is diﬀerent from marking a variable as `mut` , because we’ll get a compile-time error if we accidentally try to reassign to this variable without using the `let` keyword. By using `let` , we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.

The other diﬀerence between `mut` and shadowing is that because we’re eﬀectively creating a new variable when we use the `let` keyword again, we can change the type of the value but reuse the same name. For example, say our program asks a user to show how many spaces they want between some text by inputting space characters, and then we want to store that input as a number:

    let spaces = " ";
    let spaces = spaces.len();

The ﬁrst spaces variable is a string type and the second spaces variable is a number type. Shadowing thus spares us from having to come up with diﬀerent names, such as `spaces_str` and `spaces_num` ; instead, we can reuse the simpler spaces name. However, if we try to use `mut` for this, as shown here, we’ll get a compile-time error:

    let mut spaces = " ";		// Compile-time Error
    spaces = spaces.len(); 
  

**Data Types**

A *scalar type* represents a single value. Rust has four primary scalar types: *integers, ﬂoating-point numbers, Booleans, and characters.*

## **Integer Types**

 |Length | Signed  |Unsigned
|----------|---------|-------
| 8-bit      | i8 |u8
| 16-bit | i16 | u16
| 32-bit | i32 | u32
| 64-bit | i64 | u64
|128-bit |i128 |u128
|arch | isize | usize

Each signed variant can store numbers from `-(2n - 1)` to `2n - 1 - 1` inclusive, where `n` is the number of bits that variant uses.

>  **Note :** that number literals that can be multiple numeric types allow a type suﬃx, such as `57u8` , to designate the type. Number literals can also use `_` as a visual separator to make the number easier to read, such as `1_000` , which will have the same value as if you had speciﬁed `1000` .

Number literals |Example
|-------------|----------
| Decimal 	|	`98_222`
|Hex		|		 `0xff`
Octal 			|	`0o77`
Binary 		|	`0b1111_0000`
Byte ( u8 only) | `b'A'`

  
  

**Integer Overﬂow**

Let’s say you have a variable of type `u8` that can hold values between 0 and 255. If you try to change the variable to a value outside of that range, such as 256, integer overﬂow will occur, which can result in one of two behaviors. When you’re compiling in debug mode, Rust includes checks for integer overﬂow that cause your program to panic at runtime if this behavior occurs. Rust uses the term panicking when a program exits with an error.

When you’re compiling in release mode with the `--release` ﬂag, Rust does not include checks for integer overﬂow that cause panics. Instead, if overﬂow occurs, Rust performs two’s complement wrapping. In short, values greater than the maximum value the type can hold “wrap around” to the minimum of the values the type can hold. In the case of a `u8` , the value `256` becomes `0`, the value `257` becomes `1`, and so on. The program won’t panic, but the variable will have a value that probably isn’t what you were expecting it to have. Relying on integer overﬂow’s wrapping behavior is considered an error.

To explicitly handle the possibility of overﬂow, you can use these families of methods provided by the standard library for primitive numeric types:

• Wrap in all modes with the `wrapping_*` methods, such as `wrapping_add`

• Return the None value if there is overﬂow with the `checked_*` methods

• Return the value and a boolean indicating whether there was overﬂow with the `overflowing_*` methods

• Saturate at the value’s minimum or maximum values with `saturating_*` methods


**Floating-Point Types**

Rust also has two primitive types for ﬂoating-point numbers, which are numbers with decimal points. Rust’s ﬂoating-point types are `f32` and `f64`, which are `32 bits` and `64 bits` in size, respectively. The default type is `f64` because on modern CPUs it’s roughly the same speed as `f32` but is capable of more precision. All ﬂoating-point types are **signed**.

> Floating-point numbers are represented according to the IEEE-754 standard. The f32 type is a single-precision ﬂoat, and f64 has double precision.

  
**Numeric Operations**

Rust supports the basic mathematical operations you’d expect for all of the number types: addition, subtraction, multiplication, division, and remainder. Integer division rounds down to the nearest integer. 

    fn main() {
	    let sum = 5 + 10;							// addition
	    let difference = 95.5 - 4.3;				// subtraction
	    let product = 4 * 30;						// multiplication
	    let quotient = 56.7 / 32.2;					// division
	    let floored = 2 / 3; 						// Results in 0
	    let remainder = 43 % 5;						// remainder
    }

**The Boolean Type**

As in most other programming languages, a Boolean type in Rust has two possible values: `true` and `false` . Booleans are one byte in size. The Boolean type in Rust is speciﬁed using `bool` .

**The Character Type**

Rust’s char type is the language’s most primitive alphabetic type. Here’s some examples of declaring char values:

    fn main() {
	    let c = 'z';
	    let z: char = 'ℤ'; // with explicit type annotation
    }

> Note that we specify `char` literals with single quotes, as opposed to `string` literals, which use double quotes. Rust’s char type is *four bytes* in size and represents a Unicode Scalar Value, which means it can represent a lot more than just **ASCII**. Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width space are all valid char values in Rust. Unicode Scalar Values range from `U+0000` to `U+D7FF` and `U+E000` to `U+10FFFF` inclusive.

  
  

**Compound Types**

Compound types can group multiple values into one type. Rust has two primitive compound types: `tuples` and `arrays`.

**The Tuple Type**

A tuple is a general way of grouping together a number of values with a variety of types into one compound type. Tuples have a ﬁxed length: once declared, they cannot grow or shrink in size. We create a tuple by writing a comma-separated list of values inside parentheses. Each position in the tuple has a type, and the types of the diﬀerent values in the tuple don’t have to be the same.

    fn main() {
    	let tup: (i32, f64, u8) = (500, 6.4, 1);
    }

The variable `tup` binds to the entire tuple, because a tuple is considered a single compound element. To get the individual values out of a tuple, we can use pattern matching to destructure a tuple value, like this:

    fn main() {
    	let tup = (500, 6.4, 1);
    	let (x, y, z) = tup;
    	println!("The value of y is: {y}");
    }

This program ﬁrst creates a tuple and binds it to the variable `tup` . It then uses a pattern with `let` to take `tup` and turn it into three separate variables, `x` , `y` , and `z` . This is called destructuring, because it breaks the single tuple into three parts. Finally, the program prints the value of `y` , which is `6.4` .

We can also access a tuple element directly by using a period `( . )` followed by the index of the value we want to access. For example:

    fn main() {
    	let x: (i32, f64, u8) = (500, 6.4, 1);
    	let five_hundred = x.0;
    	let six_point_four = x.1;
    	let one = x.2;
    }

This program creates the tuple `x` and then accesses each element of the tuple using their respective indices. As with most programming languages, the ﬁrst index in a tuple is `0`. The tuple without any values has a special name, `unit`. This value and its corresponding type are both written `()` and represent an empty value or an empty return type. Expressions implicitly return the unit value if they don’t return any other value.


**The Array Type**

Another way to have a collection of multiple values is with an array. Unlike a tuple, every element of an array must have the same type. Unlike arrays in some other languages, arrays in Rust have a ﬁxed length. We write the values in an array as a comma-separated list inside square brackets:

    fn main() {
    	let a = [1, 2, 3, 4, 5];
    }

> Arrays are useful when you want your data allocated on the stack rather than the heap or when you want to ensure you always have a ﬁxed number of elements. An array isn’t as ﬂexible as the vector type, though. A vector is a similar collection type provided by the standard library that is allowed to grow or shrink in size.

You write an array’s type using square brackets with the type of each element, a semicolon, and then the number of elements in the array, like so:

    let a: [i32; 5] = [1, 2, 3, 4, 5];

You can also initialize an array to contain the same value for each element by specifying the initial value, followed by a semicolon, and then the length of the array in square brackets, as shown here:

    let a = [3; 5];

The array named a will contain `5` elements that will all be set to the value `3` initially. This is the same as writing let `a = [3, 3, 3, 3, 3];` but in a more concise way.

  
  

**Accessing Array Elements**

An array is a single chunk of memory of a known, ﬁxed size that can be allocated on the stack. You can access elements of an array using indexing, like this:

    fn main() {
    	let a = [1, 2, 3, 4, 5];
    	let first = a[0];
    	let second = a[1];
    }

  
  
  

> Rust code uses snake case as the conventional style for function and variable names, in which all letters are lowercase and underscores separate words.

  
  

**Statements and Expressions**

Function bodies are made up of a series of statements optionally ending in an expression. So far, the functions we’ve covered haven’t included an ending expression, but you have seen an expression as part of a statement. Because **Rust is an expression-based language**, this is an important distinction to understand. Other languages don’t have the same distinctions, so let’s look at what statements and expressions are and how their diﬀerences aﬀect the bodies of functions.

Statements are instructions that perform some action and do not return a value. Expressions evaluate to a resulting value. Let’s look at some examples.

We’ve actually already used statements and expressions. Creating a variable and assigning a value to it with the `let` keyword is a statement. 

    fn main() {
    	let y = 6;
    }

Expressions evaluate to a value and make up most of the rest of the code that you’ll write in Rust. Consider a math operation, such as `5 + 6` , which is an expression that evaluates to the value `11` . Expressions can be part of statements, the `6` in the statement `let y = 6;` is an expression that evaluates to the value `6` . Calling a function is an expression. Calling a macro is an expression. A new scope block created with curly brackets is an expression, for example:

    fn main() {
    	let y = {
    		let x = 3;
    		x + 1
    	};
    	println!("The value of y is: {y}");
    }

This expression:

    {
	    let x = 3;
	    x + 1
    }

is a block that, in this case, evaluates to `4` . That value gets bound to `y` as part of the `let` statement. Note that the `x + 1` line doesn’t have a semicolon at the end, unlike most of the lines you’ve seen so far. **Expressions do not include ending semicolons**. If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value. Keep this in mind as you explore function return values and expressions next.
 
**Functions with Return Values**

Functions can return values to the code that calls them. We don’t name return values, but we must declare their type after an arrow `->` . In Rust, the return value of the function is synonymous with the value of the ﬁnal expression in the block of the body of a function. You can return early from a function by using the `return` keyword and specifying a value, but most functions return the last expression implicitly. Here’s an example of a function that returns a value:

    fn five() -> i32 {
    	5
    }
    
    fn main() {
    	let x = five();
    	println!("The value of x is: {x}");
    }

  
  

**if Expressions**

An `if` expression allows you to branch your code depending on conditions. You provide a condition and then state, “If this condition is met, run this block of code. If the condition is not met, do not run this block of code.” Blocks of code associated with the conditions in if expressions are sometimes called arms, just like the arms in match expressions

    fn main() {
    	let number = 3;
    	if number < 5 {
    		println!("condition was true");
    	} else {
    		println!("condition was false");
    	}
    }

**Handling Multiple Conditions with else if**

You can use multiple conditions by combining if and else in an else if expression. For example:

    fn main() {
    	let number = 6;
    	if number % 4 == 0 {
    		println!("number is divisible by 4");
    	} else if number % 3 == 0 {
    		println!("number is divisible by 3");
    	} else if number % 2 == 0 {
    		println!("number is divisible by 2");
    	} else {
    		println!("number is not divisible by 4, 3, or 2");
    	}
    }

When this program executes, it checks each if expression in turn and executes the ﬁrst body for which the condition holds true. Note that even though 6 is divisible by 2, we don’t see the output number is divisible by 2 , nor do we see the number is not divisible by 4, 3, or 2 text from the else block. That’s because Rust only executes the block for the ﬁrst true condition, and once it ﬁnds one, it doesn’t even check the rest.

**Using if in a let Statement**

Because if is an expression, we can use it on the right side of a let statement to assign the outcome to a variable,

    fn main() {
    	let condition = true;
    	let number = if condition { 5 } else { 6 };
    	println!("The value of number is: {number}");
    }

> Rust has three kinds of loops: `loop` , `while` , and `for` .

The `loop` keyword tells Rust to execute a block of code over and over again forever or until you explicitly tell it to stop.

  
  

**Returning Values from Loops**

One of the uses of a loop is to retry an operation you know might fail, such as checking whether at thread has completed its job. You might also need to pass the result of that operation out of the loop to the rest of your code. To do this, you can add the value you want returned after the break expression you use to stop the loop; that value will be returned out of the loop so you can use it, as shown here:

    fn main() {
    	let mut counter = 0;
    	let result = loop {
    		counter += 1;
    		if counter == 10 {
    			break counter * 2;
    		}
    	};
    	println!("The result is {result}");
    }

  
  

**Loop Labels to Disambiguate Between Multiple Loops**

If you have loops within loops, break and continue apply to the innermost loop at that point. You can optionally specify a loop label on a loop that we can then use with break or continue to specify that those keywords apply to the labeled loop instead of the innermost loop. Loop labels must begin with a single quote. Here’s an example with two nested loops:

    fn main() {
    	let mut count = 0;
    	'counting_up: loop {
    		println!("count = {count}");
    		let mut remaining = 10;
    		loop {
    			println!("remaining = {remaining}");
    			if remaining == 9 {
    				break;
    			}
    			if count == 2 {
    				break 'counting_up;
    			}
    			remaining -= 1;
    		}
	    	count += 1;
    	}
    	println!("End count = {count}");
    }

The outer loop has the label `'counting_up` , and it will count up from `0` to `2`. The inner loop without a label counts down from `10` to `9`. The ﬁrst break that doesn’t specify a label will exit the inner loop only. The `break 'counting_up;` statement will exit the outer loop.

  
  

  
  

  
  

  
  

**For**

Here’s what the countdown would look like using a for loop and another method we’ve not yet talked about, rev , to reverse the range:

    fn main() {
    	for number in (1..4).rev() {
    		println!("{number}!");
    	}
    	println!("LIFTOFF!!!");
    }

  
  

  
  

## _**What Is Ownership?**_

Ownership is a set of rules that governs how a Rust program manages memory. All programs have to manage the way they use a computer’s memory while running. Some languages have garbage collection that regularly looks for no-longer used memory as the program runs; in other languages, the programmer must explicitly allocate and free the memory. Rust uses a third approach: memory is managed through a system of ownership with a set of rules that the compiler checks. If any of the rules are violated, the program won’t compile. None of the features of ownership will slow down your program while it’s running.

  
  

**Ownership Rules**

First, let’s take a look at the ownership rules. Keep these rules in mind as we work through the examples that illustrate them:

• Each value in Rust has an owner.

• There can only be one owner at a time.

• When the owner goes out of scope, the value will be dropped.

  

**Memory and Allocation**

In the case of a string literal, we know the contents at compile time, so the text is hardcoded directly into the ﬁnal executable. This is why string literals are fast and eﬃcient. But these properties only come from the string literal’s immutability. Unfortunately, we can’t put a blob of memory into the binary for each piece of text whose size is unknown at compile time and whose size might change while running the program.

With the String type, in order to support a mutable, growable piece of text, we need to allocate an amount of memory on the heap, unknown at compile time, to hold the contents. This means:

• The memory must be requested from the memory `allocator` at runtime.

• We need a way of returning this memory to the `allocator` when we’re done with our `String` .

That ﬁrst part is done by us: when we call `String::from` , its implementation requests the memory it needs. This is pretty much universal in programming languages.

However, the second part is diﬀerent. In languages with a garbage collector (GC), the GC keeps track of and cleans up memory that isn’t being used anymore, and we don’t need to think about it. In most languages without a GC, it’s our responsibility to identify when memory is no longer being used and call code to explicitly free it, just as we did to request it. Doing this correctly has historically been a diﬃcult programming problem. If we forget, we’ll waste memory. If we do it too early, we’ll have an invalid variable. If we do it twice, that’s a bug too. We need to pair exactly one allocate with exactly one free .

Rust takes a diﬀerent path: the memory is automatically returned once the variable that owns it goes out of scope.

    { 
	    let s = String::from("hello");// s is valid from this point //forward
	    // do stuff with s  
    } 	// this scope is now over, and s is no   
	    // longer valid

There is a natural point at which we can return the memory our String needs to the `allocator:` when `s` goes out of scope. When a variable goes out of scope, Rust calls a special function for us. This function is called `drop` , and it’s where the author of `String` can put the code to return the memory. Rust calls `drop` automatically at the closing curly bracket.

  
  

**Ways Variables and Data Interact: Clone**

If we do want to deeply copy the heap data of the String , not just the stack data, we can use a common method called `clone` . 

    let s1 = String::from("hello"); 
    let s2 = s1.clone();
    println!("s1 = {}, s2 = {}", s1, s2);

*Stack-Only Data: Copy*

    let x = 5;
    let y = x;
    println!("x = {}, y = {}", x, y);

But this code seems to contradict what we just learned: we don’t have a call to `clone` , but `x` is still valid and wasn’t moved into `y` .

The reason is that types such as integers that have a known size at compile time are stored entirely on the stack, so copies of the actual values are quick to make. That means there’s no reason we would want to prevent `x` from being valid after we create the variable `y` . In other words, there’s no diﬀerence between deep and shallow copying here, so calling clone wouldn’t do anything diﬀerent from the usual shallow copying and we can leave it out.

So what types implement the `Copy` trait? You can check the documentation for the given type to be sure, but as a general rule, any group of simple scalar values can implement `Copy` , and nothing that requires allocation or is some form of resource can implement `Copy` . Here are some of the types that implement Copy :

• All the integer types, such as `u32` .
• The Boolean type, `bool` , with values `true` and `false` .
• All the ﬂoating point types, such as `f64` .
• The character type, `char` .
• Tuples, if they only contain types that also implement `Copy` . For example, (`i32`, `i32`) implements `Copy` , but (`i32`, `String`) does not.

  
  

The ownership of a variable follows the same pattern every time: assigning a value to another variable moves it. When a variable that includes data on the heap goes out of scope, the value will be cleaned up by drop unless ownership of the data has been moved to another variable.

  
  

**References and Borrowing**

A reference is like a pointer in that it’s an address we can follow to access the data stored at that address; that data is owned by some other variable. Unlike a pointer, a reference is guaranteed to point to a valid value of a particular type for the life of that reference.

    fn main() {
    	let s1 = String::from("hello");
    	let len = calculate_length(&s1);
    	println!("The length of '{}' is {}.", s1, len);
    }
    fn calculate_length(s: &String) -> usize {
    	s.len()
    }

First, notice that all the tuple code in the variable declaration and the function return value is gone. Second, note that we pass `&s1` into `calculate_length` and, in its deﬁnition, we take `&String` rather than `String` . These ampersands represent references, and they allow you to refer to some value without taking ownership of it.

> **Note:** The opposite of referencing by using `&` is dereferencing, which is accomplished with the dereference operator, `*` .

  
  

We call the action of creating a reference borrowing. As in real life, if a person owns something, you can borrow it from them. When you’re done, you have to give it back. You don’t own it.

So what happens if we try to modify something we’re borrowing

    // !! Compile time Error !!
    fn main() {
    	let s = String::from("hello");
    	change(&s);
    }
    fn change(some_string: &String) {
    	some_string.push_str(", world");
    }

  
  

Just as variables are immutable by default, so are references. We’re not allowed to modify something we have a reference to.

  
  

**Mutable References**

Mutable references have one big restriction: if you have a mutable reference to a value, you can have no other references to that value. This code that attempts to create two mutable references to `s` will fail:

    let mut s = String::from("hello");
    let r1 = &mut s;
    let r2 = &mut s;
    println!("{}, {}", r1, r2);

The restriction preventing multiple mutable references to the same data at the same time allows for mutation but in a very controlled fashion. It’s something that new Rustaceans struggle with, because most languages let you mutate whenever you’d like. The beneﬁt of having this restriction is that Rust can prevent data races at compile time. A data race is similar to a race condition and happens when these three behaviors occur:

• Two or more pointers access the same data at the same time.
• At least one of the pointers is being used to write to the data.
• There’s no mechanism being used to synchronize access to the data.

As always, we can use curly brackets to create a new scope, allowing for multiple mutable references, just not simultaneous ones:

    let mut s = String::from("hello");
    {
	    let r1 = &mut s;
    } // r1 goes out of scope here, so we can make a new reference with no problems.
    let r2 = &mut s;

Rust enforces a similar rule for combining mutable and immutable references. This code results in an error:

    let mut s = String::from("hello");
    let r1 = &s; // no problem
    let r2 = &s; // no problem
    let r3 = &mut s; // BIG PROBLEM
    println!("{}, {}, and {}", r1, r2, r3);

Whew! We also cannot have a mutable reference while we have an immutable one to the same value.

Users of an immutable reference don’t expect the value to suddenly change out from under them! However, multiple immutable references are allowed because no one who is just reading the data has the ability to aﬀect anyone else’s reading of the data.

  
  

Note that a reference’s scope starts from where it is introduced and continues through the last time that reference is used. For instance, this code will compile because the last usage of the immutable references, the `println!` , occurs before the mutable reference is introduced:

    let mut s = String::from("hello");
    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{} and {}", r1, r2);
    // variables r1 and r2 will not be used after this point
    let r3 = &mut s; // no problem
    println!("{}", r3);

The scopes of the immutable references `r1` and `r2` end after the `println!` where they are last used, which is before the mutable reference `r3` is created. These scopes don’t overlap, so this code is allowed. The ability of the compiler to tell that a reference is no longer being used at a point before the end of the scope is called Non-Lexical Lifetimes (NLL for short),


**String Slices**

A string slice is a reference to part of a String , and it looks like this:

    let s = String::from("hello world");
    let hello = &s[0..5];
    let world = &s[6..11];

Rather than a reference to the entire `String` , `hello` is a reference to a portion of the `String`, speciﬁed in the extra `[0..5]` bit. We create slices using a range within brackets by specifying **[starting_index..ending_index]** , where *starting_index* is the ﬁrst position in the slice and *ending_index* is one more than the last position in the slice. Internally, the slice data structure stores the starting position and the length of the slice, which corresponds to *ending_index* minus *starting_index* . So in the case of `let world = &s[6..11];` , world would be a slice that contains a pointer to the byte at index `6` of `s` with a length value of `5`.

With Rust’s `..` range syntax, if you want to start at index zero, you can drop the value before the two periods. In other words, these are equal:

    let s = String::from("hello");
    let slice = &s[0..2];
    let slice = &s[..2];  

By the same token, if your slice includes the last byte of the String , you can drop the trailing number. That means these are equal:

    let s = String::from("hello");
    let len = s.len();
    let slice = &s[3..len];
    let slice = &s[3..];

You can also drop both values to take a slice of the entire string. So these are equal:

    let s = String::from("hello");
    let len = s.len();
    let slice = &s[0..len];
    let slice = &s[..];

  
  

**Deﬁning and Instantiating Structs**

    fn build_user(email: String, username: String) -> User {
    	User {
    		email: email,
    		username: username,
    		active: true,
    		sign_in_count: 1,
    	}
    }

It makes sense to name the function parameters with the same name as the struct ﬁelds, but having to repeat the email and username ﬁeld names and variables is a bit tedious. If the struct had more ﬁelds, repeating each name would get even more annoying.

**Using the Field Init Shorthand**

Because the parameter names and the struct ﬁeld names are exactly the same in last example, we can use the ﬁeld init shorthand syntax to rewrite `build_user` so that it behaves exactly the same but doesn’t have the repetition of email and username 

    fn build_user(email: String, username: String) -> User {
    	User {
    		email,
    		username,
    		active: true,
    		sign_in_count: 1,
    	}
    }

Here, we’re creating a new instance of the `User` struct, which has a ﬁeld named `email` . We want to set the email ﬁeld’s value to the value in the email parameter of the `build_user` function. Because the email ﬁeld and the email parameter have the same name, we only need to write `email` rather than `email: email` .

**Creating Instances From Other Instances With Struct Update Syntax**

It’s often useful to create a new instance of a struct that includes most of the values from another instance, but changes some. You can do this using struct update syntax.

    fn main() {
	    // --snip--
	    let user2 = User {
		    active: user1.active,
		    username: user1.username,
		    email: String::from("another@example.com"),
		    sign_in_count: user1.sign_in_count,
	    };
    }

  
  

Using struct update syntax, we can achieve the same eﬀect with less code, as shown in last example. The syntax `..` speciﬁes that the remaining ﬁelds not explicitly set should have the same value as the ﬁelds in the given instance. 

    fn main() {
	    // --snip--
    	let user2 = User {
    		email: String::from("another@example.com"),
    		..user1
    	};
    }

The code in Listing 5-7 also creates an instance in user2 that has a diﬀerent value for email but has the same values for the username , active , and sign_in_count ﬁelds from user1 . The ..user1 must come last to specify that any remaining ﬁelds should get their values from the corresponding ﬁelds in user1 , but we can choose to specify values for as many ﬁelds as we want in any order, regardless of the order of the ﬁelds in the struct’s deﬁnition.

**Note** that the struct update syntax uses = like an assignment; this is because it moves the data, just as we saw in the “Ways Variables and Data Interact: Move” section. In this example, we can no longer use user1 after creating user2 because the String in the username ﬁeld of user1 was moved into user2 . If we had given user2 new String values for both email and username , and thus only used the active and sign_in_count values from user1 , then user1 would still be valid after creating user2 . The types of active and sign_in_count are types that implement the Copy trait, so the behavior we discussed in the “Stack-Only Data: Copy” section would apply.

  
  

**Using Tuple Structs without Named Fields to Create Diﬀerent Types**

Rust also supports structs that look similar to tuples, called tuple structs. Tuple structs have the added meaning the struct name provides but don’t have names associated with their ﬁelds; rather, they just have the types of the ﬁelds. Tuple structs are useful when you want to give the whole tuple a name and make the tuple a diﬀerent type from other tuples, and when naming each ﬁeld as in a regular struct would be verbose or redundant.

struct Color(i32, i32, i32);

struct Point(i32, i32, i32);

fn main() {

let black = Color(0, 0, 0);

let origin = Point(0, 0, 0);

}

  
  

**Unit-Like Structs Without Any Fields**

You can also deﬁne structs that don’t have any ﬁelds! These are called unit-like structs because they behave similarly to () , the unit type that we mentioned in “The Tuple Type” section. Unit-like structs can be useful when you need to implement a trait on some type but don’t have any data that you want to store in the type itself.

struct AlwaysEqual;

fn main() {

let subject = AlwaysEqual;

}

  
  

**Method Syntax**

Methods are similar to functions: we declare them with the fn keyword and a name, they can have parameters and a return value, and they contain some code that’s run when the method is called from somewhere else. Unlike functions, methods are deﬁned within the context of a struct (or an enum or a trait object, which we cover in Chapters 6 and 17, respectively), and their ﬁrst parameter is always self , which represents the instance of the struct the method is being called on.

struct Rectangle {

width: u32,

height: u32,

}

impl Rectangle {

fn area(&self) -> u32 {

self.width * self.height

}

}

fn main() {

let rect1 = Rectangle {

width: 30,

height: 50,

};

println!(

"The area of the rectangle is {} square pixels.",

rect1.area()

);

}

  
  

To deﬁne the function within the context of Rectangle , we start an impl (implementation) block for Rectangle . Everything within this impl block will be associated with the Rectangle type. Then we move the area function within the impl curly brackets and change the ﬁrst (and in this case, only) parameter to be self in the signature and everywhere within the body. In main , where we called the area function and passed rect1 as an argument, we can instead use method syntax to call the area method on our Rectangle instance. The method syntax goes after an instance: we add a dot followed by the method name, parentheses, and any arguments.

In the signature for area , we use &self instead of rectangle: &Rectangle . The &self is actually short for self: &Self . Within an impl block, the type Self is an alias for the type that the impl block is for. Methods must have a parameter named self of type Self for their ﬁrst parameter, so Rust lets you abbreviate this with only the name self in the ﬁrst parameter spot. Note that we stillneed to use the & in front of the self shorthand to indicate this method borrows the Self instance, just as we did in rectangle: &Rectangle . Methods can take ownership of self , borrow self immutably as we’ve done here, or borrow self mutably, just as they can any other parameter.

We’ve chosen &self here for the same reason we used &Rectangle in the function version: we don’t want to take ownership, and we just want to read the data in the struct, not write to it. If we wanted to change the instance that we’ve called the method on as part of what the method does, we’d use &mut self as the ﬁrst parameter. Having a method that takes ownership of the instance by using just self as the ﬁrst parameter is rare; this technique is usually used when the method transforms self into something else and you want to prevent the caller from using the original instance after the transformation.

Note that we can choose to give a method the same name as one of the struct’s ﬁelds. For example, we can deﬁne a method on Rectangle also named width :

impl Rectangle {

fn width(&self) -> bool {

self.width > 0

}

}

  
  

Often, but not always, when we give methods with the same name as a ﬁeld we want it to only return the value in the ﬁeld and do nothing else. Methods like this are called getters, and Rust does not implement them automatically for struct ﬁelds as some other languages do. Getters are useful because you can make the ﬁeld private but the method public and thus enable read-only access to that ﬁeld as part of the type’s public API. We will be discussing what public and private are and how to designate a ﬁeld or method as public or private in Chapter 7.

  
  

**Associated Functions**

All functions deﬁned within an impl block are called associated functions because they’re associated with the type named after the impl . We can deﬁne associated functions that don’t have self as their ﬁrst parameter (and thus are not methods) because they don’t need an instance of the type to work with. We’ve already used one function like this: the String::from function that’s deﬁned on the String type.

Associated functions that aren’t methods are often used for constructors that will return a new instance of the struct. These are often called new , but new isn’t a special name and isn’t built intothe language. For example, we could choose to provide an associated function named square that would have one dimension parameter and use that as both width and height, thus making it easier to create a square Rectangle rather than having to specify the same value twice:

impl Rectangle {

fn square(size: u32) -> Self {

Self {

width: size,

height: size,

}

}

}

The **Self** keywords in the return type and in the body of the function are aliases for the type that appears after the impl keyword, which in this case is Rectangle .

To call this associated function, we use the :: syntax with the struct name; let sq = Rectangle::square(3); is an example. This function is namespaced by the struct: the :: syntax is used for both associated functions and namespaces created by modules. We’ll discuss modules in Chapter 7.

  
  

  
  

**Multiple impl Blocks**

Each struct is allowed to have multiple impl blocks.

impl Rectangle {

fn area(&self) -> u32 {

self.width * self.height

}

}

impl Rectangle {

fn can_hold(&self, other: &Rectangle) -> bool {

self.width > other.width && self.height > other.height

}

}

**Enums and Pattern Matching**

Enums allow you to deﬁne a type by enumerating its possible variants.

enum IpAddrKind {

V4,

V6,

}

IpAddrKind is now a custom data type that we can use elsewhere in our code.

**Enum Values**

We can create instances of each of the two variants of IpAddrKind like this:

let four = IpAddrKind::V4;

let six = IpAddrKind::V6;

Note that the variants of the enum are namespaced under its identiﬁer, and we use a double colon to separate the two. This is useful because now both values IpAddrKind::V4 and IpAddrKind::V6 are of the same type: IpAddrKind . We can then, for instance, deﬁne a function that takes any IpAddrKind :

fn route(ip_kind: IpAddrKind) {}

And we can call this function with either variant:

route(IpAddrKind::V4);

route(IpAddrKind::V6);

However, representing the same concept using just an enum is more concise: rather than an enum inside a struct, we can put data directly into each enum variant. This new deﬁnition of the IpAddr enum says that both V4 and V6 variants will have associated String values:

enum IpAddr {

V4(String),

V6(String),

}

let home = IpAddr::V4(String::from("127.0.0.1"));

let loopback = IpAddr::V6(String::from("::1"));

There’s another advantage to using an enum rather than a struct: each variant can have diﬀerent types and amounts of associated data. Version four type IP addresses will always have four numeric components that will have values between 0 and 255. If we wanted to store V4 addresses as four u8 values but still express V6 addresses as one String value, we wouldn’t be able to with a struct. Enums handle this case with ease:

enum IpAddr {

V4(u8, u8, u8, u8),

V6(String),

}

let home = IpAddr::V4(127, 0, 0, 1);

let loopback = IpAddr::V6(String::from("::1"));

-------------

struct Ipv4Addr {

// --snip--

}

struct Ipv6Addr {

// --snip--

}

enum IpAddr {

V4(Ipv4Addr),

V6(Ipv6Addr),

}

This code illustrates that you can put any kind of data inside an enum variant: strings, numeric types, or structs, for example. You can even include another enum! Also, standard library types are often not much more complicated than what you might come up with.

--------------------------------

enum Message {

Quit,

Move { x: i32, y: i32 },

Write(String),

ChangeColor(i32, i32, i32),

}

Deﬁning an enum with variants such as the ones in Listing 6-2 is similar to deﬁning diﬀerent kinds of struct deﬁnitions, except the enum doesn’t use the struct keyword and all the variants are grouped together under the Message type. The following structs could hold the same data that the preceding enum variants hold:

struct QuitMessage; // unit struct

struct MoveMessage {

x: i32,

y: i32,

}

struct WriteMessage(String); // tuple struct

struct ChangeColorMessage(i32, i32, i32); // tuple struct

But if we used the diﬀerent structs, which each have their own type, we couldn’t as easily deﬁne a function to take any of these kinds of messages as we could with the Message enum deﬁned in Listing 6-2, which is a single type.

There is one more similarity between enums and structs: just as we’re able to deﬁne methods on structs using impl , we’re also able to deﬁne methods on enums. Here’s a method named call that we could deﬁne on our Message enum:

impl Message {

fn call(&self) {

// method body would be defined here

}

}

let m = Message::Write(String::from("hello"));

m.call();

  
  

**The Option Enum and Its Advantages Over Null Values**

This section explores a case study of Option , which is another enum deﬁned by the standard library. The Option type encodes the very common scenario in which a value could be something or it could be nothing.

Programming language design is often thought of in terms of which features you include, but the features you exclude are important too. Rust doesn’t have the null feature that many other languages have. Null is a value that means there is no value there. In languages with null, variables can always be in one of two states: null or not-null.

The problem isn’t really with the concept but with the particular implementation. As such, Rust does not have nulls, but it does have an enum that can encode the concept of a value being present or absent. This enum is Option<T> , and it is deﬁned by the standard library as follows:

enum Option<T> {

None,

Some(T),

}

In short, because Option<T> and T (where T can be any type) are diﬀerent types, the compiler won’t let us use an Option<T> value as if it were deﬁnitely a valid value. For example, this code won’t compile because it’s trying to add an i8 to an Option<i8> :

let x: i8 = 5;

let y: Option<i8> = Some(5);

let sum = x + y;

In other words, you have to convert an Option<T> to a T before you can perform T operations with it. Generally, this helps catch one of the most common issues with null: assuming that something isn’t null when it actually is.

Eliminating the risk of incorrectly assuming a not-null value helps you to be more conﬁdent in your code. In order to have a value that can possibly be null, you must explicitly opt in by making the type of that value Option<T> . Then, when you use that value, you are required to explicitly handle the case when the value is null. Everywhere that a value has a type that isn’t an Option<T> , you can safely assume that the value isn’t null. This was a deliberate design decision for Rust to limit null’s pervasiveness and increase the safety of Rust code.

  
  

  
  

**The match Control Flow Construct**

Rust has an extremely powerful control ﬂow construct called match that allows you to compare a value against a series of patterns and then execute code based on which pattern matches. Patterns can be made up of literal values, variable names, wildcards, and many other things; Chapter 18 covers all the diﬀerent kinds of patterns and what they do. The power of match comes from the expressiveness of the patterns and the fact that the compiler conﬁrms that all possible cases are handled.

Think of a match expression as being like a coin-sorting machine: coins slide down a track with variously sized holes along it, and each coin falls through the ﬁrst hole it encounters that it ﬁts into. In the same way, values go through each pattern in a match , and at the ﬁrst pattern the value “ﬁts,” the value falls into the associated code block to be used during execution.

enum Coin {

Penny,

Nickel,

Dime,

Quarter,

}

fn value_in_cents(coin: Coin) -> u8 {

match coin {

Coin::Penny => 1,

Coin::Nickel => 5,

Coin::Dime => 10,

Coin::Quarter => 25,

}

}

This seems very similar to an expression used with if , but there’s a big diﬀerence: with **if** , the expression needs to return a Boolean value, but here, it can return any type.

  
  

**Patterns that Bind to Values**

Another useful feature of match arms is that they can bind to the parts of the values that match the pattern. This is how we can extract values out of enum variants.

  
  

  
  

**Catch-all Patterns and the _ Placeholder**

Using enums, we can also take special actions for a few particular values, but for all other values take one default action. Imagine we’re implementing a game where, if you roll a 3 on a dice roll, your player doesn’t move, but instead gets a new fancy hat. If you roll a 7, your player loses a fancy hat. For all other values, your player moves that number of spaces on the game board. Here’s a match that implements that logic, with the result of the dice roll hardcoded rather than a random value, and all other logic represented by functions without bodies because actually implementing them is out of scope for this example:

let dice_roll = 9;

match dice_roll {

3 => add_fancy_hat(),

7 => remove_fancy_hat(),

other => move_player(other),

}

fn add_fancy_hat() {}

fn remove_fancy_hat() {}

fn move_player(num_spaces: u8) {}

For the ﬁrst two arms, the patterns are the literal values 3 and 7. For the last arm that covers every other possible value, the pattern is the variable we’ve chosen to name other . The code that runs for the other arm uses the variable by passing it to the move_player function.

Rust also has a pattern we can use when we want a catch-all but don’t want to use the value in the catch-all pattern: _ is a special pattern that matches any value and does not bind to that value. This tells Rust we aren’t going to use the value, so Rust won’t warn us about an unused variable. Let’s change the rules of the game: now, if you roll anything other than a 3 or a 7, you must roll again. We no longer need to use the catch-all value, so we can change our code to use _ instead of the variable named other :

let dice_roll = 9;

match dice_roll {

3 => add_fancy_hat(),

7 => remove_fancy_hat(),

_ => reroll(),

}

fn add_fancy_hat() {}

fn remove_fancy_hat() {}

fn reroll() {}

This example also meets the exhaustiveness requirement because we’re explicitly ignoring all other values in the last arm; we haven’t forgotten anything. Finally, we’ll change the rules of the game one more time, so that nothing else happens on your turn if you roll anything other than a 3 or a 7. We can express that by using the unit value (the empty tuple type we mentioned in “The Tuple Type” section) as the code that goes with the _ arm:

let dice_roll = 9;

match dice_roll {

3 => add_fancy_hat(),

7 => remove_fancy_hat(),

_ => (),

}

fn add_fancy_hat() {}

fn remove_fancy_hat() {}

Here, we’re telling Rust explicitly that we aren’t going to use any other value that doesn’t match a pattern in an earlier arm, and we don’t want to run any code in this case.

  
  

**Concise Control Flow with if let**

The if let syntax lets you combine if and let into a less verbose way to handle values that match one pattern while ignoring the rest. Consider the program in Listing 6-6 that matches on an Option<u8> value in the config_max variable but only wants to execute code if the value is the Some variant.

let config_max = Some(3u8);

match config_max {

Some(max) => println!("The maximum is configured to be {}", max),

_ => (),

}

If the value is Some , we print out the value in the Some variant by binding the value to the variable max in the pattern. We don’t want to do anything with the None value. To satisfy the match expression, we have to add _ => () after processing just one variant, which is annoying boilerplate code to add.

Instead, we could write this in a shorter way using if let . The following code behaves the same as the match in Listing 6-6:

let config_max = Some(3u8);

if let Some(max) = config_max {

println!("The maximum is configured to be {}", max);

}

The syntax if let takes a pattern and an expression separated by an equal sign. It works the same way as a match , where the expression is given to the match and the pattern is its ﬁrst arm. In this case, the pattern is Some(max) , and the max binds to the value inside the Some . We can then use max in the body of the if let block in the same way as we used max in the corresponding match arm. The code in the if let block isn’t run if the value doesn’t match the pattern.

Using if let means less typing, less indentation, and less boilerplate code. However, you lose the exhaustive checking that match enforces. Choosing between match and if let depends on what you’re doing in your particular situation and whether gaining conciseness is an appropriate trade-oﬀ for losing exhaustive checking.

In other words, you can think of if let as syntax sugar for a match that runs code when the value matches one pattern and then ignores all other values.

  
  

**Packages and Crates**

A crate is the smallest amount of code that the Rust compiler considers at a time. Even if you run rustc rather than cargo and pass a single source code ﬁle, the compiler considers that ﬁle to be a crate. Crates can contain modules, and the modules may be deﬁned in other ﬁles that get compiled with the crate, as we’ll see in the coming sections.

A crate can come in one of two forms: a binary crate or a library crate. Binary crates are programs you can compile to an executable that you can run, such as a command-line program or a server. Each must have a function called main that deﬁnes what happens when the executable runs. All the crates we’ve created so far have been binary crates.

Library crates don’t have a main function, and they don’t compile to an executable. Instead, they deﬁne functionality intended to be shared with multiple projects.

A package can contain as many binary crates as you like, but at most only one library crate. A package must contain at least one crate, whether that’s a library or binary crate.

  
  

**Grouping Related Code in Modules**

Modules let us organize code within a crate for readability and easy reuse. Modules also allow us to control the privacy of items, because code within a module is private by default. Private items are internal implementation details not available for outside use. We can choose to make modules and the items within them public, which exposes them to allow external code to use and depend on them.

Earlier, we mentioned that src/main.rs and src/lib.rs are called crate roots. The reason for their name is that the contents of either of these two ﬁles form a module named crate at the root of the crate’s module structure, known as the module tree.

crate

└── front_of_house

├── hosting

│

├── add_to_waitlist

│

└── seat_at_table

└── serving

├── take_order

├── serve_order

└── take_payment

  
  

**Paths for Referring to an Item in the Module Tree**

To show Rust where to ﬁnd an item in a module tree, we use a path in the same way we use a path when navigating a ﬁlesystem. To call a function, we need to know its path.

A path can take two forms:

• An absolute path is the full path starting from a crate root; for code from an external crate, the absolute path begins with the crate name, and for code from the current crate, it starts with the literal crate .

• A relative path starts from the current module and uses self , super , or an identiﬁer in the current module.

Both absolute and relative paths are followed by one or more identiﬁers separated by double colons ( :: ).

mod front_of_house {

mod hosting {

fn add_to_waitlist() {}

}

}

pub fn eat_at_restaurant() {

// Absolute path

crate::front_of_house::hosting::add_to_waitlist();

// Relative path

front_of_house::hosting::add_to_waitlist();

}

The ﬁrst time we call the add_to_waitlist function in eat_at_restaurant , we use an absolute path. The add_to_waitlist function is deﬁned in the same crate as eat_at_restaurant , which means we can use the crate keyword to start an absolute path. We then include each of the successive modules until we make our way to add_to_waitlist . You can imagine a ﬁlesystem with the same structure: we’d specify the path /front_of_house/hosting/add_to_waitlist to run the add_to_waitlist program; using the crate name to start from the crate root is like using / to start from the ﬁlesystem root in your shell.

The second time we call add_to_waitlist in eat_at_restaurant , we use a relative path. The path starts with front_of_house , the name of the module deﬁned at the same level of the module tree as eat_at_restaurant . Here the ﬁlesystem equivalent would be using the path front_of_house/hosting/add_to_waitlist . Starting with a module name means that the path is relative.

Items in a parent module can’t use the private items inside child modules, but items in child modules can use the items in their ancestor modules. This is because child modules wrap and hide their implementation details, but the child modules can see the context in which they’re deﬁned. To continue with our metaphor, think of the privacy rules as being like the back oﬃce of a restaurant: what goes on in there is private to restaurant customers, but oﬃce managers can see and do everything in the restaurant they operate.

Rust chose to have the module system function this way so that hiding inner implementation details is the default. That way, you know which parts of the inner code you can change without breaking outer code. However, Rust does give you the option to expose inner parts of child modules’ code to outer ancestor modules by using the **pub** keyword to make an item public.

  
  

**Exposing Paths with the pub Keyword**

In the absolute path, we start with crate , the root of our crate’s module tree. The front_of_house module is deﬁned in the crate root. While front_of_house isn’t public, because the eat_at_restaurant function is deﬁned in the same module as front_of_house (that is, eat_at_restaurant and front_of_house are siblings), we can refer to front_of_house from eat_at_restaurant . Next is the hosting module marked with pub . We can access the parent

module of hosting , so we can access hosting . Finally, the add_to_waitlist function is marked with pub and we can access its parent module, so this function call works!

In the relative path, the logic is the same as the absolute path except for the ﬁrst step: rather than starting from the crate root, the path starts from front_of_house . The front_of_house module is deﬁned within the same module as eat_at_restaurant , so the relative path starting from the module in which eat_at_restaurant is deﬁned works. Then, because hosting and add_to_waitlist are marked with pub , the rest of the path works, and this function call is valid!

  
  

**Best Practices for Packages with a Binary and a Library**

We mentioned a package can contain both a src/main.rs binary crate root as well as a src/lib.rs library crate root, and both crates will have the package name by default. Typically, packages with this pattern of containing both a library and a binary crate will have just enough code in the binary crate to start an executable that calls code with the library crate. This lets other projects beneﬁt from the most functionality that the package provides, because the library crate’s code can be shared.

The module tree should be deﬁned in src/lib.rs. Then, any public items can be used in the binary crate by starting paths with the name of the package. The binary crate becomes a user of the library crate just like a completely external crate would use the library crate: it can only use the public API. This helps you design a good API; not only are you the author, you’re also a client!

  
  

**Starting Relative Paths with super**

We can construct relative paths that begin in the parent module, rather than the current module or the crate root, by using super at the start of the path. This is like starting a ﬁlesystem path with the .. syntax. Using super allows us to reference an item that we know is in the parent module, which can make rearranging the module tree easier when the module is closely related to the parent, but the parent might be moved elsewhere in the module tree someday.

Consider the code in Listing 7-8 that models the situation in which a chef ﬁxes an incorrect order and personally brings it out to the customer. The function fix_incorrect_order deﬁned in the back_of_house module calls the function deliver_order deﬁned in the parent module by specifying the path to deliver_order starting with super :

Filename: src/lib.rs

fn deliver_order() {}

mod back_of_house {

fn fix_incorrect_order() {

cook_order();

super::deliver_order();

}

fn cook_order() {}

}

The fix_incorrect_order function is in the back_of_house module, so we can use super to go to the parent module of back_of_house , which in this case is crate , the root. From there, we look for deliver_order and ﬁnd it. Success! We think the back_of_house module and the deliver_order function are likely to stay in the same relationship to each other and get moved together should we decide to reorganize the crate’s module tree. Therefore, we used super so we’ll have fewer places to update code in the future if this code gets moved to a diﬀerent module.

**Making Structs and Enums Public**

We can also use pub to designate structs and enums as public, but there are a few details extra to the usage of pub with structs and enums. If we use pub before a struct deﬁnition, we make the struct public, but the struct’s ﬁelds will still be private. We can make each ﬁeld public or not on a case-by-case basis. In Listing 7-9, we’ve deﬁned a public back_of_house::Breakfast struct with a public toast ﬁeld but a private seasonal_fruit ﬁeld. This models the case in a restaurant where the customer can pick the type of bread that comes with a meal, but the chef decides which fruit accompanies the meal based on what’s in season and in stock. The available fruit changes quickly, socustomers can’t choose the fruit or even see which fruit they’ll get.

mod back_of_house {

pub struct Breakfast {

pub toast: String,

seasonal_fruit: String,

}

impl Breakfast {

pub fn summer(toast: &str) -> Breakfast {

Breakfast {

toast: String::from(toast),

seasonal_fruit: String::from("peaches"),

}

}

}

}

pub fn eat_at_restaurant() {

// Order a breakfast in the summer with Rye toast

let mut meal = back_of_house::Breakfast::summer("Rye");

// Change our mind about what bread we'd like

meal.toast = String::from("Wheat");

println!("I'd like {} toast please", meal.toast);

  
  

// The next line won't compile if we uncomment it; we're not allowed

// to see or modify the seasonal fruit that comes with the meal

// meal.seasonal_fruit = String::from("blueberries");

  
  

In contrast, if we make an enum public, all of its variants are then public. We only need the pub before the enum keyword, as shown in Listing 7-10.

mod back_of_house {

pub enum Appetizer {

Soup,

Salad,

}

}

pub fn eat_at_restaurant() {

let order1 = back_of_house::Appetizer::Soup;

let order2 = back_of_house::Appetizer::Salad;

}

Because we made the Appetizer enum public, we can use the Soup and Salad variants in eat_at_restaurant . Enums aren’t very useful unless their variants are public; it would be annoying to have to annotate all enum variants with pub in every case, so the default for enum variants is to be public. Structs are often useful without their ﬁelds being public, so struct ﬁelds follow the general rule of everything being private by default unless annotated with pub .

**Bringing Paths into Scope with the _use_ Keyword**

Having to write out the paths to call functions can feel inconvenient and repetitive. In Listing 7-7,  whether we chose the absolute or relative path to the add_to_waitlist function, every time we wanted to call add_to_waitlist we had to specify front_of_house and hosting too. Fortunately, there’s a way to simplify this process: we can create a shortcut to a path with the use keyword once, and then use the shorter name everywhere else in the scope.

In Listing 7-11, we bring the crate::front_of_house::hosting module into the scope of the eat_at_restaurant function so we only have to specify hosting::add_to_waitlist to call the add_to_waitlist function in eat_at_restaurant .

mod front_of_house {

pub mod hosting {

pub fn add_to_waitlist() {}

}

}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {

hosting::add_to_waitlist();

}

Adding use and a path in a scope is similar to creating a symbolic link in the ﬁlesystem. By adding use crate::front_of_house::hosting in the crate root, hosting is now a valid name in that scope, just as though the hosting module had been deﬁned in the crate root. Paths brought into scope with use also check privacy, like any other paths.

  
  

**Providing New Names with the as Keyword**

There’s another solution to the problem of bringing two types of the same name into the same scope with use : after the path, we can specify as and a new local name, or alias, for the type. Listing 7-16 shows another way to write the code in Listing 7-15 by renaming one of the two Result types using as :

use std::fmt::Result;

use std::io::Result as IoResult;

fn function1() -> Result {

// --snip--

}

**Re-exporting Names with pub use**

When we bring a name into scope with the use keyword, the name available in the new scope is private. To enable the code that calls our code to refer to that name as if it had been deﬁned in that code’s scope, we can combine pub and use . This technique is called re-exporting because we’re bringing an item into scope but also making that item available for others to bring into their scope. Listing 7-17 shows the code in Listing 7-11 with use in the root module changed to pub use .

mod front_of_house {

pub mod hosting {

pub fn add_to_waitlist() {}

}

}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {

hosting::add_to_waitlist();

}

Using Nested Paths to Clean Up Large use Lists If we’re using multiple items deﬁned in the same crate or same module, listing each item on its own line can take up a lot of vertical space in our ﬁles. For example, these two use statements we had in the Guessing Game in Listing 2-4 bring items from std into scope:

// --snip--

use std::cmp::Ordering;

use std::io;

// --snip--

Instead, we can use nested paths to bring the same items into scope in one line. We do this by specifying the common part of the path, followed by two colons, and then curly brackets around a list of the parts of the paths that diﬀer, as shown in Listing 7-18.

// --snip--

use std::{cmp::Ordering, io};

// --snip--

We can use a nested path at any level in a path, which is useful when combining two use statements that share a subpath. For example, Listing 7-19 shows two use statements: one that brings std::io into scope and one that brings std::io::Write into scope.

use std::io;

use std::io::Write;

The common part of these two paths is std::io , and that’s the complete ﬁrst path. To merge thesetwo paths into one use statement, we can use self in the nested path, as shown in Listing 7-20.

use std::io::{self, Write};

This line brings std::io and std::io::Write into scope.

  
  

**The Glob Operator**

If we want to bring all public items deﬁned in a path into scope, we can specify that path followed by the * glob operator:

use std::collections::*;

This use statement brings all public items deﬁned in std::collections into the current scope. Be careful when using the glob operator! Glob can make it harder to tell what names are in scope and where a name used in your program was deﬁned.

  
  

**Common Collections**

Unlike the built- in array and tuple types, the data these collections point to is stored on the heap, which means the amount of data does not need to be known at compile time and can grow or shrink as the program runs.

• A **vector** allows you to store a variable number of values next to each other.

• A **string** is a collection of characters. We’ve mentioned the String type previously, but in this chapter we’ll talk about it in depth.

• A **hash map** allows you to associate a value with a particular key. It’s a particular implementation of the more general data structure called a map.

**Creating a New Vector**

let v: Vec<i32> = Vec::new();

Note that we added a type annotation here. Because we aren’t inserting any values into this vector, Rust doesn’t know what kind of elements we intend to store. This is an important point. Vectors are implemented using generics;

let v = vec![1, 2, 3];

  
  

  
  

**Updating a Vector**

To create a vector and then add elements to it, we can use the push method, as shown in Listing 8-3.

let mut v = Vec::new();

v.push(5);

v.push(6);

v.push(7);

v.push(8);

**Reading Elements of Vectors**

There are two ways to reference a value stored in a vector: via indexing or using the get method. In the following examples, we’ve annotated the types of the values that are returned from these functions for extra clarity.

Listing 8-4 shows both methods of accessing a value in a vector, with indexing syntax and the get method

let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];

println!("The third element is {}", third);

let third: Option<&i32> = v.get(2);

match third {

Some(third) => println!("The third element is {}", third),

None => println!("There is no third element."),

}

Note a few details here. We use the index value of 2 to get the third element because vectors are indexed by number, starting at zero. Using & and [] gives us a reference to the element at the index value. When we use the get method with the index passed as an argument, we get an Option<&T> that we can use with match .

The reason Rust provides these two ways to reference an element is so you can choose how the program behaves when you try to use an index value outside the range of existing elements. As an example, let’s see what happens when we have a vector of ﬁve elements and then we try to access an element at index 100 with each technique,

let v = vec![1, 2, 3, 4, 5];

let does_not_exist = &v[100];

let does_not_exist = v.get(100);

When we run this code, the ﬁrst [] method will cause the program to panic because it references a nonexistent element. This method is best used when you want your program to crash if there’s an attempt to access an element past the end of the vector.

When the get method is passed an index that is outside the vector, it returns None without panicking. You would use this method if accessing an element beyond the range of the vector may happen occasionally under normal circumstances.

  
  

**Using an Enum to Store Multiple Types**

Vectors can only store values that are the same type.

For example, say we want to get values from a row in a spreadsheet in which some of the columns in the row contain integers, some ﬂoating-point numbers, and some strings. We can deﬁne an enum whose variants will hold the diﬀerent value types, and all the enum variants will be considered the same type: that of the enum. Then we can create a vector to hold that enum and so, ultimately, holds diﬀerent types. We’ve demonstrated this in Listing 8-9.

enum SpreadsheetCell {

Int(i32),

Float(f64),

Text(String),

}

let row = vec![

SpreadsheetCell::Int(3),

SpreadsheetCell::Text(String::from("blue")),

SpreadsheetCell::Float(10.12),

];

Rust needs to know what types will be in the vector at compile time so it knows exactly how much memory on the heap will be needed to store each element. We must also be explicit about what types are allowed in this vector. If Rust allowed a vector to hold any type, there would be a chance that one or more of the types would cause errors with the operations performed on the elements of the vector. Using an enum plus a match expression means that Rust will ensure at compile time that every possible case is handled

If you don’t know the exhaustive set of types a program will get at runtime to store in a vector, the enum technique won’t work. Instead, you can use a trait object,



**What Is a String?**

The String type, which is provided by Rust’s standard library rather than coded into the core language, is a growable, mutable, owned, UTF-8 encoded string type. When Rustaceans refer to “strings” in Rust, they might be referring to either the String or the string slice &str types, not just one of those types. Although this section is largely about String , both types are used heavily in Rust’s standard library, and both String and string slices are UTF-8 encoded.

  
  

**Creating a New String**

Many of the same operations available with Vec<T> are available with String as well, because String is actually implemented as a wrapper around a vector of bytes with some extra guarantees, restrictions, and capabilities.

let mut s = String::new();

This line creates a new empty string called s , which we can then load data into. Often, we’ll have some initial data that we want to start the string with. For that, we use the to_string method, which is available on any type that implements the Display trait,

**Bytes and Scalar Values and Grapheme Clusters! Oh My!**

Another point about UTF-8 is that there are actually three relevant ways to look at strings from Rust’s perspective: as bytes, scalar values, and grapheme clusters (the closest thing to what we would call letters).

If we look at the Hindi word “नम�ते” written in the Devanagari script, it is stored as a vector of u8 values that looks like this:

[224, 164, 168, 224, 164, 174, 224, 164, 184, 224, 165, 141, 224, 164, 164,

224, 165, 135]

That’s 18 bytes and is how computers ultimately store this data. If we look at them as Unicode scalar values, which are what Rust’s char type is, those bytes look like this:

['न', 'म', 'स', '◌्', 'त', '◌े']

There are six char values here, but the fourth and sixth are not letters: they’re diacritics that don’t make sense on their own. Finally, if we look at them as grapheme clusters, we’d get what a person would call the four letters that make up the Hindi word:

["न", "म", "स्", "ते"]

Rust provides diﬀerent ways of interpreting the raw string data that computers store so that each program can choose the interpretation it needs, no matter what human language the data is in.

A ﬁnal reason Rust doesn’t allow us to index into a String to get a character is that indexing operations are expected to always take constant time (O(1)). But it isn’t possible to guarantee that performance with a String , because Rust would have to walk through the contents from the beginning to the index to determine how many valid characters there were.

**Slicing Strings**

Rather than indexing using [ ] with a single number, you can use [] with a range to create a string slice containing particular bytes:

**Methods for Iterating Over Strings**

The best way to operate on pieces of strings is to be explicit about whether you want characters or bytes. For individual Unicode scalar values, use the chars method. Calling chars on “Зд” separates out and returns two values of type char , and you can iterate over the result to access each element:

for c in "Зд".chars() {

println!("{}", c);

}

This code will print the following:

З

д

Alternatively, the bytes method returns each raw byte, which might be appropriate for your

domain:

for b in "Зд".bytes() {

println!("{}", b);

}

This code will print the four bytes that make up this string:

208

151

208

180

But be sure to remember that valid Unicode scalar values may be made up of more than 1 byte. Getting grapheme clusters from strings as with the Devanagari script is complex, so this functionality is not provided by the standard library.

  
  

**Storing Keys with Associated Values in Hash Maps**

The last of our common collections is the hash map. The type HashMap<K, V> stores a mapping of keys of type K to values of type V using a hashing function, which determines how it places these keys and values into memory. Many programming languages support this kind of data structure, but they often use a diﬀerent name, such as hash, map, object, hash table, dictionary, or associative array, just to name a few.

**Updating a Hash Map**

Although the number of key and value pairs is growable, each unique key can only have one value associated with it at a time (but not vice versa: for example, both the Blue team and the Yellow team could have value 10 stored in the scores hash map).

When you want to change the data in a hash map, you have to decide how to handle the case when a key already has a value assigned. You could replace the old value with the new value, completely disregarding the old value. You could keep the old value and ignore the new value, only adding the new value if the key doesn’t already have a value. Or you could combine the old value and the new value. Let’s look at how to do each of these!

  
  

**Adding a Key and Value Only If a Key Isn’t Present**

Hash maps have a special API for this called entry that takes the key you want to check as a parameter. The return value of the entry method is an enum called Entry that represents a value that might or might not exist. Let’s say we want to check whether the key for the Yellow team has a value associated with it. If it doesn’t, we want to insert the value 50, and the same for the Blue team.

use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);

scores.entry(String::from("Yellow")).or_insert(50);

scores.entry(String::from("Blue")).or_insert(50);

println!("{:?}", scores);

  
  

Error Handling

Rust groups errors into two major categories: recoverable and unrecoverable errors. For a recoverable error, such as a ﬁle not found error, we most likely just want to report the problem to the user and retry the operation. Unrecoverable errors are always symptoms of bugs, like trying to access a location beyond the end of an array, and so we want to immediately stop the program.

Most languages don’t distinguish between these two kinds of errors and handle both in the same way, using mechanisms such as exceptions. Rust doesn’t have exceptions. Instead, it has the type Result<T, E> for recoverable errors and the panic! macro that stops execution when the program encounters an unrecoverable error. This chapter covers calling panic! ﬁrst and then talks about returning Result<T, E> values.

  
  

**Unwinding the Stack or Aborting in Response to a Panic**

By default, when a panic occurs, the program starts unwinding, which means Rust walks back up the stack and cleans up the data from each function it encounters. However, this walking back and cleanup is a lot of work. Rust, therefore, allows you to choose the alternative of immediately aborting, which ends the program without cleaning up.

Memory that the program was using will then need to be cleaned up by the operating system. If in your project you need to make the resulting binary as small as possible, you can switch from unwinding to aborting upon a panic by adding **panic = 'abort'** to the appropriate [profile] sections in your Cargo.toml ﬁle. For example, if you want to abort on panic in release mode, add this:

[profile.release]

panic = 'abort'

  
  

**Using a panic! Backtrace**

A backtrace is a list of all the functions that have been called to get to this point. Backtraces in Rust work as they do in other languages: the key to reading the backtrace is to start from the top and read until you see ﬁles you wrote. That’s the spot where the problem originated. The lines above that spot are code that your code has called; the lines below are code that called your code. These before-and-after lines might include core Rust code, standard library code, or crates that you’re using. Let’s try getting a backtrace by setting the RUST_BACKTRACE environment variable to any value except 0. Listing 9-2 shows output similar to what you’ll see.

$ RUST_BACKTRACE=1 cargo run

thread 'main' panicked at 'index out of bounds: the len is 3 but the index is 99',

src/main.rs:4:5 stack backtrace:

0: rust_begin_unwindat

/rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/std/src/panicking.rs:483

1: core::panicking::panic_fmt at

/rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/core/src/panicking.rs:85

2: core::panicking::panic_bounds_check at

/rustc/7eac88abb2e57e752f3302f02be5f3ce3d7adfb4/library/core/src

  
  

**Recoverable Errors with Result**

enum Result<T, E> {

Ok(T),

Err(E),

}

The T and E are generic type parameters:

**Matching on Diﬀerent Errors**

use std::fs::File;

use std::io::ErrorKind;

fn main() {

let greeting_file_result = File::open("hello.txt");

let greeting_file = match greeting_file_result {

Ok(file) => file,

Err(error) => match error.kind() {

ErrorKind::NotFound => match File::create("hello.txt") {

Ok(fc) => fc,

Err(e) => panic!("Problem creating the file: {:?}", e),

},

other_error => {

panic!("Problem opening the file: {:?}", other_error);

}

},

};

}

  
  

**Propagating Errors**

When a function’s implementation calls something that might fail, instead of handling the error within the function itself, you can return the error to the calling code so that it can decide what to do. This is known as propagating the error and gives more control to the calling code, where there might be more information or logic that dictates how the error should be handled than what you have available in the context of your code.

**A Shortcut for Propagating Errors: the ? Operator**

use std::fs::File;

use std::io;

use std::io::Read;

fn read_username_from_file() -> Result<String, io::Error> {

let mut username_file = File::open("hello.txt")?;

let mut username = String::new();

username_file.read_to_string(&mut username)?;

Ok(username)

}

The ? placed after a Result value is deﬁned to work in almost the same way as the match expressions we deﬁned to handle the Result values in Listing 9-6. If the value of the Result is an Ok , the value inside the Ok will get returned from this expression, and the program will continue. If the value is an Err , the Err will be returned from the whole function as if we had used the return keyword so the error value gets propagated to the calling code.

There is a diﬀerence between what the match expression from Listing 9-6 does and what the ? operator does: error values that have the ? operator called on them go through the from function, deﬁned in the From trait in the standard library, which is used to convert values from one type into another. When the ? operator calls the from function, the error type received is converted into the error type deﬁned in the return type of the current function. This is useful when a function returns one error type to represent all the ways a function might fail, even if parts might fail for many diﬀerent reasons.

  
  

**Where The ? Operator Can Be Used**

The ? operator can only be used in functions whose return type is compatible with the value the ? is used on. This is because the ? operator is deﬁned to perform an early return of a value out of the function, in the same manner as the match expression we deﬁned in Listing 9-6. In Listing 9-6, the match was using a Result value, and the early return arm returned an Err(e) value. The return type of the function has to be a Result so that it’s compatible with this return .

This error points out that we’re only allowed to use the ? operator in a function that returns Result , Option , or another type that implements FromResidual .

Note that you can use the ? operator on a Result in a function that returns Result , and you can use the ? operator on an Option in a function that returns Option , but you can’t mix and match. The ? operator won’t automatically convert a Result to an Option or vice versa; in those cases, you can use methods like the ok method on Result or the ok_or method on Option to do the conversion explicitly.

When a main function returns a Result<(), E> , the executable will exit with a value of 0 if main returns Ok(()) and will exit with a nonzero value if main returns an Err value. Executables written in C return integers when they exit: programs that exit successfully return the integer 0 , and programs that error return some integer other than 0 . Rust also returns integers from executables to be compatible with this convention.

The main function may return any types that implement the std::process::Termination trait, which contains a function report that returns an ExitCode Consult the standard library documentation for more information on implementing the Termination trait for your own types.

  
  

**Generic Types, Traits, and Lifetimes**

Every programming language has tools for eﬀectively handling the duplication of concepts. In Rust, one such tool is generics: abstract stand-ins for concrete types or other properties. We can express the behavior of generics or how they relate to other generics without knowing what will be in their place when compiling and running the code.

struct Point<T> {

x: T,

y: T,

}

impl<T> Point<T> {

fn x(&self) -> &T {

&self.x

}

}

  
  

  
  

**Traits: Deﬁning Shared Behavior**

A trait deﬁnes functionality a particular type has and can share with other types. We can use traits to deﬁne shared behavior in an abstract way. We can use trait bounds to specify that a generic type can be any type that has certain behavior.

**Note:** Traits are similar to a feature often called interfaces in other languages, although with some diﬀerences.

pub trait Summary {

fn summarize(&self) -> String;

}

Here, we declare a trait using the trait keyword and then the trait’s name, which is Summary in this case. We’ve also declared the trait as pub so that crates depending on this crate can make use of this trait too, as we’ll see in a few examples. Inside the curly brackets, we declare the method signatures that describe the behaviors of the types that implement this trait, which in this case is fn summarize(&self) -> String .

A trait can have multiple methods in its body: the method signatures are listed one per line and each line ends in a semicolon.

**Implementing a Trait on a Type**

pub struct NewsArticle {

pub headline: String,

pub location: String,

pub author: String,

pub content: String,

}

impl Summary for NewsArticle {

fn summarize(&self) -> String {

format!("{}, by {} ({})", self.headline, self.author, self.location)

}

}

pub struct Tweet {

pub username: String,

pub content: String,

pub reply: bool,

pub retweet: bool,

}

impl Summary for Tweet {

fn summarize(&self) -> String {

format!("{}: {}", self.username, self.content)

}

}

Now that the library has implemented the Summary trait on NewsArticle and Tweet , users of the crate can call the trait methods on instances of NewsArticle and Tweet in the same way we call regular methods. The only diﬀerence is that the user must bring the trait into scope as well as the types.

use aggregator::{Summary, Tweet};

fn main() {

let tweet = Tweet {

username: String::from("horse_ebooks"),

content: String::from(

"of course, as you probably already know, people",

),

reply: false,

retweet: false,

};

println!("1 new tweet: {}", tweet.summarize());

}

Other crates that depend on the aggregator crate can also bring the Summary trait into scope to implement Summary on their own types. One restriction to note is that we can implement a trait on a type only if at least one of the trait or the type is local to our crate. For example, we can implement standard library traits like Display on a custom type like Tweet as part of our aggregator crate functionality, because the type Tweet is local to our aggregator crate. We can also implement Summary on Vec<T> in our aggregator crate, because the trait Summary is local to our aggregator crate.

But we can’t implement external traits on external types. For example, we can’t implement the Display trait on Vec<T> within our aggregator crate, because Display and Vec<T> are both deﬁned in the standard library and aren’t local to our aggregator crate. This restriction is part of a property called coherence, and more speciﬁcally the orphan rule, so named because the parent type is not present. This rule ensures that other people’s code can’t break your code and vice versa. Without the rule, two crates could implement the same trait for the same type, and Rust wouldn’t know which implementation to use.

  
  

**Default Implementations**

Sometimes it’s useful to have default behavior for some or all of the methods in a trait instead of requiring implementations for all methods on every type. Then, as we implement the trait on a particular type, we can keep or override each method’s default behavior.

pub trait Summary {

fn summarize(&self) -> String {

String::from("(Read more...)")

}

}

To use a default implementation to summarize instances of NewsArticle , we specify an empty impl block with

impl Summary for NewsArticle {}

Default implementations can call other methods in the same trait, even if those other methods don’t have a default implementation. In this way, a trait can provide a lot of useful functionality and only require implementors to specify a small part of it. For example, we could deﬁne the Summary trait to have a summarize_author method whose implementation is required, and then deﬁne a summarize method that has a default implementation that calls the summarize_author method:

pub trait Summary {

fn summarize_author(&self) -> String;

fn summarize(&self) -> String {

format!("(Read more from {}...)", self.summarize_author())

}

}

Note that it isn’t possible to call the default implementation from an overriding implementation of that same method.

  
  

  
  

**Traits as Parameters**

pub fn notify(item: &impl Summary) {

println!("Breaking news! {}", item.summarize());

}

Instead of a concrete type for the item parameter, we specify the impl keyword and the trait name. This parameter accepts any type that implements the speciﬁed trait. In the body of notify , we can call any methods on item that come from the Summary trait, such as summarize . We can call notify and pass in any instance of NewsArticle or Tweet . Code that calls the function with any other type, such as a String or an i32 , won’t compile because those types don’t implement Summary .

  
  

**Trait Bound Syntax**

The impl Trait syntax works for straightforward cases but is actually syntax sugar for a longer form known as a trait bound; it looks like this:

pub fn notify<T: Summary>(item: &T) {

println!("Breaking news! {}", item.summarize());

}

This longer form is equivalent to the example in the previous section but is more verbose. We place trait bounds with the declaration of the generic type parameter after a colon and inside angle brackets.

The impl Trait syntax is convenient and makes for more concise code in simple cases, while the fuller trait bound syntax can express more complexity in other cases. For example, we can have two parameters that implement Summary . Doing so with the impl Trait syntax looks like this:

pub fn notify(item1: &impl Summary, item2: &impl Summary) {

Using impl Trait is appropriate if we want this function to allow item1 and item2 to have diﬀerent types (as long as both types implement Summary ). If we want to force both parameters to have the same type, however, we must use a trait bound, like this:

pub fn notify<T: Summary>(item1: &T, item2: &T) {

The generic type T speciﬁed as the type of the item1 and item2 parameters constrains the function such that the concrete type of the value passed as an argument for item1 and item2 must be the same.

  
  

  
  

**Specifying Multiple Trait Bounds with the _+_ Syntax**

We can also specify more than one trait bound. Say we wanted notify to use display formatting as well as summarize on item : we specify in the notify deﬁnition that item must implement both Display and Summary . We can do so using the + syntax:

pub fn notify(item: &(impl Summary + Display)) {

The + syntax is also valid with trait bounds on generic types:

pub fn notify<T: Summary + Display>(item: &T) {

With the two trait bounds speciﬁed, the body of notify can call summarize and use {} to format item .

  
  

**Clearer Trait Bounds with where Clauses**

Using too many trait bounds has its downsides. Each generic has its own trait bounds, so functions with multiple generic type parameters can contain lots of trait bound information between the function’s name and its parameter list, making the function signature hard to read. For this reason, Rust has alternate syntax for specifying trait bounds inside a where clause after the function signature. So instead of writing this:

fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {

we can use a where clause, like this:

fn some_function<T, U>(t: &T, u: &U) -> i32

where T: Display + Clone,

U: Clone + Debug

{

  
  

**Returning Types that Implement Traits**

We can also use the impl Trait syntax in the return position to return a value of some type that implements a trait, as shown here:

fn returns_summarizable() -> impl Summary {

Tweet {

username: String::from("horse_ebooks"),

content: String::from(

"of course, as you probably already know, people",

),

reply: false,

retweet: false,

}

}

The ability to specify a return type only by the trait it implements is especially useful in the context of closures and iterators, which we cover in Chapter 13. Closures and iterators create types that only the compiler knows or types that are very long to specify. The impl Trait syntax lets you concisely specify that a function returns some type that implements the Iterator trait without needing to write out a very long type.

However, you can only use impl Trait if you’re returning a single type.

**Using Trait Bounds to Conditionally Implement Methods**

use std::fmt::Display;

struct Pair<T> {

x: T,

y: T,

}

impl<T> Pair<T> {

fn new(x: T, y: T) -> Self {

Self { x, y }

}

}

impl<T: Display + PartialOrd> Pair<T> {

fn cmp_display(&self) {

if self.x >= self.y {

println!("The largest member is x = {}", self.x);

} else {

println!("The largest member is y = {}", self.y);

}

}

}

  
  

We can also conditionally implement a trait for any type that implements another trait. Implementations of a trait on any type that satisﬁes the trait bounds are called blanket implementations and are extensively used in the Rust standard library.

  
  

**Lifetime Annotation Syntax**

Lifetime annotations don’t change how long any of the references live. Rather, they describe the relationships of the lifetimes of multiple references to each other without aﬀecting the lifetimes. Just as functions can accept any type when the signature speciﬁes a generic type parameter, functions can accept references with any lifetime by specifying a generic lifetime parameter.

Lifetime annotations have a slightly unusual syntax: the names of lifetime parameters must start with an apostrophe ( ' ) and are usually all lowercase and very short, like generic types. Most people use the name 'a for the ﬁrst lifetime annotation. We place lifetime parameter annotations after the & of a reference, using a space to separate the annotation from the reference’s type.

&i32 // a reference

&'a i32 // a reference with an explicit lifetime

&'a mut i32 // a mutable reference with an explicit lifetime

**Lifetime Annotations in Function Signatures**

To use lifetime annotations in function signatures, we need to declare the generic lifetime parameters inside angle brackets between the function name and the parameter list, just as we did with generic type parameters.

fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {

if x.len() > y.len() {

x

} else {

y

}

}

The function signature now tells Rust that for some lifetime 'a , the function takes two parameters, both of which are string slices that live at least as long as lifetime 'a . The function signature also tells Rust that the string slice returned from the function will live at least as long as lifetime 'a . In practice, it means that the lifetime of the reference returned by the longest function is the same as the smaller of the lifetimes of the values referred to by the function arguments.

Remember, when we specify the lifetime parameters in this function signature, we’re not changing the lifetimes of any values passed in or returned. Rather, we’re specifying that the borrow checker should reject any values that don’t adhere to these constraints. Note that the longest function doesn’t need to know exactly how long x and y will live, only that some scope can be substituted for 'a that will satisfy this signature.

When annotating lifetimes in functions, the annotations go in the function signature, not in the function body. The lifetime annotations become part of the contract of the function, much like the types in the signature. Having function signatures contain the lifetime contract means the analysis the Rust compiler does can be simpler. If there’s a problem with the way a function is annotated or the way it is called, the compiler errors can point to the part of our code and the constraints more precisely. If, instead, the Rust compiler made more inferences about what we intended the relationships of the lifetimes to be, the compiler might only be able to point to a use of our code many steps away from the cause of the problem.

When we pass concrete references to longest , the concrete lifetime that is substituted for 'a is the part of the scope of x that overlaps with the scope of y . In other words, the generic lifetime 'a will get the concrete lifetime that is equal to the smaller of the lifetimes of x and y . Because we’ve annotated the returned reference with the same lifetime parameter 'a , the returned reference will also be valid for the length of the smaller of the lifetimes of x and y .

Ultimately, lifetime syntax is about connecting the lifetimes of various parameters and return values of functions. Once they’re connected, Rust has enough information to allow memory-safe operations and disallow operations that would create dangling pointers or otherwise violate memory safety.

  
  

**Lifetime Annotations in Struct Deﬁnitions**

So far, the structs we’ve deﬁned all hold owned types. We can deﬁne structs to hold references, but in that case we would need to add a lifetime annotation on every reference in the struct’s deﬁnition.

struct ImportantExcerpt<'a> {

part: &'a str,

}

This struct has the single ﬁeld part that holds a string slice, which is a reference. As with generic data types, we declare the name of the generic lifetime parameter inside angle brackets after the name of the struct so we can use the lifetime parameter in the body of the struct deﬁnition. This annotation means an instance of ImportantExcerpt can’t outlive the reference it holds in its part ﬁeld.

  
  

  
  

**Lifetime Elision**

After writing a lot of Rust code, the Rust team found that Rust programmers were entering the same lifetime annotations over and over in particular situations. These situations were predictable and followed a few deterministic patterns. The developers programmed these patterns into the compiler’s code so the borrow checker could infer the lifetimes in these situations and wouldn’t need explicit annotations.

This piece of Rust history is relevant because it’s possible that more deterministic patterns will emerge and be added to the compiler. In the future, even fewer lifetime annotations might be required.

The patterns programmed into Rust’s analysis of references are called the lifetime elision rules. These aren’t rules for programmers to follow; they’re a set of particular cases that the compiler will consider, and if your code ﬁts these cases, you don’t need to write the lifetimes explicitly.

Lifetimes on function or method parameters are called input lifetimes, and lifetimes on return values are called output lifetimes.

The compiler uses three rules to ﬁgure out the lifetimes of the references when there aren’t explicit annotations. The ﬁrst rule applies to input lifetimes, and the second and third rules apply to output lifetimes. If the compiler gets to the end of the three rules and there are still references for which it can’t ﬁgure out lifetimes, the compiler will stop with an error.

**The ﬁrst rule** is that the compiler assigns a lifetime parameter to each parameter that’s a reference. In other words, a function with one parameter gets one lifetime parameter: fn foo<'a>(x: &'a i32) ; a function with two parameters gets two separate lifetime parameters: fn foo<'a, 'b>(x: &'a i32, y: &'b i32) ; and so on.

**The second rule** is that, if there is exactly one input lifetime parameter, that lifetime is assigned to all output lifetime parameters: fn foo<'a>(x: &'a i32) -> &'a i32 .

**The third rule i**s that, if there are multiple input lifetime parameters, but one of them is &self or &mut self because this is a method, the lifetime of self is assigned to all output lifetime parameters. This third rule makes methods much nicer to read and write because fewer symbols are necessary.

Because the third rule really only applies in method signatures, we’ll look at lifetimes in that context next to see why the third rule means we don’t have to annotate lifetimes in method signatures very often.

  
  

**Lifetime Annotations in Method Deﬁnitions**

Lifetime names for struct ﬁelds always need to be declared after the impl keyword and then used after the struct’s name, because those lifetimes are part of the struct’s type.

In method signatures inside the impl block, references might be tied to the lifetime of references in the struct’s ﬁelds, or they might be independent. In addition, the lifetime elision rules often make it so that lifetime annotations aren’t necessary in method signatures.

impl<'a> ImportantExcerpt<'a> {

fn level(&self) -> i32 {

3

}

}

**The Static Lifetime**

One special lifetime we need to discuss is 'static , which denotes that the aﬀected reference can live for the entire duration of the program.

let s: &'static str = "I have a static lifetime.";

The text of this string is stored directly in the program’s binary, which is always available. Therefore, the lifetime of all string literals is 'static .

You might see suggestions to use the 'static lifetime in error messages. But before specifying 'static as the lifetime for a reference, think about whether the reference you have actually lives the entire lifetime of your program or not, and whether you want it to. Most of the time, an error message suggesting the 'static lifetime results from attempting to create a dangling reference or a mismatch of the available lifetimes. In such cases, the solution is ﬁxing those problems, not specifying the 'static lifetime.

**Generic Type Parameters, Trait Bounds, and Lifetimes Together**

use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(

x: &'a str,

y: &'a str,

ann: T,

) -> &'a str

where

T: Display,

{

println!("Announcement! {}", ann);

if x.len() > y.len() {

x

} else {

y

}

}

  
  

Checking for Panics with should_panic

We do this by adding the attribute should_panic to our test function. The test passes if the code inside the function panics; the test fails if the code inside the function doesn’t panic.

pub struct Guess {

value: i32,

}

impl Guess {

pub fn new(value: i32) -> Guess {

if value < 1 || value > 100 {

panic!("Guess value must be between 1 and 100, got {}.", value);

}

Guess { value }

}

}

#[cfg(test)]

mod tests {

use super::*;

  
  

#[test]

#[should_panic]

fn greater_than_100() {

Guess::new(200);

}

}

Tests that use should_panic can be imprecise. A should_panic test would pass even if the test panics for a diﬀerent reason from the one we were expecting. To make should_panic tests more precise, we can add an optional expected parameter to the should_panic attribute. The test harness will make sure that the failure message contains the provided text. For example, consider the modiﬁed code for Guess in Listing 11-9 where the new function panics with diﬀerent messages depending on whether the value is too small or too large.

// --snip--

#[cfg(test)]

mod tests {

use super::*;

  
  

#[test]

#[should_panic(expected = "less than or equal to 100")]

fn greater_than_100() {

Guess::new(200);

}

}

**Using Result<T, E> in Tests**

#[cfg(test)]

mod tests {

#[test]

fn it_works() -> Result<(), String> {

if 2 + 2 == 4 {

Ok(())

} else {

Err(String::from("two plus two does not equal four"))

}

}

}

Writing tests so they return a Result<T, E> enables you to use the question mark operator in the body of tests, which can be a convenient way to write tests that should fail if any operation within them returns an Err variant.

You can’t use the #[should_panic] annotation on tests that use Result<T, E> . To assert that an operation returns an Err variant, don’t use the question mark operator on the Result<T, E> value. Instead, use assert!(value.is_err()) .

  
  

**Running Tests in Parallel or Consecutively**

When you run multiple tests, by default they run in parallel using threads, meaning they ﬁnish running faster and you get feedback quicker. Because the tests are running at the same time, you must make sure your tests don’t depend on each other or on any shared state, including a shared environment, such as the current working directory or environment variables.

If you don’t want to run the tests in parallel or if you want more ﬁne-grained control over the number of threads used, you can send the --test-threads ﬂag and the number of threads you want to use to the test binary. Take a look at the following example:

$ cargo test -- --test-threads=1

We set the number of test threads to 1 , telling the program not to use any parallelism. Running the tests using one thread will take longer than running them in parallel, but the tests won’t interfere with each other if they share state.

**Showing Function Output**

By default, if a test passes, Rust’s test library captures anything printed to standard output. For example, if we call println! in a test and the test passes, we won’t see the println! output in the terminal; we’ll see only the line that indicates the test passed. If a test fails, we’ll see whatever was printed to standard output with the rest of the failure message.

If we want to see printed values for passing tests as well, we can tell Rust to also show the output of successful tests with --show-output .

$ cargo test -- --show-output

**Running Single Tests**

We can pass the name of any test function to cargo test to run only that test:

$ cargo test one_hundred

**Filtering to Run Multiple Tests**

We can specify part of a test name, and any test whose name matches that value will be run. For example, because two of our tests’ names contain add , we can run those two by running cargo test add :

$ cargo test add

**Ignoring Some Tests Unless Speciﬁcally Requested**

Sometimes a few speciﬁc tests can be very time-consuming to execute, so you might want to exclude them during most runs of cargo test . Rather than listing as arguments all tests you do want to run, you can instead annotate the time-consuming tests using the ignore attribute to exclude them, as shown here:

#[test]

fn it_works() {

assert_eq!(2 + 2, 4);

}

#[test]

#[ignore]

fn expensive_test() {

// code that takes an hour to run

}

The expensive_test function is listed as ignored . If we want to run only the ignored tests, we canuse cargo test -- --ignored :

$ cargo test -- --ignored

If you want to run all tests whether they’re ignored or not, you can run

$ cargo test -- --include-ignored

  
  

**Test Organization**

As mentioned at the start of the chapter, testing is a complex discipline, and diﬀerent people use diﬀerent terminology and organization. The Rust community thinks about tests in terms of two main categories: unit tests and integration tests. Unit tests are small and more focused, testing one module in isolation at a time, and can test private interfaces. Integration tests are entirely external to your library and use your code in the same way any other external code would, using only the public interface and potentially exercising multiple modules per test.

**Unit Tests**

The purpose of unit tests is to test each unit of code in isolation from the rest of the code to quickly pinpoint where code is and isn’t working as expected. You’ll put unit tests in the src directory in each ﬁle with the code that they’re testing. The convention is to create a module named tests in each ﬁle to contain the test functions and to annotate the module with cfg(test)

**The Tests Module and #[cfg(test)]**

The #[cfg(test)] annotation on the tests module tells Rust to compile and run the test code only when you run cargo test , not when you run cargo build . This saves compile time when you only want to build the library and saves space in the resulting compiled artifact because the tests are not included. You’ll see that because integration tests go in a diﬀerent directory, they don’t need the #[cfg(test)] annotation. However, because unit tests go in the same ﬁles as the code, you’ll use #[cfg(test)] to specify that they shouldn’t be included in the compiled result.

**Integration Tests**

In Rust, integration tests are entirely external to your library. They use your library in the same way any other code would, which means they can only call functions that are part of your library’s public API.

**The tests Directory**

We create a tests directory at the top level of our project directory, next to src. Cargo knows to look for integration test ﬁles in this directory. We can then make as many test ﬁles as we want, and Cargo will compile each of the ﬁles as an individual crate.

Each ﬁle in the tests directory is a separate crate, so we need to bring our library into each test crate’s scope. For that reason we add use adder at the top of the code, which we didn’t need in the unit tests.

We don’t need to annotate any code in tests/integration_test.rs with #[cfg(test)] . Cargo treats the tests directory specially and compiles ﬁles in this directory only when we run cargo test .

  
  

**Integration Tests for Binary Crates**

If our project is a binary crate that only contains a src/main.rs ﬁle and doesn’t have a src/lib.rs ﬁle, we can’t create integration tests in the tests directory and bring functions deﬁned in the src/main.rs ﬁleminto scope with a use statement. Only library crates expose functions that other crates can use; binary crates are meant to be run on their own.

This is one of the reasons Rust projects that provide a binary have a straightforward src/main.rs ﬁle that calls logic that lives in the src/lib.rs ﬁle. Using that structure, integration tests can test the library crate with use to make the important functionality available. If the important functionality works, the small amount of code in the src/main.rs ﬁle will work as well, and that small amount of code doesn’t need to be tested.

  
  

**Closures: Anonymous Functions that Capture Their Environment**

Rust’s closures are anonymous functions you can save in a variable or pass as arguments to other functions. You can create the closure in one place and then call the closure elsewhere to evaluate it in a diﬀerent context. Unlike functions, closures can capture values from the scope in which they’re deﬁned.

  
  

  
  

**Closure Type Inference and Annotation**

There are more diﬀerences between functions and closures. Closures don’t usually require you to annotate the types of the parameters or the return value like fn functions do. Type annotations are required on functions because the types are part of an explicit interface exposed to your users. Deﬁning this interface rigidly is important for ensuring that everyone agrees on what types of values a function uses and returns. Closures, on the other hand, aren’t used in an exposed interface like this: they’re stored in variables and used without naming them and exposing them to users of our library.

Closures are typically short and relevant only within a narrow context rather than in any arbitrary scenario. Within these limited contexts, the compiler can infer the types of the parameters and the return type, similar to how it’s able to infer the types of most variables (there are rare cases where the compiler needs closure type annotations too).

let expensive_closure = |num: u32| -> u32 {

println!("calculating slowly...");

thread::sleep(Duration::from_secs(2));

num

};

  
  

let example_closure = |x| x;

let s = example_closure(String::from("hello"));

let n = example_closure(5);

The ﬁrst time we call example_closure with the String value, the compiler infers the type of x

and the return type of the closure to be String . Those types are then locked into the closure in example_closure , and we get a type error when we next try to use a diﬀerent type with the same closure.

**Capturing References or Moving Ownership**

Closures can capture values from their environment in three ways, which directly map to the three ways a function can take a parameter: borrowing immutably, borrowing mutably, and taking ownership. The closure will decide which of these to use based on what the body of the function does with the captured values.

If you want to force the closure to take ownership of the values it uses in the environment even though the body of the closure doesn’t strictly need ownership, you can use the move keyword before the parameter list. This technique is mostly useful when passing a closure to a new thread to move the data so that it’s owned by the new thread.

  
  

**Moving Captured Values Out of Closures and the Fn Traits**

Once a closure has captured a reference or captured ownership of a value where the closure is deﬁned (thus aﬀecting what, if anything, is moved into the closure), the code in the body of the closure deﬁnes what happens to the references or values when the closure is evaluated later (thus aﬀecting what, if anything, is moved out of the closure). A closure body can do any of the following: move a captured value out of the closure, mutate the captured value, neither move nor mutate the value, or capture nothing from the environment to begin with.

The way a closure captures and handles values from the environment aﬀects which traits the closure implements, and traits are how functions and structs can specify what kinds of closures they can use. Closures will automatically implement one, two, or all three of these Fn traits, in an additive fashion:

1. **FnOnce** applies to closures that can be called at least once. All closures implement at least this trait, because all closures can be called. A closure that moves captured values out of its body will only implement FnOnce and none of the other Fn traits, because it can only be called once.

2. **FnMut** applies to closures that don’t move captured values out of their body, but that might mutate the captured values. These closures can be called more than once.

3. **Fn** applies to closures that don’t move captured values out of their body and that don’t mutate captured values, as well as closures that capture nothing from their environment. These closures can be called more than once without mutating their environment, which is important in cases such as calling a closure multiple times concurrently.

  
  

**The Iterator Trait and the next Method**

The iter method produces an iterator over immutable references. If we want to create an iterator that takes ownership of v1 and returns owned values, we can call into_iter instead of iter . Similarly, if we want to iterate over mutable references, we can call iter_mut instead of iter .

  
  

**Methods that Consume the Iterator**

Methods that call next are called **consuming adaptors**, because calling them uses up the iterator. One example is the sum method, which takes ownership of the iterator and iterates through the items by repeatedly calling next , thus consuming the iterator. As it iterates through, it adds each item to a running total and returns the total when iteration is complete.

fn iterator_sum() {

let v1 = vec![1, 2, 3];

let v1_iter = v1.iter();

let total: i32 = v1_iter.sum();

assert_eq!(total, 6);

}

We aren’t allowed to use v1_iter after the call to sum because sum takes ownership of the iterator we call it on.

  
  

**Methods that Produce Other Iterators**

**Iterator adaptors** are methods deﬁned on the Iterator trait that don’t consume the iterator. Instead, they produce diﬀerent iterators by changing some aspect of the original iterator.

  
  

**Making Useful Documentation Comments**

**Commonly Used Sections**

We used the # Examples Markdown heading

• **Panics:** The scenarios in which the function being documented could panic. Callers of the function who don’t want their programs to panic should make sure they don’t call the function in these situations.

• **Errors:** If the function returns a Result , describing the kinds of errors that might occur and what conditions might cause those errors to be returned can be helpful to callers so they can write code to handle the diﬀerent kinds of errors in diﬀerent ways.

• **Safety:** If the function is unsafe to call (we discuss unsafety in Chapter 19), there should be a section explaining why the function is unsafe and covering the invariants that the function expects callers to uphold.

**Commenting Contained Items**

The style of doc comment //! adds documentation to the item that contains the comments rather than to the items following the comments. We typically use these doc comments inside the crate root ﬁle (src/lib.rs by convention) or inside a module to document the crate or the module as a whole.

For example, to add documentation that describes the purpose of the my_crate crate that contains the add_one function, we add documentation comments that start with //! to the beginning of the

//! # My Crate

//!

//! `my_crate` is a collection of utilities to make performing certain

//! calculations more convenient.

  
  

/// Adds one to the number given.

// --snip--

  
  

Notice there isn’t any code after the last line that begins with //! . Because we started the comments with //! instead of /// , we’re documenting the item that contains this comment rather than an item that follows this comment. In this case, that item is the src/lib.rs ﬁle, which is the crate root. These comments describe the entire crate.

When we run cargo doc --open , these comments will display on the front page of the documentation for my_crate above the list of public items in the crate,

  
  

  
  

**Smart Pointers**

Smart pointers are usually implemented using structs. Unlike an ordinary struct, smart pointers implement the **Deref** and **Drop** traits. The Deref trait allows an instance of the smart pointer struct to behave like a reference so you can write your code to work with either references or smart pointers. The Drop trait allows you to customize the code that's run when an instance of the smart pointer goes out of scope.

• **Box<T>** for allocating values on the heap

• **Rc<T>** , a reference counting type that enables multiple ownership

• **Ref<T>** and **RefMut<T>** , accessed through **RefCell<T>** , a type that enforces the borrowing rules at runtime instead of compile time

  
  

**Using Box<T> to Point to Data on the Heap**

The most straightforward smart pointer is a box, whose type is written Box<T> . Boxes allow you to store data on the heap rather than the stack. What remains on the stack is the pointer to the heap data.

Boxes don’t have performance overhead, other than storing their data on the heap instead of on the stack. But they don’t have many extra capabilities either. You’ll use them most often in these situations:

• When you have a type whose size can’t be known at compile time and you want to use a value of that type in a context that requires an exact size

• When you have a large amount of data and you want to transfer ownership but ensure the data won’t be copied when you do so

• When you want to own a value and you care only that it’s a type that implements a particular trait rather than being of a speciﬁc type

The Box<T> type is a smart pointer because it implements the **Deref** trait, which allows Box<T> values to be treated like references. When a Box<T> value goes out of scope, the heap data that the box is pointing to is cleaned up as well because of the **Drop** trait implementation.

**Treating Smart Pointers Like Regular References with the _Deref_ Trait**

Implementing the Deref trait allows you to customize the behavior of the dereference operator * (not to be confused with the multiplication or glob operator). By implementing Deref in such a way that a smart pointer can be treated like a regular reference, you can write code that operates on references and use that code with smart pointers too.

  
  

**Implicit Deref Coercions with Functions and Methods**

Deref coercion converts a reference to a type that implements the Deref trait into a reference to another type.

Deref coercion is a convenience Rust performs on arguments to functions and methods, and works only on types that implement the Deref trait. It happens automatically when we pass a reference to a particular type’s value as an argument to a function or method that doesn’t match the parameter type in the function or method deﬁnition. A sequence of calls to the deref method converts the type we provided into the type the parameter needs.

Deref coercion was added to Rust so that programmers writing function and method calls don’t need to add as many explicit references and dereferences with & and * . The deref coercion feature also lets us write more code that can work for either references or smart pointers.

When the Deref trait is deﬁned for the types involved, Rust will analyze the types and use Deref::deref as many times as necessary to get a reference to match the parameter’s type. The number of times that Deref::deref needs to be inserted is resolved at compile time, so there is no runtime penalty for taking advantage of deref coercion!

  
  

**How Deref Coercion Interacts with Mutability**

Similar to how you use the Deref trait to override the * operator on immutable references, you can use the DerefMut trait to override the * operator on mutable references.

Rust does deref coercion when it ﬁnds types and trait implementations in three cases:

• From &T to &U when T: Deref<Target=U>

• From &mut T to &mut U when T: DerefMut<Target=U>

• From &mut T to &U when T: Deref<Target=U>

The ﬁrst two cases are the same as each other except that the second implements mutability. The ﬁrst case states that if you have a &T , and T implements Deref to some type U , you can get a &U transparently. The second case states that the same deref coercion happens for mutable references.

The third case is trickier: Rust will also coerce a mutable reference to an immutable one. But the reverse is not possible: immutable references will never coerce to mutable references. Because of the borrowing rules, if you have a mutable reference, that mutable reference must be the only reference to that data (otherwise, the program wouldn’t compile). Converting one mutable reference to one immutable reference will never break the borrowing rules. Converting an immutable reference to a mutable reference would require that the initial immutable reference is the only immutable reference to that data, but the borrowing rules don’t guarantee that. Therefore, Rust can’t make the assumption that converting an immutable reference to a mutable reference is possible.

  
  

**Running Code on Cleanup with the Drop Trait**

Drop , which lets you customize what happens when a value is about to go out of scope. You can provide an implementation for the Drop trait on any type, and that code can be used to release resources like ﬁles or network connections.

You specify the code to run when a value goes out of scope by implementing the Drop trait. The Drop trait requires you to implement one method named drop that takes a mutable reference to self .

Rust automatically called drop for us when our instances went out of scope, calling the code we speciﬁed. Variables are dropped in the reverse order of their creation, so d was dropped before c .

**Dropping a Value Early with std::mem::drop**

Unfortunately, it’s not straightforward to disable the automatic drop functionality. Disabling drop isn’t usually necessary; the whole point of the Drop trait is that it’s taken care of automatically. Occasionally, however, you might want to clean up a value early. One example is when using smart pointers that manage locks: you might want to force the drop method that releases the lock so that other code in the same scope can acquire the lock. Rust doesn’t let you call the Drop trait’s drop method manually; instead you have to call the std::mem::drop function provided by the standard library if you want to force a value to be dropped before the end of its scope.

A destructor is analogous to a constructor, which creates an instance. The drop function in Rust is one particular destructor.

Rust doesn’t let us call drop explicitly because Rust would still automatically call drop on the value at the end of main . This would cause a double free error because Rust would be trying to clean up the same value twice.

The std::mem::drop function is diﬀerent from the drop method in the Drop trait. We call it by passing as an argument the value we want to force drop. The function is in the prelude, so we can modify main

fn main() {

let c = CustomSmartPointer {

data: String::from("some data"),

};

println!("CustomSmartPointer created.");

drop(c);

println!("CustomSmartPointer dropped before the end of main.");

}

**Rc<T>, the Reference Counted Smart Pointer**

You have to enable multiple ownership explicitly by using the Rust type Rc<T> , which is an abbreviation for reference counting. The Rc<T> type keeps track of the number of references to a value to determine whether or not the value is still in use. If there are zero references to a value, the value can be cleaned up without any references becoming invalid.

We use the Rc<T> type when we want to allocate some data on the heap for multiple parts of our program to read and we can’t determine at compile time which part will ﬁnish using the data last. If we knew which part would ﬁnish last, we could just make that part the data’s owner, and the normal ownership rules enforced at compile time would take eﬀect.

**RefCell<T> and the Interior Mutability Pattern**

Interior mutability is a design pattern in Rust that allows you to mutate data even when there are immutable references to that data; normally, this action is disallowed by the borrowing rules. To mutate data, the pattern uses unsafe code inside a data structure to bend Rust’s usual rules that govern mutation and borrowing. Unsafe code indicates to the compiler that we’re checking the rules manually instead of relying on the compiler to check them for us;

We can use types that use the interior mutability pattern only when we can ensure that the borrowing rules will be followed at runtime, even though the compiler can’t guarantee that. The unsafe code involved is then wrapped in a safe API, and the outer type is still immutable.

**Enforcing Borrowing Rules at Runtime with RefCell<T>**

Unlike Rc<T> , the RefCell<T> type represents single ownership over the data it holds.

With references and Box<T> , the borrowing rules’ invariants are enforced at compile time. With RefCell<T> , these invariants are enforced at runtime. With references, if you break these rules, you’ll get a compiler error. With RefCell<T> , if you break these rules, your program will panic and exit.

  
  

Here is a recap of the reasons to choose Box<T> , Rc<T> , or RefCell<T> :

• Rc<T> enables multiple owners of the same data; Box<T> and RefCell<T> have single owners.

• Box<T> allows immutable or mutable borrows checked at compile time; Rc<T> allows only immutable borrows checked at compile time; RefCell<T> allows immutable or mutable borrows checked at runtime.

• Because RefCell<T> allows mutable borrows checked at runtime, you can mutate the value inside the RefCell<T> even when the RefCell<T> is immutable.

Mutating the value inside an immutable value is the interior mutability pattern.

**Keeping Track of Borrows at Runtime with RefCell<T>**

When creating immutable and mutable references, we use the & and &mut syntax, respectively. With RefCell<T> , we use the borrow and borrow_mut methods, which are part of the safe API that belongs to RefCell<T> . The borrow method returns the smart pointer type Ref<T> , and borrow_mut returns the smart pointer type RefMut<T> . Both types implement Deref , so we can treat them like regular references.

The RefCell<T> keeps track of how many Ref<T> and RefMut<T> smart pointers are currently active. Every time we call borrow , the RefCell<T> increases its count of how many immutable borrows are active. When a Ref<T> value goes out of scope, the count of immutable borrows goes down by one. Just like the compile-time borrowing rules, RefCell<T> lets us have many immutable borrows or one mutable borrow at any point in time.

**Reference Cycles Can Leak Memory**

Rust’s memory safety guarantees make it diﬃcult, but not impossible, to accidentally create memory that is never cleaned up (known as a memory leak). Preventing memory leaks entirely is not one of Rust’s guarantees, meaning memory leaks are memory safe in Rust. We can see that Rust allows memory leaks by using Rc<T> and RefCell<T> : it’s possible to create references where items refer to each other in a cycle. This creates memory leaks because the reference count of each item in the cycle will never reach 0, and the values will never be dropped.

  
  

  
  

  
  

**Characteristics of Object-Oriented Languages**

There is no consensus in the programming community about what features a language must have to be considered object-oriented. Rust is inﬂuenced by many programming paradigms, including OOP; for example, we explored the features that came from functional programming in Chapter 13. Arguably, OOP languages share certain common characteristics, namely objects, encapsulation, and inheritance. Let’s look at what each of those characteristics means and whether Rust supports it.

**Encapsulation that Hides Implementation Details**

Another aspect commonly associated with OOP is the idea of encapsulation, which means that the implementation details of an object aren’t accessible to code using that object. Therefore, the only way to interact with an object is through its public API; code using the object shouldn’t be able to reach into the object’s internals and change data or behavior directly. This enables the programmer to change and refactor an object’s internals without needing to change the code that uses the object.

We discussed how to control encapsulation in Chapter 7: we can use the **pub** keyword to decide which modules, types, functions, and methods in our code should be public, and by default everything else is private. For example, we can deﬁne a struct AveragedCollection that has a ﬁeld

containing a vector of i32 values. The struct can also have a ﬁeld that contains the average of the values in the vector, meaning the average doesn’t have to be computed on demand whenever anyone needs it. In other words, AveragedCollection will cache the calculated average for us.

pub struct AveragedCollection {

list: Vec<i32>,

average: f64,

}

The struct is marked pub so that other code can use it, but the ﬁelds within the struct remain private. This is important in this case because we want to ensure that whenever a value is added or removed from the list, the average is also updated. We do this by implementing add , remove , and average methods on the struct, as shown in Listing 17-2:

If encapsulation is a required aspect for a language to be considered object-oriented, then Rust meets that requirement. The option to use pub or not for diﬀerent parts of code enables encapsulation of implementation details.

  
  

  
  

  
  

**Inheritance as a Type System and as Code Sharing**

Inheritance is a mechanism whereby an object can inherit elements from another object’s deﬁnition, thus gaining the parent object’s data and behavior without you having to deﬁne them again.

If a language must have inheritance to be an object-oriented language, then Rust is not one. There is no way to deﬁne a struct that inherits the parent struct’s ﬁelds and method implementations without using a macro.

However, if you’re used to having inheritance in your programming toolbox, you can use other solutions in Rust, depending on your reason for reaching for inheritance in the ﬁrst place.

You would choose inheritance for two main reasons. One is for reuse of code: you can implement particular behavior for one type, and inheritance enables you to reuse that implementation for a diﬀerent type. You can do this in a limited way in Rust code using default **trait** method implementations,

The other reason to use inheritance relates to the type system: to enable a child type to be used in the same places as the parent type. This is also called **polymorphism**, which means that you can substitute multiple objects for each other at runtime if they share certain characteristics.

**Polymorphism**

To many people, polymorphism is synonymous with inheritance. But it’s actually a more general concept that refers to code that can work with data of multiple types. For inheritance, those types are generally subclasses. Rust instead uses generics to abstract over diﬀerent possible types and trait bounds to impose constraints on what those types must provide. This is sometimes called **bounded parametric polymorphism.**

  
  

**Conditional if let Expressions**

In Chapter 6 we discussed how to use if let expressions mainly as a shorter way to write the equivalent of a match that only matches one case. Optionally, if let can have a corresponding else containing code to run if the pattern in the if let doesn’t match.

Listing 18-1 shows that it’s also possible to mix and match if let , else if , and else if let expressions. Doing so gives us more ﬂexibility than a match expression in which we can express only one value to compare with the patterns. Also, Rust doesn't require that the conditions in a series of if let , else if , else if let arms relate to each other.

fn main() {

let favorite_color: Option<&str> = None;

let is_tuesday = false;

let age: Result<u8, _> = "34".parse();

if let Some(color) = favorite_color {

println!("Using your favorite color, {color}, as the background");

} else if is_tuesday {

println!("Tuesday is green day!");

} else if let Ok(age) = age {

if age > 30 {

println!("Using purple as the background color");

} else {

println!("Using orange as the background color");

}

} else {

println!("Using blue as the background color");

}

}

  
  

**while let Conditional Loops**

Similar in construction to if let , the while let conditional loop allows a while loop to run for as long as a pattern continues to match. In Listing 18-2 we code a while let loop that uses a vector as a stack and prints the values in the vector in the opposite order in which they were pushed.

let mut stack = Vec::new();

stack.push(1);

stack.push(2);

stack.push(3);

while let Some(top) = stack.pop() {

println!("{}", top);

}

**let Statements**

Prior to this chapter, we had only explicitly discussed using patterns with match and if let , but in fact, we’ve used patterns in other places as well, including in let statements. For example, consider this straightforward variable assignment with let :

let x = 5;

Every time you've used a let statement like this you've been using patterns, although you might not have realized it! More formally, a let statement looks like this:

let PATTERN = EXPRESSION;

**Refutability: Whether a Pattern Might Fail to Match**

Patterns come in two forms: refutable and irrefutable. Patterns that will match for any possible value passed are irrefutable. An example would be x in the statement let x = 5; because x matches anything and therefore cannot fail to match. Patterns that can fail to match for some possible value are refutable. An example would be Some(x) in the expression if let Some(x) = a_value because if the value in the a_value variable is None rather than Some , the Some(x) pattern will not match.

Function parameters, let statements, and for loops can only accept irrefutable patterns, because the program cannot do anything meaningful when values don’t match. The if let and while let expressions accept refutable and irrefutable patterns, but the compiler warns against irrefutable patterns because by deﬁnition they’re intended to handle possible failure: the functionality of a conditional is in its ability to perform diﬀerently depending on success or failure.

**Multiple Patterns**

In match expressions, you can match multiple patterns using the **|** syntax, which is the pattern or operator. For example, in the following code we match the value of x against the match arms, the ﬁrst of which has an or option, meaning if the value of x matches either of the values in that arm, that arm’s code will run:

let x = 1;

match x {

1 | 2 => println!("one or two"),

3 => println!("three"),

_ => println!("anything"),

}

This code prints one or two .

  
  

**Matching Ranges of Values with ..=**

The ..= syntax allows us to match to an inclusive range of values. In the following code, when a pattern matches any of the values within the given range, that arm will execute:

let x = 5;

match x {

1..=5 => println!("one through five"),

_ => println!("something else"),

}

If x is 1, 2, 3, 4, or 5, the ﬁrst arm will match. This syntax is more convenient for multiple match values than using the | operator to express the same idea; if we were to use | we would have to specify 1 | 2 | 3 | 4 | 5 . Specifying a range is much shorter, especially if we want to match, say, any number between 1 and 1,000!

  
  

**Destructuring to Break Apart Values\**

**Destructuring Structs**

struct Point {

x: i32,

y: i32,

}

fn main() {

let p = Point { x: 0, y: 7 };

let Point { x: a, y: b } = p;

assert_eq!(0, a);

assert_eq!(7, b);

}

------or------

struct Point {

x: i32,

y: i32,

}

fn main() {

let p = Point { x: 0, y: 7 };

let Point { x, y } = p;

assert_eq!(0, x);

assert_eq!(7, y);

}

  
  

We can also destructure with literal values as part of the struct pattern rather than creating variables for all the ﬁelds. Doing so allows us to test some of the ﬁelds for particular values while creating variables to destructure the other ﬁelds.

In Listing 18-14, we have a match expression that separates Point values into three cases: points that lie directly on the x axis (which is true when y = 0 ), on the y axis ( x = 0 ), or neither.

fn main() {

let p = Point { x: 0, y: 7 };

match p {

Point { x, y: 0 } => println!("On the x axis at {}", x),

Point { x: 0, y } => println!("On the y axis at {}", y),

Point { x, y } => println!("On neither axis: ({}, {})", x, y),

}

}

  
  

The ﬁrst arm will match any point that lies on the x axis by specifying that the y ﬁeld matches if its value matches the literal 0 . The pattern still creates an x variable that we can use in the code for this arm.

Similarly, the second arm matches any point on the y axis by specifying that the x ﬁeld matches if its value is 0 and creates a variable y for the value of the y ﬁeld. The third arm doesn’t specify any literals, so it matches any other Point and creates variables for both the x and y ﬁelds.

In this example, the value p matches the second arm by virtue of x containing a 0, so this code will print On the y axis at 7 . Remember that a match expression stops checking arms once it has found the ﬁrst matching pattern, so even though Point { x: 0, y: 0} is on the x axis and the y axis, this code would only print On the x axis at 0 .

  
  

  
  

**Ignoring Remaining Parts of a Value with ..**

With values that have many parts, we can use the .. syntax to use speciﬁc parts and ignore the rest, avoiding the need to list underscores for each ignored value. The .. pattern ignores any parts of a value that we haven’t explicitly matched in the rest of the pattern. In Listing 18-23, we have a Point struct that holds a coordinate in three-dimensional space. In the match expression, we want to operate only on the x coordinate and ignore the values in the y and z ﬁelds.

struct Point {

x: i32,

y: i32,

z: i32,

}

let origin = Point { x: 0, y: 0, z: 0 };

match origin {

Point { x, .. } => println!("x is {}", x),

}

We list the x value and then just include the .. pattern. This is quicker than having to list y: _ and z: _ , particularly when we’re working with structs that have lots of ﬁelds in situations where onlyone or two ﬁelds are relevant.

  
  

**Extra Conditionals with Match Guards**

A match guard is an additional if condition, speciﬁed after the pattern in a match arm, that must also match for that arm to be chosen. Match guards are useful for expressing more complex ideas than a pattern alone allows.

The condition can use variables created in the pattern. Listing 18-26 shows a match where the ﬁrst arm has the pattern Some(x) and also has a match guard of if x % 2 == 0 (which will be true if the number is even).

let num = Some(4);

match num {

Some(x) if x % 2 == 0 => println!("The number {} is even", x),

Some(x) => println!("The number {} is odd", x),

None => (),

}

This example will print The number 4 is even . When num is compared to the pattern in the ﬁrst arm, it matches, because Some(4) matches Some(x) . Then the match guard checks whether the remainder of dividing x by 2 is equal to 0, and because it is, the ﬁrst arm is selected.

If num had been Some(5) instead, the match guard in the ﬁrst arm would have been false because the remainder of 5 divided by 2 is 1, which is not equal to 0. Rust would then go to the second arm, which would match because the second arm doesn’t have a match guard and therefore matches any Some variant. There is no way to express the if x % 2 == 0 condition within a pattern, so the match guard gives us the ability to express this logic. The downside of this additional expressiveness is that the compiler doesn't try to check for exhaustiveness when match guard expressions are involved.

fn main() {

let x = Some(5);

let y = 10;

match x {

Some(50) => println!("Got 50"),

Some(n) if n == y => println!("Matched, n = {n}"),

_ => println!("Default case, x = {:?}", x),

}

println!("at the end: x = {:?}, y = {y}", x);

}

This code will now print Default case, x = Some(5) . The pattern in the second match arm doesn’t introduce a new variable y that would shadow the outer y , meaning we can use the outer y in the match guard. Instead of specifying the pattern as Some(y) , which would have shadowed the outer y , we specify Some(n) . This creates a new variable n that doesn’t shadow anything because there is no n variable outside the match .

  
  

**@ Bindings**

The at operator @ lets us create a variable that holds a value at the same time as we’re testing that value for a pattern match. In Listing 18-29, we want to test that a Message::Hello id ﬁeld is withinthe range 3..=7 . We also want to bind the value to the variable id_variable so we can use it in the code associated with the arm. We could name this variable id , the same as the ﬁeld, but for this example we’ll use a diﬀerent name.

enum Message {

Hello { id: i32 },

}

let msg = Message::Hello { id: 5 };

match msg {

Message::Hello {

id: id_variable @ 3..=7,

} => println!("Found an id in range: {}", id_variable),

Message::Hello { id: 10..=12 } => {

println!("Found an id in another range")

}

Message::Hello { id } => println!("Found some other id: {}", id),

}

This example will print Found an id in range: 5 . By specifying id_variable @ before the range 3..=7 , we’re capturing whatever value matched the range while also testing that the value matched the range pattern.

In the second arm, where we only have a range speciﬁed in the pattern, the code associated with the arm doesn’t have a variable that contains the actual value of the id ﬁeld. The id ﬁeld’s value could have been 10, 11, or 12, but the code that goes with that pattern doesn’t know which it is. The pattern code isn’t able to use the value from the id ﬁeld, because we haven’t saved the id value in a variable.

Using @ lets us test a value and save it in a variable within one pattern.

  
  

**Unsafe Superpowers**

To switch to unsafe Rust, use the unsafe keyword and then start a new block that holds the unsafe code. You can take ﬁve actions in unsafe Rust that you can’t in safe Rust, which we call unsafe superpowers. Those superpowers include the ability to:

• Dereference a raw pointer

• Call an unsafe function or method

• Access or modify a mutable static variable

• Implement an unsafe trait

• Access ﬁelds of **union** s

It’s important to understand that unsafe doesn’t turn oﬀ the borrow checker or disable any other of Rust’s safety checks: if you use a reference in unsafe code, it will still be checked. The unsafe keyword only gives you access to these ﬁve features that are then not checked by the compiler for memory safety. You’ll still get some degree of safety inside of an unsafe block.

In addition, unsafe does not mean the code inside the block is necessarily dangerous or that it will deﬁnitely have memory safety problems: the intent is that as the programmer, you’ll ensure the code inside an unsafe block will access memory in a valid way.

To isolate unsafe code as much as possible, it’s best to enclose unsafe code within a safe abstraction and provide a safe API, which we’ll discuss later in the chapter when we examine unsafe functions and methods. Parts of the standard library are implemented as safe abstractions over unsafe code that has been audited. Wrapping unsafe code in a safe abstraction prevents uses of unsafe from leaking out into all the places that you or your users might want to use the functionality implemented with unsafe code, because using a safe abstraction is safe.

**Dereferencing a Raw Pointer**

Unsafe Rust has two new types called raw pointers that are similar to references. As with references, raw pointers can be immutable or mutable and are written as ***const T** and ***mut T** , respectively. The asterisk isn’t the dereference operator; it’s part of the type name. In the context of raw pointers, immutable means that the pointer can’t be directly assigned to after being dereferenced.

Diﬀerent from references and smart pointers, raw pointers:

• Are allowed to ignore the borrowing rules by having both immutable and mutable pointers or multiple mutable pointers to the same location

• Aren’t guaranteed to point to valid memory

• Are allowed to be null

• Don’t implement any automatic cleanup

By opting out of having Rust enforce these guarantees, you can give up guaranteed safety in exchange for greater performance or the ability to interface with another language or hardware where Rust’s guarantees don’t apply.

let mut num = 5;

let r1 = &num as *const i32; // this is pointer location of num

let r2 = &mut num as *mut i32;

Notice that we don’t include the unsafe keyword in this code. We can create raw pointers in safe code; we just can’t dereference raw pointers outside an unsafe block, as you’ll see in a bit.

Recall that we can create raw pointers in safe code, but we can’t dereference raw pointers and read the data being pointed to. In Listing 19-3, we use the dereference operator * on a raw pointer that requires an unsafe block.

  
  

unsafe {

println!("r1 is: {}", *r1);

println!("r2 is: {}", *r2);

}

With raw pointers, we can create a mutable pointer and an immutable pointer to the same location and change data through the mutable pointer, potentially creating a data race. Be careful!

  
  

**Calling an Unsafe Function or Method**

The second type of operation you can perform in an unsafe block is calling unsafe functions. **Unsafe** functions and methods look exactly like regular functions and methods, but they have an extra unsafe before the rest of the deﬁnition.

unsafe fn dangerous() {}

  
  

unsafe {

dangerous();

}

**Creating a Safe Abstraction over Unsafe Code**

Just because a function contains unsafe code doesn’t mean we need to mark the entire function as unsafe. In fact, wrapping unsafe code in a safe function is a common abstraction.

fn split_at_mut(values: &mut [i32], mid: usize) -> (&mut [i32], &mut [i32]) {

let len = values.len();

assert!(mid <= len);

(&mut values[..mid], &mut values[mid..])

}

We can’t implement this function using only safe Rust. An attempt might look something like Listing 19-5, which won’t compile. For simplicity, we’ll implement split_at_mut as a function rather than a method and only for slices of i32 values rather than for a generic type T

Rust’s borrow checker can’t understand that we’re borrowing diﬀerent parts of the slice; it only knows that we’re borrowing from the same slice twice. Borrowing diﬀerent parts of a slice is fundamentally okay because the two slices aren’t overlapping, but Rust isn’t smart enough to know this. When we know code is okay, but Rust doesn’t, it’s time to reach for unsafe code.

use std::slice;

fn split_at_mut(values: &mut [i32], mid: usize) -> (&mut [i32], &mut [i32]) {

let len = values.len();

let ptr = values.as_mut_ptr();

assert!(mid <= len);

unsafe {

(

slice::from_raw_parts_mut(ptr, mid),

slice::from_raw_parts_mut(ptr.add(mid), len - mid),

)

}

}

  
  

Note that we don’t need to mark the resulting split_at_mut function as unsafe , and we can call this function from safe Rust. We’ve created a safe abstraction to the unsafe code with an implementation of the function that uses unsafe code in a safe way, because it creates only valid pointers from the data this function has access to.

  
  

**Using extern Functions to Call External Code**

Sometimes, your Rust code might need to interact with code written in another language. For this, Rust has the keyword **extern** that facilitates the creation and use of a Foreign Function Interface **(FFI)**. An FFI is a way for a programming language to deﬁne functions and enable a diﬀerent (foreign) programming language to call those functions.

Functions declared within extern blocks are always unsafe to call from Rust code. The reason is that other languages don’t enforce Rust’s rules and guarantees, and Rust can’t check them, so responsibility falls on the programmer to ensure safety.

extern "C" {

fn abs(input: i32) -> i32;

}

fn main() {

unsafe {

println!("Absolute value of -3 according to C: {}", abs(-3));

}

}

Within the extern "C" block, we list the names and signatures of external functions from another language we want to call. The "C" part deﬁnes which application binary interface **(ABI)** the external function uses: the ABI deﬁnes how to call the function at the assembly level. The "C" ABI is the most common and follows the C programming language’s ABI.

**Calling Rust Functions from Other Languages**

We can also use extern to create an interface that allows other languages to call Rust functions. Instead of an creating a whole extern block, we add the extern keyword and specify the ABI to use just before the fn keyword for the relevant function. We also need to add a **#[no_mangle]** annotation to tell the Rust compiler not to mangle the name of this function. Mangling is when a compiler changes the name we’ve given a function to a diﬀerent name that contains more information for other parts of the compilation process to consume but is less human readable. Every programming language compiler mangles names slightly diﬀerently, so for a Rust function to be nameable by other languages, we must disable the Rust compiler’s name mangling.

In the following example, we make the call_from_c function accessible from C code, after it’s compiled to a shared library and linked from C:

#[no_mangle]

pub extern "C" fn call_from_c() {

println!("Just called a Rust function from C!");

}

This usage of extern does not require unsafe .

  
  

**Accessing or Modifying a Mutable Static Variable**

In this book, we’ve not yet talked about **global variables,** which Rust does support but can be problematic with Rust’s ownership rules. If two threads are accessing the same mutable global variable, it can cause a data race. In Rust, global variables are called **static** variables.

static HELLO_WORLD: &str = "Hello, world!";

fn main() {

println!("name is: {}", HELLO_WORLD);

}

Static variables are similar to constants, The names of static variables are in SCREAMING_SNAKE_CASE by convention. Static variables can only store references with the 'static lifetime, which means the Rust compiler can ﬁgure out the lifetime and we aren’t required to annotate it explicitly. Accessing an immutable static variable is safe.

A subtle diﬀerence between constants and immutable static variables is that values in a static variable have a ﬁxed address in memory. Using the value will always access the same data. Constants, on the other hand, are allowed to duplicate their data whenever they’re used. Another diﬀerence is that static variables can be mutable. Accessing and modifying mutable static variables is unsafe.

static mut COUNTER: u32 = 0;

fn add_to_count(inc: u32) {

unsafe {

COUNTER += inc;

}

}

fn main() {

add_to_count(3);

unsafe {

println!("COUNTER: {}", COUNTER);

}

}

With mutable data that is globally accessible, it’s diﬃcult to ensure there are no data races, which is why Rust considers mutable static variables to be unsafe. Where possible, it’s preferable to use the concurrency techniques and thread-safe smart pointers we discussed in Chapter 16 so the compiler checks that data accessed from diﬀerent threads is done safely.

**Implementing an Unsafe Trait**

We can use unsafe to implement an unsafe trait. A trait is unsafe when at least one of its methods has some invariant that the compiler can’t verify. We declare that a trait is unsafe by adding the unsafe keyword before trait and marking the implementation of the trait as unsafe too.

unsafe trait Foo {

// methods go here

}

  
  

unsafe impl Foo for i32 {

// method implementations go here

}

**Accessing Fields of a Union**

The ﬁnal action that works only with unsafe is accessing ﬁelds of a **union**. A union is similar to a struct , but only one declared ﬁeld is used in a particular instance at one time. Unions are primarily used to interface with unions in C code. Accessing union ﬁelds is unsafe because Rust can’t guarantee the type of the data currently being stored in the union instance.

  
  

**Specifying Placeholder Types in Trait Deﬁnitions with Associated Types**

Associated types connect a type placeholder with a trait such that the trait method deﬁnitions can use these placeholder types in their signatures. The implementor of a trait will specify the concrete type to be used instead of the placeholder type for the particular implementation. That way, we can deﬁne a trait that uses some types without needing to know exactly what those types are until the trait is implemented.

pub trait Iterator {

type Item;

fn next(&mut self) -> Option<Self::Item>;

}

Associated types might seem like a similar concept to generics, in that the latter allow us to deﬁne a function without specifying what types it can handle. To examine the diﬀerence between the two concepts, we’ll look at an implementation of the Iterator trait on a type named Counter that speciﬁes the Item type is u32 :

impl Iterator for Counter {

type Item = u32;

fn next(&mut self) -> Option<Self::Item> {

// --snip--

This syntax seems comparable to that of generics. So why not just deﬁne the Iterator trait withgenerics, as shown in Listing 19-13?

The diﬀerence is that when using generics, as in Listing 19-13, we must annotate the types in each implementation; because we can also implement Iterator<String> for Counter or any other type, we could have multiple implementations of Iterator for Counter . In other words, when a trait has a generic parameter, it can be implemented for a type multiple times, changing the concrete types of the generic type parameters each time. When we use the next method on Counter , we would have to provide type annotations to indicate which implementation of Iterator we want to use.

With associated types, we don’t need to annotate types because we can’t implement a trait on a type multiple times. In Listing 19-12 with the deﬁnition that uses associated types, we can only choose what the type of Item will be once, because there can only be one impl Iterator for Counter . We don’t have to specify that we want an iterator of u32 values everywhere that we call next on Counter .

Associated types also become part of the trait’s contract: implementors of the trait must provide a type to stand in for the associated type placeholder. Associated types often have a name that describes how the type will be used, and documenting the associated type in the API documentation is good practice.

**Default Generic Type Parameters and Operator Overloading**

When we use generic type parameters, we can specify a default concrete type for the generic type. This eliminates the need for implementors of the trait to specify a concrete type if the default type works. You specify a default type when declaring a generic type with the <PlaceholderType=ConcreteType> syntax.

A great example of a situation where this technique is useful is with operator overloading, in which you customize the behavior of an operator (such as + ) in particular situations.

Rust doesn’t allow you to create your own operators or overload arbitrary operators. But you can overload the operations and corresponding traits listed in std::ops by implementing the traits associated with the operator. For example, in Listing 19-14 we overload the + operator to add two Point instances together. We do this by implementing the Add trait on a Point struct:

use std::ops::Add;

#[derive(Debug, Copy, Clone, PartialEq)]

struct Point {

x: i32,

y: i32,

}

impl Add for Point {

type Output = Point;

fn add(self, other: Point) -> Point {

Point {

x: self.x + other.x,

y: self.y + other.y,

}

}

}

fn main() {

assert_eq!(

Point { x: 1, y: 0 } + Point { x: 2, y: 3 },

Point { x: 3, y: 3 }

);

}

  
  

----------------------------

trait Add<Rhs=Self> {

type Output;

fn add(self, rhs: Rhs) -> Self::Output;

}

This code should look generally familiar: a trait with one method and an associated type. The new part is Rhs=Self : this syntax is called default type parameters. The Rhs generic type parameter (short for “right hand side”) deﬁnes the type of the rhs parameter in the add method. If we don’t specify a concrete type for Rhs when we implement the Add trait, the type of Rhs will default to Self , which will be the type we’re implementing Add on.

When we implemented Add for Point , we used the default for Rhs because we wanted to add two Point instances.

Let’s look at an example of implementing the Add trait where we want to customize the Rhs type rather than using the default.

We have two structs, Millimeters and Meters , holding values in diﬀerent units. This thin wrapping of an existing type in another struct is known as the newtype pattern,

use std::ops::Add;

struct Millimeters(u32);

struct Meters(u32);

impl Add<Meters> for Millimeters {

type Output = Millimeters;

fn add(self, other: Meters) -> Millimeters {

Millimeters(self.0 + (other.0 * 1000))

}

}

To add Millimeters and Meters , we specify impl Add<Meters> to set the value of the Rhs type parameter instead of using the default of Self .

You’ll use default type parameters in two main ways:

• To extend a type without breaking existing code

• To allow customization in speciﬁc cases most users won’t need

**Fully Qualiﬁed Syntax for Disambiguation: Calling Methods with the Same Name**

Nothing in Rust prevents a trait from having a method with the same name as another trait’s method, nor does Rust prevent you from implementing both traits on one type. It’s also possible to implement a method directly on the type with the same name as methods from traits.

trait Pilot {

fn fly(&self);

}

trait Wizard {

fn fly(&self);

}

struct Human;

impl Pilot for Human {

fn fly(&self) {

println!("This is your captain speaking.");

}

}

impl Wizard for Human {

fn fly(&self) {

println!("Up!");

}

}

impl Human {

fn fly(&self) {

println!("*waving arms furiously*");

}

}

When we call fly on an instance of Human , the compiler defaults to calling the method that is directly implemented on the type, as shown in Listing 19-17.

fn main() {

let person = Human;

person.fly();

}

To call the fly methods from either the Pilot trait or the Wizard trait, we need to use more

explicit syntax to specify which fly method we mean. Listing 19-18 demonstrates this syntax.

fn main() {

let person = Human;

Pilot::fly(&person);

Wizard::fly(&person);

person.fly();

}

Specifying the trait name before the method name clariﬁes to Rust which implementation of fly we want to call. We could also write Human::fly(&person) , which is equivalent to the person.fly() that we used in Listing 19-18, but this is a bit longer to write if we don’t need to disambiguate.

However, associated functions that are not methods don’t have a self parameter. When there are multiple types or traits that deﬁne non-method functions with the same function name, Rust doesn't always know which type you mean unless you use fully qualiﬁed syntax.

trait Animal {

fn baby_name() -> String;

}

struct Dog;

impl Dog {

fn baby_name() -> String {

String::from("Spot")

}

}

impl Animal for Dog {

fn baby_name() -> String {

String::from("puppy")

}

}

fn main() {

println!("A baby dog is called a {}", Dog::baby_name());

}

This output isn’t what we wanted. We want to call the baby_name function that is part of the Animal trait that we implemented on Dog so the code prints A baby dog is called a puppy . The technique of specifying the trait name that we used in Listing 19-18 doesn’t help here; if we changemain to the code in Listing 19-20, we’ll get a compilation error.

fn main() {

println!("A baby dog is called a {}", Animal::baby_name());

}

To disambiguate and tell Rust that we want to use the implementation of Animal for Dog as opposed to the implementation of Animal for some other type, we need to use fully qualiﬁed syntax. Listing 19-21 demonstrates how to use fully qualiﬁed syntax.

fn main() {

println!("A baby dog is called a {}", <Dog as Animal>::baby_name());

}

implemented on Dog We’re providing Rust with a type annotation within the angle brackets, which indicates we want to call the baby_name method from the Animal trait as implemented on Dog by saying that we want to treat the Dog type as an Animal for this function call. This code will now print what we want:

In general, fully qualiﬁed syntax is deﬁned as follows:

<Type as Trait>::function(receiver_if_method, next_arg, ...);

For associated functions that aren’t methods, there would not be a receiver : there would only be the list of other arguments. You could use fully qualiﬁed syntax everywhere that you call functions or methods. However, you’re allowed to omit any part of this syntax that Rust can ﬁgure out from other information in the program. You only need to use this more verbose syntax in cases where there are multiple implementations that use the same name and Rust needs help to identify which implementation you want to call

  
  

**Using Supertraits to Require One Trait’s Functionality Within Another Trait**

Sometimes, you might write a trait deﬁnition that depends on another trait: for a type to implement the ﬁrst trait, you want to require that type to also implement the second trait. You would do this so that your trait deﬁnition can make use of the associated items of the second trait. The trait your trait deﬁnition is relying on is called a **supertrait** of your trait.

use std::fmt;

trait OutlinePrint: fmt::Display {

fn outline_print(&self) {

let output = self.to_string();

let len = output.len();

println!("{}", "*".repeat(len + 4));

println!("*{}*", " ".repeat(len + 2));

println!("* {} *", output);

println!("*{}*", " ".repeat(len + 2));

println!("{}", "*".repeat(len + 4));

}

}

Because we’ve speciﬁed that OutlinePrint requires the Display trait, we can use the to_string unction that is automatically implemented for any type that implements Display . If we tried to use to_string without adding a colon and specifying the Display trait after the trait name, we’d get an error saying that no method named to_string was found for the type &Self in the current scope.

Let’s see what happens when we try to implement OutlinePrint on a type that doesn’t implement Display , such as the Point struct:

struct Point {

x: i32,

y: i32,

}

impl OutlinePrint for Point {}

We get an error saying that Display is required but not implemented:

use std::fmt;

impl fmt::Display for Point {

fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {

write!(f, "({}, {})", self.x, self.y)

}

}

Then implementing the OutlinePrint trait on Point will compile successfully, and we can call outline_print on a Point instance to display it within an outline of asterisks.

**Using the Newtype Pattern to Implement External Traits on External Types**

we mentioned the orphan rule that states we’re only allowed to implement a trait on a type if either the trait or the type are local to our crate. It’s possible to get around this restriction using the newtype pattern, which involves creating a new type in a tuple struct.

The tuple struct will have one ﬁeld and be a thin wrapper around the type we want to implement a trait for. Then the wrapper type is local to our crate, and we can implement the trait on the wrapper. Newtype is a term that originates from the Haskell programming language. There is no runtime performance penalty for using this pattern, and the wrapper type is elided at compile time.

use std::fmt;

struct Wrapper(Vec<String>);

impl fmt::Display for Wrapper {

fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {

write!(f, "[{}]", self.0.join(", "))

}

}

fn main() {

let w = Wrapper(vec![String::from("hello"), String::from("world")]);

println!("w = {}", w);

}

  
  

  
  

  
  

  
  

**Advanced Types**

The Rust type system has some features that we’ve so far mentioned but haven’t yet discussed. We’ll start by discussing newtypes in general as we examine why newtypes are useful as types. Then we’ll move on to type aliases, a feature similar to newtypes but with slightly diﬀerent semantics. We’ll also discuss the ! **type** and dynamically sized types.

C**reating Type Synonyms with Type Aliases**

Rust provides the ability to declare a type alias to give an existing type another name. For this we use the type keyword. For example, we can create the alias Kilometers to i32 like so:

type Kilometers = i32;

Now, the alias Kilometers is a synonym for i32 ; unlike the Millimeters and Meters types we created in Listing 19-15, Kilometers is not a separate, new type. Values that have the type Kilometers will be treated the same as values of type i32 :

type Kilometers = i32;

let x: i32 = 5;

let y: Kilometers = 5;

println!("x + y = {}", x + y);

This code is much easier to read and write! Choosing a meaningful name for a type alias can help communicate your intent as well (thunk is a word for code to be evaluated at a later time, so it’s an appropriate name for a closure that gets stored).

  
  

let f: Box<dyn Fn() + Send + 'static> = Box::new(|| println!("hi"));

fn takes_long_type(f: Box<dyn Fn() + Send + 'static>) {

// --snip--

}

fn returns_long_type() -> Box<dyn Fn() + Send + 'static> {

// --snip--

}

A type alias makes this code more manageable by reducing the repetition. In Listing 19-25, we’ve introduced an alias named Thunk for the verbose type and can replace all uses of the type with the shorter alias Thunk .

type Thunk = Box<dyn Fn() + Send + 'static>;

let f: Thunk = Box::new(|| println!("hi"));

fn takes_long_type(f: Thunk) {

// --snip--

}

fn returns_long_type() -> Thunk {

// --snip--

}

**The Never Type that Never Returns**

Rust has a special type named **!** that’s known in type theory lingo as the empty type because it has no values. We prefer to call it the never type because it stands in the place of the return type when a function will never return. Here is an example:

fn bar() -> ! {

// --snip--

}

This code is read as “the function bar returns never.” Functions that return never are called **diverging functions**. We can’t create values of the type **!** so **bar** can never possibly return.

**Dynamically Sized Types and the Sized Trait**

Rust needs to know certain details about its types, such as how much space to allocate for a value of a particular type. This leaves one corner of its type system a little confusing at ﬁrst: the concept of dynamically sized types. Sometimes referred to as DSTs or unsized types, these types let us write code using values whose size we can know only at runtime.

Let’s dig into the details of a dynamically sized type called str , which we’ve been using throughout the book. That’s right, not &str , but str on its own, is a DST. We can’t know how long the string is until runtime, meaning we can’t create a variable of type str , nor can we take an argument of type str . Consider the following code, which does not work:

let s1: str = "Hello there!";

let s2: str = "How's it going?";

So although a &T is a single value that stores the memory address of where the T is located, a &str is two values: the address of the str and its length. As such, we can know the size of a &str value at compile time: it’s twice the length of a usize . That is, we always know the size of a &str , no matter how long the string it refers to is. In general, this is the way in which dynamically sized types are used in Rust: they have an extra bit of metadata that stores the size of the dynamic information. The golden rule of dynamically sized types is that we must always put values of dynamically sized types behind a pointer of some kind.

We can combine str with all kinds of pointers: for example, Box<str> or Rc<str> .

To work with DSTs, Rust provides the **Sized** trait to determine whether or not a type’s size is known at compile time. This trait is automatically implemented for everything whose size is known at compile time. In addition, Rust implicitly adds a bound on Sized to every generic function. That is, a generic function deﬁnition like this:

fn generic<T>(t: T) {

// --snip--

}

is actually treated as though we had written this:

fn generic<T: **Sized**>(t: T) {

// --snip--

}

By default, generic functions will work only on types that have a known size at compile time. However, you can use the following special syntax to relax this restriction:

fn generic<T: **?Sized**>(t: &T) {

// --snip--

}

A trait bound on **?Sized** means _“ T may or may not be Sized ”_ and this notation overrides the default that generic types must have a known size at compile time. The ?Trait syntax with this meaning is only available for Sized , not any other traits.

Also note that we switched the type of the t parameter from T to &T . Because the type might not be Sized , we need to use it behind some kind of pointer. In this case, we’ve chosen a reference.

**Function Pointers**

The **fn** type is called a function pointer. Passing functions with function pointers will allow you to use functions as arguments to other functions.

The syntax for specifying that a parameter is a function pointer is similar to that of closures, as shown in Listing 19-27, where we’ve deﬁned a function add_one that adds one to its parameter. The function do_twice takes two parameters: a function pointer to any function that takes an i32 parameter and returns an i32 , and one i32 value . The do_twice function calls the function f twice, passing it the arg value, then adds the two function call results together. The main function calls do_twice with the arguments add_one and 5 .

fn add_one(x: i32) -> i32 {

x + 1

}

fn do_twice(f: fn(i32) -> i32, arg: i32) -> i32 {

f(arg) + f(arg)

}

fn main() {

let answer = do_twice(add_one, 5);

println!("The answer is: {}", answer);

}

This code prints The answer is: 12 . We specify that the parameter f in do_twice is an fn that takes one parameter of type i32 and returns an i32 . We can then call f in the body of do_twice .

In main , we can pass the function name add_one as the ﬁrst argument to do_twice . Unlike closures, fn is a type rather than a trait, so we specify fn as the parameter type directly rather than declaring a generic type parameter with one of the Fn traits as a trait bound.

Function pointers implement all three of the closure traits ( Fn , FnMut , and FnOnce ), meaning you can always pass a function pointer as an argument for a function that expects a closure. It’s best to write functions using a generic type and one of the closure traits so your functions can accept either functions or closures.

**Macros**

We’ve used macros like println! throughout this book, but we haven’t fully explored what a macro is and how it works. The term macro refers to a family of features in Rust: declarative macros with macro_rules! and three kinds of procedural macros:

• Custom #[derive] macros that specify code added with the derive attribute used on structs and enums

• Attribute-like macros that deﬁne custom attributes usable on any item

• Function-like macros that look like function calls but operate on the tokens speciﬁed as their argument

The Diﬀerence Between Macros and Functions Fundamentally, macros are a way of writing code that writes other code, which is known as metaprogramming. In Appendix C, we discuss the derive attribute, which generates an implementation of various traits for you. We’ve also used the println! and vec! Macros throughout the book. All of these macros expand to produce more code than the code you’ve written manually.

Metaprogramming is useful for reducing the amount of code you have to write and maintain, which is also one of the roles of functions. However, macros have some additional powers that functions don’t.

A function signature must declare the number and type of parameters the function has. Macros, on the other hand, can take a variable number of parameters: we can call println!("hello") with one argument or println!("hello {}", name) with two arguments. Also, macros are expanded before the compiler interprets the meaning of the code, so a macro can, for example, implement a trait on a given type. A function can’t, because it gets called at runtime and a trait needs to be implemented at compile time.

The downside to implementing a macro instead of a function is that macro deﬁnitions are more complex than function deﬁnitions because you’re writing Rust code that writes Rust code. Due to this indirection, macro deﬁnitions are generally more diﬃcult to read, understand, and maintain than function deﬁnitions.

Another important diﬀerence between macros and functions is that you must deﬁne macros or bring them into scope before you call them in a ﬁle, as opposed to functions you can deﬁne anywhere and call anywhere.

**Declarative Macros with macro_rules! for General Metaprogramming**

The most widely used form of macros in Rust is the declarative macro. These are also sometimes referred to as “macros by example,” “ **macro_rules!** macros,” or just plain “macros.” At their core, declarative macros allow you to write something similar to a Rust match expression. As discussed in Chapter 6, match expressions are control structures that take an expression, compare the resulting value of the expression to patterns, and then run the code associated with the matching pattern. Macros also compare a value to patterns that are associated with particular code: in this situation, the value is the literal Rust source code passed to the macro; the patterns are compared with the structure of that source code; and the code associated with each pattern, when matched, replaces the code passed to the macro. This all happens during compilation.

#[macro_export]

macro_rules! vec {

( $( $x:expr ),* ) => {

{

let mut temp_vec = Vec::new();

$(

temp_vec.push($x);

)*

temp_vec

}

};

}

The #[macro_export] annotation indicates that this macro should be made available whenever the crate in which the macro is deﬁned is brought into scope. Without this annotation, the macro can’t be brought into scope.

We then start the macro deﬁnition with macro_rules! and the name of the macro we’re deﬁningwithout the exclamation mark.

The structure in the vec! body is similar to the structure of a match expression. Here we have one arm with the pattern ( $( $x:expr ),* ) , followed by => and the block of code associated with this pattern. If the pattern matches, the associated block of code will be emitted. Given that this is the only pattern in this macro, there is only one valid way to match; any other pattern will result in an error. More complex macros will have more than one arm.

First, we use a set of parentheses to encompass the whole pattern. We use a dollar sign ( $ ) to declare a variable in the macro system that will contain the Rust code matching the pattern. The dollar sign makes it clear this is a macro variable as opposed to a regular Rust variable. Next comes a set of parentheses that captures values that match the pattern within the parentheses for use in the replacement code. Within $() is $x:expr , which matches any Rust expression and gives the expression the name $x .

The comma following $() indicates that a literal comma separator character could optionally appear after the code that matches the code in $() . The * speciﬁes that the pattern matches zero or more of whatever precedes the * .

When we call this macro with vec![1, 2, 3]; , the $x pattern matches three times with the three expressions 1 , 2 , and 3 .

Now let’s look at the pattern in the body of the code associated with this arm: temp_vec.push() within $()* is generated for each part that matches $() in the pattern zero or more times depending on how many times the pattern matches. The $x is replaced with each expression matched.

  
  

**Procedural Macros for Generating Code from Attributes**

The second form of macros is the procedural macro, which acts more like a function (and is a type of procedure). Procedural macros accept some code as an input, operate on that code, and produce some code as an output rather than matching against patterns and replacing the code with other code as declarative macros do. The three kinds of procedural macros are custom derive, attribute- like, and function-like, and all work in a similar fashion.

When creating procedural macros, the deﬁnitions must reside in their own crate with a special crate type. This is for complex technical reasons that we hope to eliminate in the future.

use proc_macro;

#[some_attribute]

pub fn some_name(input: TokenStream) -> TokenStream {}

The function that deﬁnes a procedural macro takes a TokenStream as an input and produces a TokenStream as an output. The TokenStream type is deﬁned by the proc_macro crate that is included with Rust and represents a sequence of tokens. This is the core of the macro: the source code that the macro is operating on makes up the input TokenStream , and the code the macro produces is the output TokenStream . The function also has an attribute attached to it that speciﬁes which kind of procedural macro we’re creating. We can have multiple kinds of procedural macros in the same crate.

  
  

**How to Write a Custom derive Macro**

Let’s create a crate named hello_macro that deﬁnes a trait named HelloMacro with one associated function named hello_macro . Rather than making our users implement the HelloMacro trait for each of their types, we’ll provide a procedural macro so users can annotate their type with #[derive(HelloMacro)] to get a default implementation of the hello_macro function. The default implementation will print Hello, Macro! My name is TypeName! where TypeName is the name of the type on which this trait has been deﬁned.

use hello_macro::HelloMacro;

use hello_macro_derive::HelloMacro;

#[derive(HelloMacro)]

struct Pancakes;

fn main() {

Pancakes::hello_macro();

}

  
  

**Attribute-like macros**

Attribute-like macros are similar to custom derive macros, but instead of generating code for the derive attribute, they allow you to create new attributes. They’re also more ﬂexible: derive only works for structs and enums; attributes can be applied to other items as well, such as functions.

Here’s an example of using an attribute-like macro: say you have an attribute named route that annotates functions when using a web application framework:

  
  

#[route(GET, "/")]

fn index() {

his #[route] attribute would be deﬁned by the framework as a procedural macro. The signature of the macro deﬁnition function would look like this:

#[proc_macro_attribute]

pub fn route(attr: TokenStream, item: TokenStream) -> TokenStream {

Here, we have two parameters of type TokenStream . The ﬁrst is for the contents of the attribute: the GET, "/" part. The second is the body of the item the attribute is attached to: in this case, fn index() {} and the rest of the function’s body

**Function-like macros**

Function-like macros deﬁne macros that look like function calls. Similarly to macro_rules! Macros, they’re more ﬂexible than functions; for example, they can take an unknown number of arguments. However, macro_rules! macros can be deﬁned only using the match-like syntax we discussed in the section “Declarative Macros with macro_rules! for General Metaprogramming” earlier. Function-like macros take a TokenStream parameter and their deﬁnition manipulates that TokenStream using

Rust code as the other two types of procedural macros do. An example of a function-like macro is an sql! macro that might be called like so:

let sql = sql!(SELECT * FROM posts WHERE id=1);

This macro would parse the SQL statement inside it and check that it’s syntactically correct, which is much more complex processing than a macro_rules! macro can do. The sql! macro would be deﬁned like this:

#[proc_macro]

pub fn sql(input: TokenStream) -> TokenStream {

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

**Keywords Currently in Use**

• **as** - perform primitive casting, disambiguate the speciﬁc trait containing an item, or rename

items in use statements

• **async** - return a Future instead of blocking the current thread

• **await** - suspend execution until the result of a Future is ready

• **break** - exit a loop immediately

• **const** - deﬁne constant items or constant raw pointers

• **continue** - continue to the next loop iteration

• **crate** - in a module path, refers to the crate root

• **dyn** - dynamic dispatch to a trait object

• **else** - fallback for if and if let control ﬂow constructs

• **enum** - deﬁne an enumeration

• **extern** - link an external function or variable

• **false** - Boolean false literal

• **fn** - deﬁne a function or the function pointer type

• **for** - loop over items from an iterator, implement a trait, or specify a higher-ranked lifetime

• **if** - branch based on the result of a conditional expression

• **impl** - implement inherent or trait functionality

• **in** - part of for loop syntax

• **let** - bind a variable

• **loop** - loop unconditionally

• **match** - match a value to patterns

• **mod** - deﬁne a module

• **move** - make a closure take ownership of all its captures

• **mut** - denote mutability in references, raw pointers, or pattern bindings

• **pub** - denote public visibility in struct ﬁelds, impl blocks, or modules

• **ref** - bind by reference

• **return** - return from function

• **Self** - a type alias for the type we are deﬁning or implementing

• **self** - method subject or current module

• **static** - global variable or lifetime lasting the entire program execution

• **struct** - deﬁne a structure

• **super** - parent module of the current module

• **trait** - deﬁne a trait

• **true** - Boolean true literal

• **type** - deﬁne a type alias or associated type

• **union** - deﬁne a union; is only a keyword when used in a union declaration

• **unsafe** - denote unsafe code, functions, traits, or implementations

• **use** - bring symbols into scope

• **where** - denote clauses that constrain a type

• **while** - loop conditionally based on the result of an expression

  
  

**Keywords Reserved for Future Use**

• abstract

• become

• box

• do

• final

• macro

• override

• priv

• try

• typeof

• unsized

• virtual

• yield

  
  

  
  

  
  

  
  

**Raw Identiﬁers**

Raw identiﬁers are the syntax that lets you use keywords where they wouldn’t normally be allowed. You use a raw identiﬁer by preﬁxing a keyword with **r#** .

fn r#match(needle: &str, haystack: &str) -> bool {

haystack.contains(needle)

}

fn main() {

assert!(r#match("foo", "foobar"));

}

This code will compile without any errors. Note the **r#** preﬁx on the function name in its deﬁnition as well as where the function is called in main .

  
  

  
  

**Operators**

  
  

_**Operator Example Explanation Overloadable?**_

! ident!(...) ,

ident!{...} , Macro expansion

ident![...]

! !expr Bitwise or logical complement Not

!= expr != expr Nonequality comparison PartialEq

% expr % expr Arithmetic remainder Rem

%= var %= expr Arithmetic remainder and

assignment RemAssign

& &expr , &mut expr Borrow

& &type , &mut type, Borrowed pointer type

&'a type , &'a mut

type

& expr & expr Bitwise AND BitAnd

&= var &= expr Bitwise AND and assignment BitAndAssign

&& expr && expr Short-circuiting logical AND

* expr * expr Arithmetic multiplication Mul

*= var *= expr Arithmetic multiplication and MulAssign

assignment

* *expr Dereference Deref

* *const type , *mut Raw pointer

type

+ trait + trait , 'a Compound type constraint

+ trait

+ expr + expr Arithmetic addition Add

+= var += expr Arithmetic addition and AddAssign

assignment

, expr, expr Argument and element

separator

- - expr Arithmetic negation Neg

- expr – expr Arithmetic subtraction Sub

-= var -= expr Arithmetic subtraction and SubAssign

assignment

→ fn(...) -> type , Function and closure return type

|...| -> type

. expr.ident Member access

.. .. , expr.. , Right-exclusive range literal PartialOrd

..expr ,

expr..expr

..= ..=expr , Right-inclusive range literal PartialOrd

expr..=expr

.. ..expr Struct literal update syntax

.. variant(x, ..) , “And the rest” pattern binding

struct_type { x,

.. }

… expr...expr (Deprecated, use ..= instead) In

a pattern: inclusive range pattern

/ expr / expr Arithmetic division Div

/= var /= expr Arithmetic division and DivAssign

assignment

: pat: type , ident: Constraints

type

: ident: expr Struct ﬁeld initializer

: 'a: loop {…} Loop label

; expr; Statement and item terminator

; [...; len] Part of ﬁxed-size array syntax

<< expr << expr Left-shift Shl

<<= var <<= expr Left-shift and assignment ShlAssign

< expr < expr Less than comparison PartialOrd

<= expr <= expr Less than or equal to PartialOrd

comparison

= var = expr , ident Assignment/equivalence

= type

== expr == expr Equality comparison PartialEq

  
  

=> pat => expr Part of match arm syntax

> expr > expr Greater than comparison PartialOrd

>= expr >= expr Greater than or equal to PartialOrd

comparison

>> expr >> expr Right-shift Shr

>>= var >>= expr Right-shift and assignment ShrAssign

@ ident @ pat Pattern binding

^ expr ^ expr Bitwise exclusive OR BitXor

^= var ^= expr Bitwise exclusive OR and BitXorAssign

assignment

| pat | pat Pattern alternatives

| expr | expr Bitwise OR BitOr

|= var |= expr Bitwise OR and assignment BitOrAssign

|| expr || expr Short-circuiting logical OR

? expr? Error propagation

  
  

  
  

**Non-operator Symbols**

The following list contains all symbols that don’t function as operators; that is, they don’t behave like a function or method call.

_**Symbol Explanation**_

'ident Named lifetime or loop label

...u8 , ...i32 , ...f64 , Numeric literal of speciﬁc type

...usize , etc.

"…" String literal

r"..." , r#"..."# , r##"..."## , Raw string literal, escape characters not processed

etc.

b"…" Byte string literal; constructs an array of bytes instead

of a string

br"..." , br#"..."# , Raw byte string literal, combination of raw and byte string literal

br##"..."## , etc.

'…' Character literal

b'…' ASCII byte literal

|...| expr Closure

! Always empty bottom type for diverging functions

_ “Ignored” pattern binding; also used to make integer

literals readable

  
  

  
  

  
  

**Path-Related Syntax**

_**Symbol Explanation**_

ident::ident Namespace path

::path Path relative to the crate root (i.e., an explicitly absolute path)

self::path Path relative to the current module (i.e., an explicitly

relative path).

super::path Path relative to the parent of the current module

type::ident , <type as Associated constants, functions, and types

trait>::ident

<type>::… Associated item for a type that cannot be directly named

(e.g., <&T>::... , <[T]>::... , etc.)

trait::method(…) Disambiguating a method call by naming the trait that deﬁnes it

type::method(…) Disambiguating a method call by naming the type for which it’s deﬁned

<type as Disambiguating a method call by naming the trait and type

trait>::method(...)

  
  

**Generics**

_**Symbol Explanation**_

path<...> Speciﬁes parameters to generic type in a type (e.g., Vec<u8> )

path::<...> , Speciﬁes parameters to generic type, function, or method in an

method::<...> expression; often referred to as turboﬁsh (e.g., "42".parse::

<i32>() )

fn ident<...> … Deﬁne generic function

struct ident<...> ... Deﬁne generic structure

enum ident<...> … Deﬁne generic enumeration

impl<...> … Deﬁne generic implementation

for<...> type Higher-ranked lifetime bounds

type<ident=type> A generic type where one or more associated types have speciﬁc

assignments (e.g., Iterator<Item=T> )

**Trait Bound Constraints**

_**Symbol Explanation**_

T: U Generic parameter T constrained to types that implement U

T: 'a Generic type T must outlive lifetime 'a (meaning the type cannot

transitively contain any references with lifetimes shorter than 'a )

T: 'static Generic type T contains no borrowed references other than 'static

ones

'b: 'a Generic lifetime 'b must outlive lifetime 'a

T: ?Sized Allow generic type parameter to be a dynamically sized type

'a + trait , Compound type constraint

trait + trait

  
  

**Macros and Attributes**

_**Symbol Explanation**_

#[meta] Outer attribute

#![meta] Inner attribute

$ident Macro substitution

$ident:kind Macro capture

$(…)…Macro repetition Macro invocation

ident!(...) , ident!{...} ,

ident![...]

  
  

**Comments**

_**Symbol Explanation**_

// Line comment

//! Inner line doc comment

/// Outer line doc comment

/*...*/ Block comment

/*!...*/ Inner block doc comment

/**...*/ Outer block doc comment

**Tuples**

_**Symbol Explanation**_

() Empty tuple (aka unit), both literal and type

(expr) Parenthesized expression

(expr,) Single-element tuple expression

(type,) Single-element tuple type

(expr, …) Tuple expression

(type, …) Tuple type

expr(expr, …) Function call expression; also used to initialize tuple struct s and

tuple enum variants

expr.0 , expr.1 , Tuple indexing

etc.

  
  

**Square Brackets**

_**Context Explanation**_

[…] Array literal

[expr; len]

Array literal containing len copies of expr

[type; len] Array type containing len instances of type

expr[expr] Collection indexing. Overloadable ( Index , IndexMut )

expr[..] , expr[a..], Collection indexing pretending to be collection slicing, using

expr[..b] , expr[a..b] Range , RangeFrom , RangeTo , or RangeFull as the “index”

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

  
  

**NOTE : Repeat chapters**

  
  

1. Closoure repeat from chapter 13.

2 smart pointers from ch 15

3. Conncurrency 16

4. Macro & last chapter

























