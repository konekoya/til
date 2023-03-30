# Use Object.hasOwn to check Object properties in JavaScript

The `Object.hasOwn()` is a modern JavaScript feature that allows you to check if a given property exists in an object. It's recommended over the `Object.prototype.hasOwnProperty()` function since [it's safer and more intuitive](<https://igorgonchar.medium.com/javascript-hasown-new-way-to-check-if-object-has-property-b93810e47070#:~:text=The%20main%20difference%20is%20that,checks%20only%20the%20object%20itself.&text=hasOwnProperty()%20besides%20focusing%20only,also%20omits%20getters%20and%20setters.>)

For example, if we have a custom object of a person:

```js
const person = {
  name: 'John',
  age: 24,
  gender: 'male',
  bloodType: 'O',
};
```

We can use `Object.hasOwn()` function to check if the `bloodType` property is present in the `person` object:

```js
Object.hasOwn(person, 'bloodType'); // true
```

The above example would have the same result as calling `Object.proptype.hasOwnerProperty.call(person, 'bloodType');`. However, `Object.hasOwn()` is much shorter and more convenient to use.

Here is another example of checking the property in a loop:

```js
const people = [
  {
    name: 'Carly',
    yearOfBirth: 1942,
    yearOfDeath: 1970,
  },
  {
    name: 'Ray',
    yearOfBirth: 1962,
    yearOfDeath: 2011,
  },
  {
    name: 'Jane',
    yearOfBirth: 1912,
    yearOfDeath: 1941,
  },
  {
    name: 'Josh',
    yearOfBirth: 1933,
  },
];

const findTheOldest = (array) =>
  array.filter((person) => Object.hasOwn(person, 'yearOfDeath'));

console.log(findTheOldest(people));
```

References:

- [Object.hasOwn()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn) - MDN docs
- [JavaScript: hasOwn() — new way to check if Object has property](<https://igorgonchar.medium.com/javascript-hasown-new-way-to-check-if-object-has-property-b93810e47070#:~:text=The%20main%20difference%20is%20that,checks%20only%20the%20object%20itself.&text=hasOwnProperty()%20besides%20focusing%20only,also%20omits%20getters%20and%20setters.>)
