## FP :: TERMS
#### 1 - Pure Function  
  - Given the same input, always returns the same output.
  - Produces no side effects. // console.log is side effect.
#### 2 - Idempotent
  - A function is said to be idempotent if it **returns the same output for the same input. or does what we expect it to do** (predictable). Idempotence is different from pure function as it allows side effects.
**Example**
```js
  // even with same input it will give us diffrent output each time.
  const random = (num) => Math.random(num);
  random(5);
  // we give it same input return same result always -- but it have side effect.
  function numberFive(num) {
    console.log(num);
  }
  numberFive(5);
  //
  Math.abs(Math.abs(5)) // Always return same result.
```
#### 3 - Imperative(how to do things - OOP) vs Declarative(what to do -- FP) :: example --> { Computser vs Human || fro vs foreach } 
  - imperative code is where you explicitly spell out each step of how you want something done, whereas with declarative code you merely say what it is that you want done.
#### 4 - Immutability
   - **Mutable (save)** : is a type of variable that can be changed. In JavaScript, only objects and arrays are mutable, not primitive values. (You can make a variable name point to a new value, but the previous value is still held in memory. Hence the need for garbage collection.) A mutable object is an object whose state can be modified after it is created.
      ** Example **
      ```js
        const a = [2, 1, 4, 3];
        console.log(a);
        // output: [2, 1, 4, 3]
        const b= a.sort();
        console.log(b);
        // output: [1, 2, 3, 4]
        console.log(a)
        // output: [1, 2, 3, 4]
      ```
   - **Immutables (save as)** : are the objects/arrays whose state cannot be changed once the object is created. In JavaScript String and Numbers are immutable data types. "A princess kisses a frog hoping it will turn into a handsome prince. The concept of immutability says that a frog will always be a frog."
   - **NOTE** : so how we can change it ?? copying is bad idea because it is not efficient neither with respect of time/space, So there is structural sharing tree/trie (data structure) more performant.
  - **Immutable vs persistent** : persistent we have kind of trace for old versions (we can access old versions -- stay arround).
  - **partiale persistent data structure** : we can back and check old versions without update. all what we can update is last version.
  - **fully persistent data structure** : we can back and update any of past version.
  - **Structural Sharing** : concept related to Immutability -- we share structure of tree between multi version
  - **Libs to implement** : mori - immutablejs (facebook) - 
  - **What is the good part of the immutability? Why do we need to care about the immutability in the first place? Why even bother?**
    Immutability gives stricter control over your data immediately making your code safer and more predictable. In other words, immutable objects allow you to control the interface and data flow in a predictable manner, discovering the changes efficiently. It also makes it easier to implement complex features such as undo/redo, time travel debugging, optimistic updates and rollback, and so on. 
If we talk about the frontend library React, Vue os state management library Redux then immutability can also help achieve better performance by enabling quick and cheap comparisons between versions of the state before and after changes. Components can take advantage of this and intelligently re-render itself only when needed. This can significantly boost performance. 
The main benefits of immutability are predictability, performance, and better mutation tracking.

  1. Predictability
In any application when we work on some front-end libraries, we declare a lot of state in it. We perform the asynchronous action and it updates the original state (mutation). Once the end-user starts using it the updated state will be significantly different from the initial state. Mutating the state hides changes and it creates side effects that can cause several bugs. Debugging becomes hard in such cases.
When you keep your application architecture immutable and mental model simple it becomes easier to predict the data in the state at any given time and then you can rest assured that it won’t create any nasty side effects. 

2. Performance
Creating an immutable object cost memory. How? When you add value to an immutable object you need to create a new object and in this new object, you copy the existing value with the new value which requires additional memory. To reduce memory consumption we use structural sharing.
Whatever update we make it returns new values, but we share the structures internally to reduce memory consumption. For example, if you append to a vector with 100 elements, it doesn’t create a new vector 101 elements long. Only a few small objects are allocated internally.

3. Mutation Tracking
One of the advantages of immutability is that you can optimize your application by making use of reference and value equality. This makes it easy to identify if anything has changed. You can consider the example of state change in the React component. shouldComponentUpdate can be used to check if the state is identical comparing the state object and preventing it from unnecessary rendering. 
Immutability allows you to track the changes that happen to these objects like a chain of events. Variables have new references that are easy to track compared to existing variables. This helps in debugging the code and building the concurrent application. Also, event debuggers help you to replay DOM events with video playbacks that work on tracking mutation. 

  geeksforgeeks - [Why is Immutability so Important in JavaScript?](https://www.geeksforgeeks.org/why-is-immutability-so-important-in-javascript/)
  Anjana Vakil Talk 2017 - [Immutable data structures for functional JS](https://www.youtube.com/watch?v=Wo0qiGPSV-s)
#### 5 - Currying
  > Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c).
    Currying doesn’t call a function. It just transforms it.
   
 - **Arity** : the number of arguments can function take.
 **Example**
  ```js 
   //Currying
   const multiply = (a, b) => a * b
   const curriedMultiply = (a) => (b) => a * b
   curriedMultiply(5)(20)
   const multiplyBy5 = curriedMultiply(5)
   multiplyBy5(20)
```
[Currying in javascript](https://dev.to/cglikpo/currying-in-javascript-1jke)
   
#### 6 - Partial Application : :

**Example**
```js
    const multiply = (a, b, c) => a * b * c
    const partialMultiplyBy5 = multiply.bind(null, 5)
    partialMultiplyBy5(10, 20)
 ```
#### 7 - Compose && Pipe : :

##### Reduce Example : :
```js
const array1 = [1, 2, 3, 4];
const reducer = (previousValue, currentValue) => previousValue + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

##### Functional Programing Demo : :

```js
// compose
const compose = (f,g) => (...args) => f(g(...args));
// reduce
const purchaseItem = (...functionss) => functions.reduce(compose);

const user = {
  name: "abdo",
  pay: "earth",
  cart: [],
  purchases: []
}

purchaseItem(
  emptyUserCart,
  buyItem,
  applyTaxToItems,
  addItemToCart
)(user, {name: 'Tv', price: 120})

function addItemToCart(user, item) {
  const newCart = user.cart.concat(item);
  return Object.assign({}, user, {cart: newCart});
}

fucntion applyTaxToItems(user) {
  const {cart} = user;
  const taxToApply = 1.5;
  // create new array -- not modify previous.
  const newCart = cart.map( cartItem => {
    return {
      name: cartItem.name,
      price: cartItem.price*taxToApply
    }
  });
  return Object.assign({}, user, {cart: newCart});
}

function buyItem(user) { 
  const itemsInCart = user.cart;
  return Object.assign({}, user, { purchases: itemsInCart });
}
function emptyUserCart(user) { 
  return Object.assign({}, user, { cart: [] });
}
```
