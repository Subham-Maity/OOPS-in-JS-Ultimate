# 🔗 [You can read here](https://dev.to/codexam/oops-in-js-ultimate-4j34)
##  ▶️ Intro

###  ⭐ What is OOPs ?

Object-oriented programming is an approach to  solving problems by creating objects  .

### ⭐ 4 Pillars of OOP

Terminologies in OOP

1. **Abstraction** - Hiding internal details (show only essential info!)
2. **Encapsulation** - The act of putting various components together (in a capsule)
3. **Inheritance** - The act of deriving new things from existing things
4. **Polymorphism** - One entity, many forms


![js](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pnu2pnsb4tkym4hoxz7h.png)





##  ▶️ Prototypes and __proto__

JavaScript's objects have a special property called `prototype` that is  *either `null` or references another object* 


**When we  try to read a property from an object, and it's missing, JavaScript automatically takes it from the prototype. This is called prototype inheritance**

###  ⭐ Setting a Prototype

**We can set the prototype by setting `__proto__`. If we read a property from an object that is not in the object but is present in the prototype, JavaScript will take it from the prototype. If we have a method in the object, it will be called from the object. If it's missing in the object and present in the prototype, it will be called from the prototype.**

###  ⭐ Example:

```javascript
//It will work properly
let p = {
    run : () => {
        console.log("run")
    }
}

p.run()//Output: - run

//Let's define another property
let a = {
    name : " subham"
}

a.run() //TypeError: a.run is not a function

//Now with proto
let b = {
    name : " subham"
}
b.__proto__ = p
b.run() //Output: - run
```

Simply, you can inherit some object’s prototype in another object. This is called prototype inheritance.

```js
//It will work properly
let p = {
    run : () => {
        console.log("p run")
    }
}

p.run()//Output: - p run

//Now with proto
let b = {
    run : () => {
        console.log("b run")
    }
}
b.__proto__ = p
b.run() //Output: - b run

```
**If a property or method is already present in the object, JavaScript will use that property or method. If it's not present in the object but is present in the prototype, JavaScript will take it from the prototype. In this example, since the `run` method is already present in the `b` object, it will print 'b run'.**

##  ▶️ Classes and Object

- In object-oriented programming, a class is a template definition of the methods and variables in a particular kind of object
- In object-oriented programming, an object is a specific instance of a class (or struct) which has been allocated in memory.


###  ⭐ Example:
```js
//class
class GoogleForm {
    submit() {
       console.log(this.name + " " + this.roll + " Your form submitted")
    }
    cancel() {
        console.log(this.name + " " + this.roll +" Your form cancelled")
    }
    fill(given_name , roll) {
        this.name = given_name
        this.roll = roll
    }
}


//object
const student1Form = new GoogleForm()

student1Form.fill("Rahul" , 24)

const student2Form = new GoogleForm()

student2Form.fill("Raj" , 25)

student2Form.cancel()


student1Form.submit()

student2Form.submit()
```

## ▶️ Constructor

In JavaScript, a constructor is  a **special function** that creates and initializes objects, setting their initial state and properties. 

Let's say they forget to fill the form and click on the submit button it will throw undefined!
```js
class Form {

    submit() {
        console.log(this.name + ": Your form is submitted for train number: " + this.trainno)
    }

    cancel() {
        console.log(this.name + ": This form is cancelled for train number: " + this.trainno)
        this.trainno = 0
    }
    fill(givenname, trainno) {
        this.name = givenname
        this.trainno = trainno
    }
    
}

let myForm1 = new Form()

let myForm2 = new Form()
//
// myForm1.fill("Gaurav", 1234)
//
// myForm2.fill("Rahul", 5678)

myForm1.submit()

myForm2.submit()

myForm2.cancel()

// Output: undefined: Your form is submitted for train number: undefined
// Output: undefined: Your form is submitted for train number: undefined
// Output: undefined: This form is cancelled for train number: undefined
 
```


Now create constructor,

```js
class Form {

    constructor() {
        this.name = "Gaurav"
        this.trainno = 0
    }

    submit() {
        console.log(this.name + ": Your form is submitted for train number: " + this.trainno)
    }

    cancel() {
        console.log(this.name + ": This form is cancelled for train number: " + this.trainno)
        this.trainno = 0
    }
    fill(givenname, trainno) {
        this.name = givenname
        this.trainno = trainno
    }

}

let myForm1 = new Form()

let myForm2 = new Form()

// myForm1.fill("Gaurav", 1234)
//
// myForm2.fill("Rahul", 5678)

myForm1.submit()

myForm2.submit()

myForm2.cancel()

// Output: Gaurav: Your form is submitted for train number: 0
// Output: Gaurav: Your form is submitted for train number: 0
// Output: Gaurav: This form is cancelled for train number: 0
```


###  ⭐ Types of Constructors

1. **Non-Parameterized Constructor**: A constructor that has no arguments.

```js
    class Example {
        constructor() {
            this.property = "default value";
        }
    }
```

2. **Parameterized Constructor**: A constructor that takes parameters.

```js
    class Example {
        constructor(value) {
            this.property = value;
        }
    }
```

3. **Copy Constructor**: JavaScript does not have a built-in copy constructor like C++ or Java. However, you can create a method to copy an object.

```js
    class Example {
        constructor(value) {
            this.property = value;
        }

        copy() {
            return new Example(this.property);
        }
    }

    const original = new Example("original value");
    const copy = original.copy();
```

Unlike languages like C++, JavaScript does not have destructors. Instead, JavaScript relies on an efficient garbage collector that automatically deallocates memory.

## ▶️ Inheritance

The capability of a class to derive properties and characteristics from another class is called Inheritance. 

###  ⭐ Why ?

#### If you don't know what is Inheritance

```js
class Animal {
    constructor(name, color , age) {
        this.name = name
        this.color = color
        this.age = age
    }
    run() {
        console.log(this.name + ' is running')
    }

    shout() {

        console.log(this.name + ' is shouting')
    }

    sleep() {
        console.log(this.name + ' is sleeping')
    }
}

//If you are nub developer you will do
class Monkey {
    constructor(name, color) {
        this.name = name
        this.color = color
    }
    run() {
        console.log(this.name + ' is running')
    }

    shout() {

        console.log(this.name + ' is shouting')
    }

    sleep() {
        console.log(this.name + ' is sleeping')
    }

    eatBanana() {
        console.log(this.name + ' is eating banana')
    }
}

const animal_1 = new Monkey('Simba monkey', 'Brown', 2)

const animal_2 = new Animal('Donkey', 'White', 3)

animal_1.eatBanana()

animal_2.shout()
```
#### If you know

```js
//Parent Class - Base Class
class Animal {
    constructor(name, color , age) {
        this.name = name
        this.color = color
        this.age = age
    }
    run() {
        console.log(this.name + ' is running')
    }

    shout() {

        console.log(this.name + ' is shouting')
    }

    sleep() {
        console.log(this.name + ' is sleeping')
    }
}

//Child Class - Derived Class
class Monkey extends Animal{
    eatBanana() {
        console.log(this.name + ' is eating banana')
    }
    //you can also add new methods
    hide() {
        console.log(this.name + ' is hiding')
    }
}

const animal_1 = new Monkey('Simba monkey', 'Brown', 2)

const animal_2 = new Animal('Donkey', 'White', 3)

animal_1.eatBanana()
animal_1.run()
animal_1.hide()

animal_2.shout()
```



###  ⭐ Types of Inheritance

1. Single Inheritance when one class inherits another class, it is known as single level inheritance.

```javascript
class Shape {
  area() {
    console.log("Displays Area of Shape");
  }
}

class Triangle extends Shape {
  area(h, b) {
    console.log((1/2) * b * h);
  }
}

const triangle = new Triangle();
triangle.area(10, 5); // Output: 25
```

2. Hierarchical Inheritance is defined as the process of deriving more than one class from a base class.

```javascript
class Shape {
  area() {
    console.log("Displays Area of Shape");
  }
}

class Triangle extends Shape {
  area(h, b) {
    console.log((1/2) * b * h);
  }
}

class Circle extends Shape {
  area(r) {
    console.log(3.14 * r * r);
  }
}

const triangle = new Triangle();
triangle.area(10, 5); // Output: 25

const circle = new Circle();
circle.area(7); // Output: 153.86
```

3. Multilevel Inheritance is a process of deriving a class from another derived class.

```javascript
class Shape {
  area() {
    console.log("Displays Area of Shape");
  }
}

class Triangle extends Shape {
  area(h, b) {
    console.log((1/2) * b * h);
  }
}

class EquilateralTriangle extends Triangle {
  constructor(side) {
    super();
    this.side = side;
  }

  area() {
    console.log((Math.sqrt(3) / 4) * this.side * this.side);
  }
}

const equilateralTriangle = new EquilateralTriangle(5);
equilateralTriangle.area(); // Output: 10.825317547305486
```

4. Hybrid Inheritance is a combination of simple, multiple inheritance and hierarchical inheritance. JavaScript does not support multiple inheritance directly, but we can achieve similar behavior using mixins.

```javascript
class Shape {
  area() {
    console.log("Displays Area of Shape");
  }
}

class Triangle extends Shape {
  area(h, b) {
    console.log((1/2) * b * h);
  }
}

class Circle extends Shape {
  area(r) {
    console.log(3.14 * r * r);
  }
}

const mixin = (Base) => class extends Base {
  perimeter() {
    console.log("Calculates Perimeter");
  }
};

class EquilateralTriangle extends mixin(Triangle) {
  constructor(side) {
    super();
    this.side = side;
  }

  area() {
    console.log((Math.sqrt(3) / 4) * this.side * this.side);
  }
}

const equilateralTriangle = new EquilateralTriangle(5);
equilateralTriangle.area(); // Output: 10.825317547305486
equilateralTriangle.perimeter(); // Output: Calculates Perimeter
```

## ▶️ Method Overriding

If the  same method is defined in both the superclass and the subclass, then the method of the subclass class overrides the method of the superclass 

- General

```js
class human {
    constructor(name , age , body_type) {
        this.name = name
        this.age = age
        this.body_type = body_type
    }

    getName() {
        console.log("The name of the human is : ", this.name)
    }

    getAge() {

        console.log("The age of the human is :", this.age)
    }

    getBodyType() {
        console.log("The body type of the human is :", this.body_type)
    }
}

class student extends human {}

const student_1 = new student("Subham" , 24 , "Thin")

student_1.getAge() //The age of the human is : 24
```
### ⭐ Super Keyword - Types

The super keyword is used to call the parent class's constructor to access its properties and methods.

#### Overriding the Constructor

```js
class Human {
    constructor(name, age, bodyType) {
        this.name = name;
        this.age = age;
        this.bodyType = bodyType;
    }

    getName() {
        console.log("The name of the human is:", this.name);
    }

    getAge() {
        console.log("The age of the human is:", this.age);
    }

    getBodyType() {
        console.log("The body type of the human is:", this.bodyType);
    }
}

class Student extends Human {
    constructor() {
        super("Rahul", 80, "Fat");
    }
}

const student1 = new Student();

student1.getName(); // The name of the human is: Rahul
```
#### Overriding a Method


```js
class Human {
    constructor(name, age, bodyType) {
        this.name = name;
        this.age = age;
        this.bodyType = bodyType;
    }

    getName() {
        console.log("The name of the human is:", this.name);
    }

    getAge() {
        console.log("The age of the human is:", this.age);
    }

    getBodyType() {
        console.log("The body type of the human is:", this.bodyType);
    }
}

class Student extends Human {
    constructor() {
        super("Rahul", 80, "Fat");
    }

    // Overriding using super keyword in child class
    getAge() {
        super.getAge();
        console.log("The age of the student is:", 20);
    }
}

const student1 = new Student();

student1.getAge(); // The age of the human is: 80
                   // The age of the student is: 20

```
### ⭐ Key Points of Method Overriding

1. **Same Method Name**: The method in the child class must have the same name as in the parent class.

2. **Same Parameters**: The method in the child class must have the same parameter list as the parent class method.

3. **IS-A Relationship**: Method overriding only occurs in two classes that have an IS-A relationship (inheritance).

4. **Access Modifiers**: The overriding method can have a less restrictive access modifier, but not a more restrictive one.

5. **Super Keyword**: You can use the `super` keyword to call the overridden method from the parent class.

### ⭐ Extra Notes
#### Note 1
```js
class human {
    constructor() {
        console.log("Human class constructor")
    }
    eat() {
        console.log("Human can eat")
    }
}
class student extends human {
}
const student_1 = new student()
student_1.eat()

//Human class constructor
// Human can eat
```

If you don’t explicitly define a constructor in a subclass, JavaScript will automatically create one for you that calls the parent class’s constructor using super().
like this

```js
class human {
    constructor() {
        console.log("Human class constructor")
    }
    eat() {
        console.log("Human can eat")
    }
}
class student extends human {
    constructor(...arg) {
        super(...arg);
    }
}
const student_1 = new student()
student_1.eat()
```

#### Note 2


```js
class human {
    constructor() {
        console.log("Human class constructor")
    }
    eat() {
        console.log("Human can eat")
    }
}
class student extends human {
    constructor() {
        console.log("This is student class constructor")
    }
}
const student_1 = new student()
student_1.eat()

// console.log("This is student class constructor")
//ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor

```

You have to use super keyword like this

```js
class human {
    constructor() {
        console.log("Human class constructor")
    }
    eat() {
        console.log("Human can eat")
    }
}
class student extends human {
    constructor() {
        super()
        console.log("This is student class constructor")
    }
}
const student_1 = new student()
student_1.eat()
```

#### Note 3

```js
class human {
    constructor(name) {
        console.log("Human class constructor" , name)
        this.name = name
    }
    eat() {
        console.log("Human can eat")
    }
}
class student extends human {
    constructor(name) {
        this.name = name //not allow
        super()
        console.log("Student class constructor" , name)

    }
}
const student_1 = new student("subham")
student_1.eat()

// this.name = name
// ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
```
After super keyword you can use this

```js
class human {
    constructor(name) {
        console.log("Human class constructor" , name)
        this.name = name
    }
    eat() {
        console.log("Human can eat")
    }
}
class student extends human {
    constructor(name) {
        super()
        this.name = name
        console.log("Student class constructor" , name)

    }
}
const student_1 = new student("subham")
student_1.eat()

// Human class constructor undefined
// Student class constructor subham
// Human can eat
```
## ▶️ Method Overloading

Having two or more methods (or functions) in a class with the same name and different arguments (or parameters)

### ⭐ Can We Overload a Function in JavaScript?
In JavaScript, method overloading as seen in some other languages (like Java) is not natively supported. This means you cannot define multiple methods with the same name but different parameters in the same class. However, you can achieve similar functionality using techniques like checking the number and type of arguments within a single method.


You can't do this in JS

```js
class Calculator {
    add(a, b) {
        return a + b;
    }

    add(a, b, c) {
        return a + b + c;
    }
}

const calc = new Calculator();
console.log(calc.add(1, 2)); // This will throw an error because the first add method is overwritten
```
If you want, you can achieve by doing this
```js
class Calculator {
    add(...args) {
        if (args.length === 2) {
            return args[0] + args[1];
        } else if (args.length === 3) {
            return args[0] + args[1] + args[2];
        } else {
            throw new Error("Invalid number of arguments");
        }
    }
}

const calc = new Calculator();

console.log(calc.add(1, 2)); // Output: 3
console.log(calc.add(1, 2, 3)); // Output: 6
```


## ▶️ Access Modifiers


 Access modifier is a keyword that is used to set the accessibility of a class member 

### ⭐ Types of Access Modifiers

1. **Public**: Members declared as public are accessible from any other class.
2. **Protected**: Members declared as protected are accessible within the same class and by derived class instances.
3. **Private**: Members declared as private are accessible only within the same class.

### ⭐ Accessibility Table

| Modifier      | Parent Class | Child Class | Outside Class |
|---------------|--------------|-------------|---------------|
| **Public**    | ✔️           | ✔️          | ✔️            |
| **Protected** | ✔️           | ✔️          | ❌             |
| **Private**   | ✔️           | ❌           | ❌             |

### ⭐ Example

#### 1. Public Members

Public members are accessible from anywhere.

```javascript
class Parent {
    publicProperty = "I'm public";

    publicMethod() {
        return "This is a public method";
    }
}

class Child extends Parent {
    useParentPublic() {
        console.log(this.publicProperty);
        console.log(this.publicMethod());
    }
}

const parent = new Parent();
const child = new Child();

console.log(parent.publicProperty);  // Output: I'm public
console.log(parent.publicMethod());  // Output: This is a public method
child.useParentPublic();
// Output: 
// I'm public
// This is a public method
```

In this example, `publicProperty` and `publicMethod` are accessible from:
- Within the Parent class
- Within the Child class
- Outside any class

#### 2. Protected Members (Simulated)

In JavaScript, we use an underscore prefix to indicate protected members by convention. They're still technically public, but developers agree not to access them directly outside the class or its subclasses.

```javascript
class Parent {
    _protectedProperty = "I'm protected";

    _protectedMethod() {
        return "This is a protected method";
    }
}

class Child extends Parent {
    useParentProtected() {
        console.log(this._protectedProperty);
        console.log(this._protectedMethod());
    }
}

const parent = new Parent();
const child = new Child();

child.useParentProtected();
// Output:
// I'm protected
// This is a protected method

// These work, but violate the convention:
console.log(parent._protectedProperty);
console.log(parent._protectedMethod());
```

In this scenario:
- `_protectedProperty` and `_protectedMethod` are accessible within Parent
- They're also accessible within Child (inheritance)
- They're technically accessible outside, but this violates the convention

#### 3. Private Members

Private members are truly private and only accessible within the class they're defined in.

```javascript
class Parent {
    #privateProperty = "I'm private";

    #privateMethod() {
        return "This is a private method";
    }

    usePrivate() {
        console.log(this.#privateProperty);
        console.log(this.#privateMethod());
    }
}

class Child extends Parent {
    tryToUseParentPrivate() {
        // These would cause errors if uncommented:
        // console.log(this.#privateProperty);
        // console.log(this.#privateMethod());
    }
}

const parent = new Parent();
const child = new Child();

parent.usePrivate();
// Output:
// I'm private
// This is a private method

// These would cause errors:
// console.log(parent.#privateProperty);
// console.log(parent.#privateMethod());
// child.tryToUseParentPrivate();
```

In this case:
- `#privateProperty` and `#privateMethod` are only accessible within Parent
- They're not accessible in Child, even though it extends Parent
- They're not accessible outside the class at all

#### Key Takeaways

1. Public members (default) are accessible everywhere.
2. Protected members (convention with `_`) are accessible within the class and subclasses, but shouldn't be accessed outside (though technically they can be).
3. Private members (with `#`) are only accessible within the defining class, not in subclasses or outside.
4. When using protected members, they behave like public members in terms of accessibility, but developers agree to treat them as if they were protected.
5. True privacy and encapsulation are only achieved with private members using the `#` syntax.

## ▶️ Static

The static keyword defines a static method or field for a class

A static method is a method that belongs to the class itself, not to any specific instance of the class.


```javascript
class Animal {
    constructor(name) {
        this.name = Animal.capitalize(name);
    }

    static capitalize(name) {
        return name.charAt(0).toUpperCase() + name.slice(1);
    }

    walk() {
        console.log(`Animal ${this.name} is walking`);
    }
}

const animal = new Animal("lion");
animal.walk(); // Output: Animal Lion is walking

console.log(Animal.capitalize("elephant")); // Output: Elephant
```

Key points:
1. The `capitalize` method is declared as static using the `static` keyword.
2. It's called on the class (`Animal.capitalize`) not on instances.
3. It can be used inside the constructor or other methods using the class name.

### ⭐ Inheritance and Static Methods

Static methods are inherited by subclasses:

```javascript
class Human extends Animal {
    static greet() {
        console.log("Hello!");
    }
}

const human = new Human("john");
human.walk(); // Output: Animal John is walking

console.log(Human.capitalize("sarah")); // Output: Sarah
Human.greet(); // Output: Hello!
```

Note:
1. The `Human` class inherits the static `capitalize` method from `Animal`.
2. `Human` can also define its own static methods, like `greet`.

### ⭐ Calling Static Methods from Non-Static Methods

You can call static methods from non-static methods, but you need to use the class name:

```javascript
class Calculator {
    static add(a, b) {
        return a + b;
    }

    multiply(a, b) {
        // Using a static method in a non-static method
        return Calculator.add(a, 0) * b;
    }
}

const calc = new Calculator();
console.log(calc.multiply(3, 4)); // Output: 12
console.log(Calculator.add(5, 6)); // Output: 11
```

### ⭐ Static Methods vs. Instance Methods

Here's a comparison to illustrate the difference:

```javascript
class MyClass {
    static staticMethod() {
        return "I'm a static method";
    }

    instanceMethod() {
        return "I'm an instance method";
    }
}

console.log(MyClass.staticMethod()); // Output: I'm a static method

const obj = new MyClass();
console.log(obj.instanceMethod()); // Output: I'm an instance method

// This would throw an error:
// console.log(MyClass.instanceMethod());

// This would also throw an error:
// console.log(obj.staticMethod());
```

### ⭐  Use Cases for Static Methods

1. **Utility Functions**: Methods that don't require object state.
2. **Factory Methods**: Creating instances with special properties.
3. **Cache or Fixed-Configuration**: Storing shared data for all instances.

Example of a factory method:

```javascript
class User {
    constructor(name, role) {
        this.name = name;
        this.role = role;
    }

    static createAdmin(name) {
        return new User(name, "admin");
    }
}

const admin = User.createAdmin("Alice");
console.log(admin.role); // Output: admin
```

### ⭐ Key Takeaways

1. Static methods are defined on the class, not instances.
2. They're called using the class name: `ClassName.methodName()`.
3. They can be inherited by subclasses.
4. They can't directly access instance properties or methods.
5. They're useful for utility functions, factory methods, and managing class-level data.
6. You can't call static methods on instances, and you can't call instance methods on the class.


## ▶️ Getter & Setter


 Getters and setters are functions that allow you to get and set object values, respectively

```js
//getter setter
class human {
    constructor(name, age) {
        this._name = name;
    }
    get getName() {
        return this._name;
    }
    set setName(name) {
        this._name = name;
    }
}

const person = new human("", 0);
person.setName = "Raj";
person.setAge = 25;

console.log(person.getName);
console.log(person.getAge);

//Raj
//25
```
## ▶️ instanceOf Operator

 Check if an object is an instance of a class, subclass, or interface 

```js
//getter setter
class human {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    get getName() {
        return this.name;
    }
    set setName(name) {
        this.name = name;
    }
    get getAge() {
        return this.age;
    }
    set setAge(age) {
        this.age = age;
    }
}

const person = new human("", 0);
person.setName = "Raj";
person.setAge = 25;

console.log(person.getName);
console.log(person.getAge);

const person1 = "Subham"

console.log( person instanceof human)//true
console.log( person1 instanceof human)//false
```

It also returns true for subclass

```js
//getter setter
class human {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    get getName() {
        return this.name;
    }
    set setName(name) {
        this.name = name;
    }
    get getAge() {
        return this.age;
    }
    set setAge(age) {
        this.age = age;
    }
}

class Coder extends human {
    constructor(name, age, language) {
        super(name, age);
        this.language = language;
    }
}

const person = new human("", 0);
const subham = new Coder("subham", 22, "java");
person.setName = "Raj";
person.setAge = 25;


console.log( person instanceof human)
console.log( subham instanceof human)
```




## ▶️ Encapsulation

Encapsulation is a way to restrict the direct access to some components of an object

```js
class BankAccount {
    #balance; // Private field

    constructor(initialBalance) {
        this.#balance = initialBalance;
    }

    deposit(amount) {
        if (amount > 0) {
            this.#balance += amount;
        }
    }

    getBalance() {
        return this.#balance;
    }
}

const account = new BankAccount(1000);
account.deposit(500);
console.log(account.getBalance()); // 1500
// console.log(account.#balance); // Syntax error: private field
```


```js
//Encapsulation
const user = {
    firstName: "John",
    lastName: "Doe",
    age: 25,
    getAgeYear: function() {
        return new Date().getFullYear() - this.age;
    }
}
console.log(user.getAgeYear());
```

## ▶️ Polymorphism

Polymorphism means "many forms", and it occurs when we have many classes that are related to each other by inheritance.


```js
// Parent class
class Animal {
  makeSound() {
    console.log("The animal makes a sound");
  }
}

// Child classes
class Dog extends Animal {
  makeSound() {
    console.log("The dog barks");
  }
}

class Cat extends Animal {
  makeSound() {
    console.log("The cat meows");
  }
}

// Function to demonstrate polymorphism
function animalSound(animal) {
  animal.makeSound();
}

// Usage
const animal = new Animal();
const dog = new Dog();
const cat = new Cat();

animalSound(animal); // Output: The animal makes a sound
animalSound(dog); // Output: The dog barks
animalSound(cat); // Output: The cat meows
```
## ▶️ Abstraction

Abstraction is the concept of hiding complex implementation details and showing only the necessary features of an object.


```js
// Abstraction: Hiding complex implementation details and showing only the necessary features of an object.

// Abstract class
class Vehicle {
    constructor(brand) {
        this.brand = brand;
    }

    // Abstract method
    start() {
        throw new Error("Method 'start()' must be implemented.");
    }

    getBrand() {
        return this.brand;
    }
}

// Concrete class
class Car extends Vehicle {
    start() {
        return `${this.brand} car is starting...`;
    }
}

// Usage
const myCar = new Car("Toyota");
console.log(myCar.getBrand()); // Output: Toyota
console.log(myCar.start());    // Output: Toyota car is starting...
```
