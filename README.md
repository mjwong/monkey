# monkey
Intrepretor for the Monkey programming language. 

In the Monkey programming language, everything besides let and return statements is an expression, i.e an expression alone can be a statement itself. The language features are as follows:

- C-like syntax
- variable bindings
- integers and booleans
- arithmetic expressions
- built-in functions
- first-class and higher-order functions
- closures
- a string data structure
- an array data structure
- a hash data structure
- operator precedence, infix/prefix operators

E.g.

Binding values:

```
let age = 1;
let name = "Monkey";
let result = 10 * (20 / 2);
```

Binding an array of integers:

```
let myArray = {1, 2, 3, 4, 5};
```

Binding a hash:

```
let me = {"name": "Michael", "age": 21};
```

Accessing elements in arrays and hashes:

```
myArray[0]	// ==> 1
me["name"] 	// ==> "Michael"
```

Binding functions:

Function literals as expression, i.e. function literals can be used
in every place where any other expression is valid:

```
let add = fn(a, b) { return a + b; };
```

Function literal in place of an identifier:

```
fn(x, y) { return x + y}(5, 5)
(fn(x) { return x}(5) * 10
```

If expressions in function literals:

```
let result = if (10>5)n { true } else { false };
```
result // => true

Implicit return values (i.e. value of the last statement/expression in function is returned):

```
let add = fn(a, b) { a + b; };
```

Calling function:

```
add(1, 2);
```

Recursive calls to function (tail recursion):

```
let fibonacci = fn(x) {
	if (x == 0) {
		0
	} else {
		if (x == 1) {
			1
		} else {
			fibonacci(x - 1) + fibonacci(x - 2);
		}
	}
};
```

Function literal as the expression in a return statement inside another function literal:
```
fn() {
	return fn(x, y) { return x > y; };
}
```

Using a function literal as an argument when calling another function:
```
myFunc(x, y, fn(x, y) { return x > y; });
```

Binding higher order functions:
```
let twice = fn(f, x) {
	return f(f(x));
};

let addTwo = fn(x) {
	return x + 2;
};

twice(addTwo, 2); 	// ==> 6
```

Operator precedence:

The validity of a token's position depends on the context the tokens that come before and after, and their precedence.


Top Down Operator Precedence (PRATT) Parsing methodology is used to parse Expressions.

The PRATT paraser's approach is to associate the parsing function with token types.
Whenever this token type is encountered, the parsing functions are called to parse the appropriate expression and return an AST node that represents it.
Each token type n have up to two parsing functions associated with it, depending on whether the token if found in a prefix o4 qn infix position.

Major parts:

- Lexer
- Parser
- Abstract Syntax Tree (AST)
- Internal object system
- Evaluator
