#WWF-UK Javascript Style guide

This document draws heavily from the following guides written by smarter people than me:

- https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
- http://javascript.crockford.com/code.html
- https://github.com/airbnb/javascript

It should be considered as both draft *and* canonical. Draft because I'm open to a debate on the practices defined. Canonical because in the absence of that debate the guidance here should be reflected in your code.

##tl;dr
- Use .js files
- "use strict"
- Use jshint
- Use camelCaseVariableNamesIcanUnderstand
- Avoid global variables
- Do not use `eval`
- Do Use `===`

##Javascript Files
Use them for anything other than short snippets or code that is specific to that particular page view. They can be loaded in parallel miniifed and cached. It also makes it easier to lint your code.

##Strict mode
Adding `"use strict"` to the start of a function tells the browser to use strict mode. This will make the browser fussier with you code - more errors reported = more predictable code. For example this code will give you "Uncaught ReferenceError: watsInTheTin is not defined" with strict mode but without it you'll just be wondering where your sausages went.

```javascript
function foo() {
    var whatsInTheTtin = 'beans';
    watsInTheTin = whatsInTheTtin + ' and sausages';
    return whatsInTheTtin;
}
```
##Spacings
Spaces around `=`, `+`, and `-` etc makes things more readable:

```javascript
function foo() {
    var something = 1,
        somethingElse = 1 + (2 * something);
}
````

##Indentation
Spaces. Multiples of four.

##Line Length
Try to keep lines under about 80 character.
Here are some strategies:

###Long strings should be built like this:
```javascript
var pandaIntro = 'This charismatic and universally-loved species – the' +
    'symbol of our organisation – is one of the rarest and most' +
    'endangered bears in the world.';
```
###Methods should be chained like this:
```javascript
$('.pandas')
    .find('.wild-pandas')
        .count()
        .countAgain()
        .addToSurvey()
    .end()
    .find('.baby-pandas')
        .count()
        .countAgain()
        .addToSurvey();
```
###Function arguments
Should normally be on one line but if they are very long (which they should be if it helps understand their purpose) then use one per line like so:

```javascript
function foo(
    veryClearlyDescribedArgument,
    anotherEasilyUnderstoodArgument,
    thisOneIsVeryLongToo) {
//...
}
```
##Comments
Comment well, but don't feel the need to over-explain. We all know what `var i=0;` does. Use the prefixes `//FIXME` and `//TODO` where appropriate.
##Variables
Variable names should err on the long and descriptive side. Use camelCaseToSeparate#words (in contrast, filenames should be all lowercase and css classes should be [separated by hyphens](https://github.com/WWF-International/wwf-uk-css-style-guide "WWF-UK CSS style guide") ). Use global variables sparingly. Declare variables at the start of functions with a separate `var` statement for each to aid readability. Start with assigned variables. Use CAPS for constant values (But note that javascript has no real constants). Use `$` as a prefix when you're caching jQuery representations of the DOM object (which is a good idea).

```javascript

var pandas=getPandas();
var $partOfTheDOMImGonnaMessWith = $("#very-important-button");
var TAU=Math.PI*2;
var angleOfPandaUrinatingUpATree;

```
##Semicolons
Use them. I'm very good at forgetting too. JsHint is very good at reminding me.
##if...
if statements get their brackets and braces for clarity eg.

```javascript

if (condition){
    // statements  
} else if {
    // statements
} else {
    // statements
}
```

Use the ternary operator for simple conditional assignments as long as your code is still readable.

```javascript
msg = score > 100 ? 'Great score' : 'Nice try!'

```

If you're considering breaking a ternary operator out into separate lines for readability then an old fashioned `if (valueWeHave === valueWeWant){}` is more readble IMHO.


##eval()
Don't use it.

##Equals or not
Use `===` and `!==`


##Object and Array Literals

Use them for defining new objects and arrays eg `objFoo={foo:'baa'}` or `arrCountMeIn=[5,6,7,8]` rather than `new Object()` or `new Array()`

##Date()
The Date() function accepts input in two forms:
1: a list of integers eg: Date(2016,02,19,20,30) **NOTE** month is zero indexed so 0 = Jan, 1 = Feb, 2 = March
2: A date formatted string, Different browsers support different string formats, however the ECMA standard (http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15 )is of the form  2016-03-19T20:30:00.000Z 

Preference in our javascript should be to use the first form. If the second method is used it should be with the above standard to avoid cross browser compatibility issues.

