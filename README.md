## FP :: TERMS
### 1 - Pure Function  
  - Given the same input, always returns the same output.
  - Produces no side effects. // console.log is side effect.
### 2 - Idempotent
### 3 - Imperative vs Declarative :: example --> { Computser vs Human || fro vs foreach } 
### 4 - Immutability (Structural Sharing) :: 
#### 5 - Currying
  > Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c).
    Currying doesn’t call a function. It just transforms it.
    
 **Example**
  ```
   //Currying
   const multiply = (a, b) => a * b
   const curriedMultiply = (a) => (b) => a * b
   curriedMultiply(5)(20)
   const multiplyBy5 = curriedMultiply(5)
   multiplyBy5(20)
   ```
#### 6 - Partial Application : :

**Example**
```
    const multiply = (a, b, c) => a * b * c
    const partialMultiplyBy5 = multiply.bind(null, 5)
    partialMultiplyBy5(10, 20)
 ```
#### 7 - Compose && Pipe : :

##### Reduce Example : :
```
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

```
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
