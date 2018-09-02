# Secrets of the JavaScript Ninja

The following are notes took from the 2nd edition of this book.

## Ch.4 Function invovation

When invoked with the keyword ```new```, an empty object instance is created and passed to the function as its function context, the ```this``` parameter.

## Ch.7 Object orientation with prototypes

```instanceof``` checks whether the prototype of the right-side function is in the prototype chain of the object on the left.

## Ch.8 Controlling access to objects

Getters and setters allow us to define object
properties that are used like standard object properties, but are methods that can execute
additional code whenever we read or write to a particular property. This is an
incredibly useful feature that enables us to perform logging, validate assignment values,
and even notify other parts of the code when certain changes occur.

When the expression proxy.clan = "Tokugawa" is evaluated, the value Tokugawa
is stored in the daimyo’s clan property because the proxy doesn’t have a
set trap, so the default action of setting the property is carried out on the target,
daimyo object.

## Ch.9 Dealing with collections

### Array

Manually overriding the length property with a lower value deletes the excess items.

If we try to access an index outside those bounds—for example, with ```ninjas[4]``` (remember,
we have only three ninjas!), we won’t get the scary “Array index out of bounds” exception
that we receive in most other programming languages. Instead, undefined is
returned, signaling that there’s nothing there.

Methods to add and remove items:
* ```push``` adds an item to the end of the array.
* ```unshift``` adds an item to the beginning of the array.
* ```pop``` removes an item from the end of the array.
* ```shift``` removes an item from the beginning of the array.

**Performance considerations: pop and push versus shift and unshift**

The pop and push methods only affect the last item in an array: pop by removing the
last item, and push by inserting an item at the end of the array. On the other hand,
the shift and unshift methods change the first item in the array. This means the
indexes of any subsequent array items have to be adjusted. For this reason, push
and pop are significantly faster operations than shift and unshift, and we recommend
using them unless you have a good reason to do otherwise.

```delete``` method only creates a hole in the array. It will return ```undefined``` when accessing the item via indexing. However, using ```splice``` method would remove the item and update the indexes of subsequent items.

```find``` vs ```filter```: ```find``` to find the first array item vs ```filter``` to find multiple items

**Agregating**:

```javascript
const numbers = [1, 2, 3, 4];
const sum = 0;
numbers.forEach(number => {
  sum += number;
});
```

becomes:

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((aggregated, number) =>
  aggregated + number, 0);
```

In JavaScript, we can’t overload the equality operator, and the two objects,
even though they have the same content, are always considered different. This isn’t
the case with other languages, such as Java and C#, so be careful!
