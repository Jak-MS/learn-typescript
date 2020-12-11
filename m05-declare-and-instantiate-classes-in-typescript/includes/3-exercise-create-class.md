To create a class, define its members: properties, a `constructor`, accessors, and methods.

- Properties, also referred to as fields, are the data (or attributes) for the object. These are the defining characteristics of the object that you can set or return from your code.

- The ``constructor`` is a special function used to create and initialize objects based on the class. When you create a new instance of the class, the constructor creates a new object with the class shape and initializes it with the values passed to it.

- Accessors are a type of function that you use to ``get`` or ``set`` the value of properties. Properties can be read-only by simply omitting the set accessor in the class, or inaccessible by omitting the get accessor (the property will return `undefined` if you attempt to access it, even if it's assigned a value during initialization.)

- Methods are functions that define the behaviors or actions that the object can do. You can call these methods to invoke the behavior of the object. You can also define methods that are only accessible from within the class itself and are typically called by other methods in the class to perform a task.

Let's open the [Playground](https://www.typescriptlang.org/play) and create a new class called `````Car`````. You can use the Car class on its own to create basic Car objects, or you can extend the Car class to create new classes for specific types of cars, like a `GasCar` or `ElectricCar` class. These properties will inherit the properties and methods of the Car class, as well as have their own properties and methods.

1. Create a new `class` by using the class keyword followed by the class name, `Car`. By convention, class names are CamelCase. Let's also add some comments to make it easier to add the class members in the correct places.

```typescript
class Car {

    // Properties

    // Constructor

    // Accessors

    // Methods

}

```

## Declare the class properties

You can think of the properties of a class as the raw data that is passed to the object when it's initialized.

The properties of the `Car` class are those that apply to any car, regardless of the specific make or model. For example, these properties may include the make of the car, the color, and the number of doors. Because you're working in TypeScript, you can also apply type attributes to the properties.

1. Declare the three properties for the `Car` class: `_model: string`, `_color: string`, and `_doors: number`.

```typescript
// Properties

_make: string;

_color: string;

_doors: number;

```

## Define the class constructor

Classes in TypeScript create two separate types: the instance type, which defines what members an instance of a class has, and the ```constructor``` function type, which defines what members the class constructor function has. The constructor function type is also known as the "static side" type because it includes static members of the class.

Using a `constructor` can simplify classes and make them easier to manage when you're working with many classes.

A constructor function initializes the properties of the class and has three parts:

- The `constructor` keyword.

- A parameter list, which defines the parameters that will be passed to the new object when a new instance is created. When defining the parameter list, remember that:

  - It is not required to define a parameter for every property in the class.

  - As with all TypeScript functions, the parameters can be required or optional, have default values, or be rest parameters. (This is a key difference from JavaScript.)

  - The parameter names can be different from the property names. Keep in mind that these names will appear in Intellisense when you work with objects of this type so use names that are sufficiently descriptive.

- The property assignments. Each statement assigns the value of a parameter to the value of a property. To indicate that you are accessing a member of the class (in this case, the property), apply the `this.` keyword.

A class may contain at most one ```constructor``` declaration. If a class contains no constructor declaration, an automatic constructor is provided.

Continue defining the `Car` class in the Playground.

1. Create the ``constructor`` for the ```Car``` class. Start with the constructor keyword and then define the parameters and types that will be passed to the new Car object when a new instance is created. For the Car class, define one parameter for each of the three properties and annotate it with the type. Make the `doors` parameter optional with a default value of `4`.

1. Inside the code block for the constructor, assign a parameter value to each property (for example, `this._make = make`). In this case, you'll just set it to the value of the associated parameter but note that you can assign any expression that returns the required type.

```typescript
// Constructor

constructor(make: string, color: string, doors = 4) {

    this._make = make;

    this._color = color;

    this._doors = doors;

}

```

> [!TIP]
> TIP  The underscore (_) before the property name is not required in the property declaration but it provides a way to distinguish the property declaration from the parameters that are accessible through the constructor, while still tying the two together visually.
## Define the accessors

While you can access the class properties directly (they are `public`, by default), TypeScript supports getters/setters as a way of intercepting access to a property. This gives you finer-grained control over how a member is accessed on each object.

To `set` or return the value of the object's members from code, you must define `get` and set accessors in the class.

Continue defining the `Car` class in the Playground.

1. Define a `get` block for the `make` parameter that returns the value of the `_make` property.

```typescript
// Accessors

get make() {

    return this._make;

}

```

1. Define a `set` block for the ``make`` parameter that sets the value of the `_make` property to the value of the make parameter.

```typescript
set make(make) {

    this._make = make;

}

```

1. You can also use ``get`` and ``set`` blocks to validate data, impose constraints, or perform other manipulation of the data before you return it to the program. Define get and set blocks for the `color` parameter, but this time, return a string concatenated to the value of the `_color` property.

```typescript
get color() {

    return 'The color of the car is ' + this._color;

}

set color(color) {

    this._color = color;

}

```

1. Define `get` and `set` blocks for the ``doors`` parameter. Before returning the value of the `_doors` property, verify that the value of the doors parameter is an even number. If not, throw an error.

```typescript
get doors() {

    return this._doors;

}

set doors(doors) {

    if ((doors % 2) === 0) {

        this._doors = doors;

    } else {

        throw new Error('Doors must be an even number');

}

```

## Instantiate a class

At this point, you have a class named ```Car``` that has three properties, and you can get and set the value of those properties. Now, you can instantiate the Car class using the `new` keyword and pass parameters to it, creating a new Car object.

Continue working in the Playground.

1. Below the class declaration, declare a variable called `my`Car`1` and assign a new Car object to it, passing in values for the `make`, `color`, and ``doors`` parameters (make sure that the doors parameter is assigned an even number.)

```typescript
let myCar1 = new Car('Honda', 'blue', 2);  // Instantiates the Car object with all parameters

```

1. You can now access the properties of the new `myCar1` object. Enter `myCar1.` and you should see a list of the members defined in the class, including `color` and `_color`. Return the value of both properties to the console. What happens? Why?

```typescript
console.log(myCar1.color);

console.log(myCar1._color);

```

1. The member `_``color``` represents the property defined in the class, while color is the parameter that you pass to the constructor. When you refer to `_color`, you're accessing the raw data for the property, which returns `'blue'`. When you refer to color, you're accessing the property through the `get` or `set` accessor, which returns `'The color of the car is blue'`. It's important to understand the difference between the two because you often do not want to allow direct access to the property without doing some validation or other work on the data before getting or setting it. You'll learn about using access modifiers to control the visibility of class members later in the unit.

1. Recall that the `set` block for the ```doors``` parameter tests the value to determine if it is even or odd. Test this by declaring a variable called `my`Car`2` and assigning a new Car object to it, passing in values for the `make`, `color`, and doors parameters. This time set the value of the doors parameter to an odd number. Now, run the code. What happens? Why?

```typescript
let myCar2 = new Car('Toyota', 'red', 3);

```

1. Although you passed an odd number to ``doors``, it compiles and runs without errors because no data validation occurs in the ``constructor``. Try `set`ting the value of doors to another odd number (for example, `my`Car`2.doors = 5`) and test it. This should invoke the set block and throw an error. If you want to perform this validation step when the Car object is initialized, you should add a validation check to the constructor.

```typescript
constructor(make: string, color: string, doors?: number) {

    this._make = make;

    this._color = color;

    if ((doors % 2) === 0) {

        this._doors = doors;

    } else {

        throw new Error('Doors must be an even number');

    }

}

```

1. Finally, test the optional parameter `doors` by omitting it from the object initialization.

```typescript
let myCar3 = new Car('Ford', 'gray');

console.log(myCar3.doors);  // returns 4, the default value

```

## Define the class methods

You can define any TypeScript function within a class and call it as a method on the object or from other functions within the class. These class members describe the behaviors that your class can perform and can perform any other tasks required by the class.

Continue defining the `Car` class in the Playground.

1. Define these four methods for the `Car` class: `accelerate`, `brake`, `turn`, and `worker`. You'll notice that there is no `function` keyword. This is not required or allowed when defining functions in a class, so it helps you keep the syntax succinct.

```typescript
// Methods

accelerate(speed: number): string {

    return this.worker() + " is accelerating to " + speed + " MPH."

}

brake(): string {

    return this.worker() + " is braking with the standard braking system."

}

turn(direction: 'left' | 'right'): string {

    return this.worker() + " is turning " + direction;

}

// This function performs work for the other method functions

worker(): string {

    return this._make;

}

```

1. Test the methods by sending the return value to the console.

```typescript
console.log(myCar1.accelerate(35));

console.log(myCar1.brake());

console.log(myCar1.turn('right'));

```

## Work with access modifiers

All class members are public, by default. This means that they are accessible from outside of the containing class. You saw an example of this earlier when you returned the value of two members of the `Car` class: the `_`color`` (a property defined in the class) and color (a parameter defined in the `constructor`.) Sometimes it is desirable to provide access to both, but you will typically want to control access to the raw data contained in the property by only allowing access through the `get` or `set` accessor.

You can also control access to method functions. For example, the `Car` class contains a function called `worker` that is only called from other method functions within the class. Calling this function directly from outside of the class may cause undesirable results.

In TypeScript, you can control the visibility of class members by adding the `public`, `private`, or `protected` keyword before the member name.

| Access modifier| Description|
| :--- | :--- |
| public| If you don't specify an access modifier, the default is public. You can also explicitly set the member to public by using the public keyword.|
| private| If you modify the member with the private keyword, it cannot be accessed from outside of its containing class.|
| protected| The protected modifier acts much like the private modifier with the exception that members declared protected can also be accessed within deriving classes. (You'll learn more about this later in the module.)|

In addition, properties can be made `readonly` by using the readonly modifier. Readonly properties may only be set when initialized at their declaration or in the `constructor`.

Continue defining the `Car` class in the Playground.

1. Test the access of the class members by typing `myCar1.` and notice that all the members appear in the list, including the properties, the `constructor` parameters, the methods, and the `worker` function.

![Intellisense showing all of the public members of the Car class: _color, _doors, _make, accelerate, brake, color, doors, make, turn, and worker.](../media/m05_public_private.jpg)


1. Set the access modifier of the `_color`, `_doors`, and `_make` properties and the `worker` function to `private`.

```typescript
// Properties

private _make: string;

private _color: string;

private _doors: number;

// ...

private worker(): string {

    return this._make;

}

```

1. Test the access of the class members again by typing `myCar1.` and notice that the properties and the `worker` function are now unavailable. Any attempt to use the class member will raise an error at compile time, for example, **Property '_color' is private and only accessible within class 'Car'.**

![Intellisense showing all of the public members of the Car class with properties and the worker method set to private: accelerate, brake, color, doors, make, and turn.](../media/m05_public_private_2.jpg)


> [!NOTE]
> NOTE  TypeScript is a structural type system. When you compare two different types, regardless of where they came from, if the types of all members are compatible, then we say the types themselves are compatible. However, when comparing types that have private and protected members, these types are treated differently. For two types to be considered compatible, if one of them has a private member, then the other must have a private member that originated in the same declaration. The same applies to protected members.