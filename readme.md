#WWF-UK Javascript Style guide

This document draws heavily from the following guides written by smarter people than me:

- https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
- http://javascript.crockford.com/code.html
- https://github.com/airbnb/javascript

It should be considered as both draft and canonical. Draft because I'm open to a debate on the practices defined. Canonical because in the absence of that debate the guidance here should be reflected in your code.

##tl;dr
- Use .js files
- "use strict"
- Use jshint
- Use camelCaseVariableNamesIcanUnderstand
- Avoid global variables
- Do not use `eval()`
- Use `===`

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
Spaces around `=`, `+`, and `( variable )` etc makes things more readable:

```javascript
function foo( variable ) {
    var something = 1,
        somethingElse = 1 + 2 * something;
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
    .countagain()
    .addToSurvey();
```
###Function arguments
Should normally be on one line but if they are very long (which they should be if it helps understand their purpose) then use one per line like so:

```javascript
function foo(
    veryClearlyDescribedArgument,
    anotherEasilyUnderstoodArgument,
    thisOneIsVeryLongToo ){
//...
}
```
##Comments
Comment well, but don't feel the need to over-explain. We all know what `var i=0;` does. Use the prefixes `//FIXME` and `//TODO` where appropriate.
##Variables
Use global variables sparingly. Declare variables at the start of functions with a separate `var` statement for each to aid readability. Start with assigned variables. Use CAPS for constant values (But note that javascript has no real constants)

```javascript
var pandas = getPandas();
var TAU = Math.PI*2;
var angleOfPandaUrinatingUpATree;

```
##Semicolons
Use them. I'm very good at forgetting too. JsHint is very good at reminding me.
##if...
if statements get their brackets and braces for clarity eg.

```javascript
if ( condition ){
  // statements  
} else if {
  // statements
} else {
  // statements
}
```

Use the ternary operator for simple conditional assignments as long as your code is still readable.

```javascript
msg = score > 100 ? 'Great score' : 'Nice try';

```
If you're considering breaking a ternary operator out into separate lines for readability then an old fashioned `if ( valueWeHave === valueWeWant ){}` is more readble IMHO.
  
##eval()
Don't use it.

##Equals
Use `===` and `!==`

