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

### Map

In JavaScript, we can’t overload the equality operator, and the two objects,
even though they have the same content, are always considered different. This isn’t
the case with other languages, such as Java and C#, so be careful!

### Set

Check out the ```...``` operator.

## Ch.10 Wrangling regular expressions

The literal syntax is preferred when the regex is known at development
time, and the constructor approach is used when the regex is constructed at
runtime by building it up dynamically in a string.

One of the reasons that the literal syntax is preferred over expressing regexes in a
string is that (as you’ll soon see) the backslash character plays an important part in
regular expressions. But the backslash character is also the escape character for string
literals, so to express a backslash within a string literal, we need to use a double backslash
(\\). This can make regular expressions, which already possess a cryptic syntax,
even more odd-looking when expressed within strings.

In addition to the expression itself, five flags can be associated with a regex:

* i—Makes the regex case-insensitive, so /test/i matches not only test, but also
Test, TEST, tEsT, and so on.
* g—Matches all instances of the pattern, as opposed to the default of local, which
matches only the first occurrence. More on this later.
* m—Allows matches across multiple lines, as might be obtained from the value of
a textarea element.
* y—Enables sticky matching. A regular expression performs sticky matching in
the target string by attempting to match from the last match position.
* u—Enables the use of Unicode point escapes (\u{...}).

These flags are appended to the end of the literal (for example, ```/test/ig```) or passed
in a string as the second parameter to the RegExp constructor (```new RegExp("test",
"ig")```)

## Ch.12 Working the DOM

The style object doesn’t reflect any style information inherited from CSS style sheets.

It should be noted that any values in an element’s style property take precedence over
anything inherited by a style sheet (even if the style sheet rule uses the !important
annotation).

React’s virtual DOM
> One of the most popular client-side libraries is Facebook’s React (https://
facebook.github.io/react/). React achieves great performance by using a virtual
DOM, a set of JavaScript objects that mimic the actual DOM. When we develop
applications in React, we perform all modifications on the virtual DOM, without any
regard for layout thrashing. Then, at an appropriate time, React uses the virtual DOM
to figure out what changes have to be made to the actual DOM, in order to keep the
UI in sync. This batching of updates increases the performance of applications.

## Ch.13 Surviving events

An event-loop task represents an action performed by the browser. Tasks are
grouped into two categories:
* Macrotasks are discrete, self-contained browser actions such as creating the
main document object, handling various events, and making URL changes.
* Microtasks are smaller tasks that should be executed as soon as possible.
Examples include promise callbacks and DOM mutation changes.

In Netscape’s event model, the event handling starts with the top element and
trickles down to the event target element. In our case, the event handlers would be
executed in the following order: document click handler, outerContainer click handler,
and finally innerContainer click handler. This is called event capturing.

Microsoft chose to go the other way around: start from the targeted element and
bubble up the DOM tree. In our case, the events would be executed in the following
order: innerContainer click handler, outerContainer click handler, and document
click handler. This is called event bubbling.


```
outerContainer.addEventListener("click", function(event){
  report("innerContainer handler");
  assert(this === outerContainer,
    "This refers to the outerContainer");
  assert(event.target === innerContainer,
    "event.target refers to the innerContainer");
});
```
Within the outerContainer handler, if we’re handling the event originating on the
innerContainer, this will refer to the outerContainer and event.target to innerContainer.

This level of decoupling helps to keep code modular, easier to write, and a lot
easier to debug when something goes wrong. It also makes it easy to share portions
of code and to move them around without fear of violating a coupled dependency
between the code fragments. Decoupling is a fundamental advantage when using
**custom events** in code, and it allows us to develop applications in a much more
expressive and flexible manner.
