* About *this*
* Binding
----
# About `this`
##  What `this` is not 
1. `this` is not a reference to the function itself. The following code trying to track how many time `foo` is called doesn't work as expected. 
```js
function foo(num) {
	console.log( "foo: " + num );

	// keep track of how many times `foo` is called
	this.count++;
}

foo.count = 0;

var i;

for (i=0; i<10; i++) {
	if (i > 5) {
		foo( i );
	}
}
// foo: 6
// foo: 7
// foo: 8
// foo: 9

// how many times was `foo` called?
console.log( foo.count ); // 0 -- WTF?
```

2. `this` is not a reference to this function's lexical scope. The following code trying to reference variable `a` from function `bar()` doesn't work. 
```js
function foo() {
	var a = 2;
	this.bar();
}

function bar() {
	console.log( this.a );
}

foo(); //undefined
```

## What `this` is 
`this` is a runtime binding. The binding is made when a function is invoked and determinded entirely by the call-site where the function is called. 

# About binding
There are 4 different bindings. 
1. default binding. undefined in strict mode, global object otherwise.
2. implicit binding. Called with a context object owning the call? Use that context object.
3. explicit and hard binding. Called with call or apply (or bind)? Use the specified object.
4. `new` binding. Called with new? Use the newly constructed object.

Precedence: 4 > 3 > 2 > 1