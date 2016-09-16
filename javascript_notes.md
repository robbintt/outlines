
### Javascript Reference Notes



#### Understanding: [JavaScript Versions](http://benmccormick.org/2015/09/14/es5-es6-es2016-es-next-whats-going-on-with-javascript-versioning/)


- When you say `Client-Side JavaScript`, people are thinking `ES5`.
- When you say `node.js`, people think `Google's V8 Engine-> Gradual ES6 Coverage`.
- ES6 seems to be a superset of ES5.  I'm not 100% on this one.
- [Another ES6 vs. ES5 resource](https://addyosmani.com/blog/ecmascript-6-resources-for-the-curious-javascripter/)

- `ECMAScript 5` was released in December 2009.
- `ECMAScript 6` was released in June 2015.
- `ECMAScript 7` is slated for Summer 2016.


- [ES6 Changes and Comparison](http://es6-features.org/#Constants)

- [ES6 can be transpiled back to ES5 in a build toolchain](https://en.wikipedia.org/wiki/ECMAScript#6th_Edition). This sounds like a great approach to using ES6 with gulp.

#### Understanding: [Modern node.js](https://en.wikipedia.org/wiki/Node.js#History)
>In September 2015, Node.js v0.12 and io.js v3.3 were merged back together into Node v4.0.[36] This brought V8 ES6 features into Node.js, and a long-term support release cycle.[37] As of 2016, the io.js website recommends that developers switch back to Node.js.[38]

#### Understanding: [JavaScript Engines](https://en.wikipedia.org/wiki/JavaScript_engine)

- [Nitro (in webkit)](https://en.wikipedia.org/wiki/WebKit) supports most of ES6.
- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) supports most of ES6.
- [SpiderMonkey]() is Firefox's javascript engine and it is competing hard against V8 and seems to be winning.
- [arewefastyet 'compare os'](http://arewefastyet.com/#machine=31) tracks some js engines.
- There are a lot of active [javascript engines](https://en.wikipedia.org/wiki/JavaScript_engine#JavaScript_engines).


#### Understanding: [ES6 Browser Support](https://kangax.github.io/compat-table/es6/)

Each browser just depends on its JavaScript Engine.

- Edge 14, Firefox 45, and Chrome 51 support most of ES6.
- Safari 6.1/7 seems to have almost no support.
- Safari 7.1/8 seems to have only 20% coverage.
- Safari 9 has 50% coverage.
- Safari TP supports most of ES6.  What is safari TP?


#### Javascript Refresher:

- [ES6 Reserved Words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)
- [JavaScript 'String' type and String Escapes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#Escape_notation)
- [ES6 Template Literals (previously template strings)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- [MDN JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
- [Comparison Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)
    - Use strict `equals` and `not equals` as much as possible: `===` and `!==`
- [Expressions and Operators (advanced operators)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators) 
- [Functions Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function)
- [Error handling: throw, try, catch, finally](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw) 
- [Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
    - `myarray.push(thingy);` to append `thingy` to the end.
    - `var shifted_thingy = myarray.pop();` to remove the last (rightmost) thingy.
    - `myarray.unshift(thingy);` to left-append `thingy` to the beginning.
    - `var shifted_thingy = myarray.shift();` to remove the leftmost thingy.
    - `shift` and `pop` return the removed value.
    - `push` and `unshift` return the new length of the array.
    - `push` and `unshift` can take multiple arguments.
    - Join array values to make a long string: myarray.join(', ');
    - Combine arrays: `new_array = myarray.concat(another_array);`
    - Find the index of a value in an array: `i = myarray.indexOf('apple');`. If `apple` doesn't exist, return `-1`.
- [Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
    - `var shifted_thingy = myarray.shift();`
    - `for... in` loop for objects. `for (var key in myobject) { console.log(key, " : ", myobject[key]); }`
    - `window` is the global object in the browser.  `document` and `screen` exist inside window but are aliased in the global scope, as far as I understand.
    - View these in the browser console by typing `window` or `document` to view the objects. Also check out `window.location` or `window.location.host` etc.
    - Also: `window.document.head === document.head`. THUS: `Document Object Model`. The document object is your .html, .php, .aspx, etc object.
- [Ellipses / ... / Spread Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)
    - Ellipses are the same as a * operator in python on an argument list.
    - Ellipses supports both modes, in functions and when passing arrays to functions.


#### JavaScript Browser API: [MDN Web API Reference](https://developer.mozilla.org/en-US/docs/Web/reference/API)
- The [Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) is the major Browser API.
- [Global Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
- Three DOM Actions
    - Manipulation: manipulate the elements
    - Traversal: Select a element based on its relation with another element.
    - Events: Listen to a specific event like a mouseclick or keypress and have something execute.
- Create, Remove, and Modify elements:
    - [createElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
    - [appendChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)
    - [removeChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)
    - [textContent](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)
    - [className](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)
    - [HTMLInputElement.type (for adding the type of input to provide, e.g. checkbox etc.)](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement)
- Traverse Elements: 
    - [node.parentNode](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentNode)
	- [querySelector](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelector)
	- [parentnode.children](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)
	- [getElementById](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById)
	- [getElementsByTagname](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName)
	- [getElementsByClassName](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)

- [Use thingy.addEventListener to add events](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
    - e.g. `'click'` event instead of using `onclick`.
- [Element.classList (add, remove, update, check, index an element's classes](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList) 


Special Note on innerText/textContent (from treehouse docs):

- Mozilla didn't implement innerText but has implemented textContent.
- innerText can be used in older versions of Internet Explorer and all versions of Chrome and Safari.
- textContent can be used in Internet Explorer 9 onwards and all other browsers.
- Here's some cross-browser compatible code for the edit button:

```javascript  
  // cross compatible code
  if (typeof editButton.innerText === "undefined")  {
    editButton.textContent = "Edit";
  } else {
    editButton.innerText = "Edit";
  }
```


##### [The four-P's Problem Solving Method] (https://medium.com/@MatHelme/the-four-ps-of-problem-solving-6e15a39a0712#.u6oj4sst7):
    - Preparation: Understand the problem. Think up a high-level solution.
    - Plan: Plan out the solution.
    - Perform: Perform what is required.
    - Perfect: Perfect our solution incrementally. Nothing is ever 'perfect'.





#### [Official React Tutorial](https://facebook.github.io/react/docs/tutorial.html)

- 


#### Resources

[JavaScript Engine in WebKit browsers](https://en.wikipedia.org/wiki/WebKit#JavaScriptCore)
