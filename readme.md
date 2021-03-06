![](https://javascript30.com/images/JS3-social-share.png)

# JavaScript30

Vanilla JavaScript 30 Day Challenge.
Grab the course at [https://JavaScript30.com](https://JavaScript30.com)

### Index
Click :memo: to go each topic

day|topic|memo
|:--:|:--:|:--:|
1|Access to the DOM|[:memo:](#day1-Access-to-the-DOM)
2|Update styles every second|[:memo:](#day2-Update-styles-every-second)
3|CSS Variables|[:memo:](#day3-CSS-Variables)
4|day 4 Array Methods|[:memo:](#day4-Array-Methods)
5|Flexible layout|[:memo:](#day5-flexible-layout)
6|Typeahead|[:memo:](#day6-Typeahead)
7|Array Methods 2|[:memo:](#day7-Array-Methods-2)
8|HTML5 canvas|[:memo:](#day8-HTML5-canvas)
9|dev tools & console tricks|[:memo:](#day9-dev-tools-and-console-tricks)
10|forEach() & MouseEvent()|[:memo:](#day10-forEach-and-MouseEvent)
11|Custom Video Player|[:memo:](#day11-Custom-Video-Player)
12|KONAMI CODE|[:memo:](#day12-KONAMI-CODE)
13|Slide in on Scroll|[:memo:](#day13-Slide-in-on-Scroll)
14|Reference vs Copy|[:memo:](#day14-Reference-vs-Copy)
15|LocalStorage and Event Delegation|[:memo:](#day15-LocalStorage-and-Event-Delegation)
16|Mouse Move Shadow|[:memo:](#day16-Mouse-Move-Shadow)
17|Sort Without Articles|[:memo:](#day17-Sort-Without-Articles)
18|Adding Up Times with Reduce|[:memo:](#day18-Adding-Up-Times-with-Reduce)

## day1 Access to the DOM
![image](https://user-images.githubusercontent.com/26381972/71702379-7f678080-2e12-11ea-8c7d-7971a3199c2c.png)
#### 1. To access to the DOM element
- `Document.querySelector()`
  - Returns the first Element node within the document, in document order, that matches the specified selectors.
- `Document.querySelectorAll()`
  - Returns a list of all the Element nodes within the document that match the specified selectors.
#### 2. To add event
: The EventListener interface represents an object that can handle an event dispatched by an EventTarget object.
- `EventTarget.addEventListener(type, listener)`
  - `type`: a keyword that represent event type to listen for.
  - `listener`: EventListener interface || JS function
- `window.addEventListener('keydown', playSound)`
  - if `keydown` event occurs play a listener `playSound`

## day2 Update styles every second
![image](https://user-images.githubusercontent.com/26381972/71702821-d8381880-2e14-11ea-90bc-8c4fe3e3a59f.png)
#### 1. Access and update styles of element nodes
`node.style.property = value`
```JavaScript
const now = new Date();
const s = now.getSeconds();
const m = now.getMinutes();
const h = now.getHours();

secondHand.style.transform = `rotate(${(s / 60) * 360 + 90}deg)`;
minHand.style.transform = `rotate(${(m / 60) * 360 + 90}deg)`;
hourHand.style.transform = `rotate(${(h / 12) * 360 + 90}deg)`;
```

## day3 CSS Variables
![image](https://user-images.githubusercontent.com/26381972/71702171-3d8a0a80-2e11-11ea-8c21-908c2093981b.png)

#### 1. css custom properties
Property names that are prefixed with `--` represent custom properties that contain a value
```CSS
:root {
  --base: #ffc600;
  --spacing: 10px;
  --blur: 10px;
}
```
#### 2. css variables
custom properties can be used in other declarations using the `var()` function.
```CSS
img {
  padding: var(--spacing);
  background: var(--base);
  filter: blur(var(--blur));
}
```
#### 3. update css property
```
style.setProperty(propertyName, newValue);
```
```JavaScript
const inputs = document.querySelectorAll('.controls input')
function handleUpdate() {
  const suffix = this.dataset.sizing || '';
  document.documentElement.style.setProperty(
    `--${this.name}`, this.value + suffix
    );
}
inputs.forEach(e => e.addEventListener('change', handleUpdate));
inputs.forEach(e => e.addEventListener('mousemove', handleUpdate));
```

## day4 Array Methods
#### `array.filter(callback)`
- The `filter()` method creates a new array with all elements that pass the callback function.
```JavaScript
// 1. Filter the list of inventors for those who were born in the 1500's
const fifteens = inventors.filter(e => 1500 <= e.year && e.year < 1600 );
```
#### ` array.map(callback)`
- The `map()` method creates a new array populated with the results of the callback function on every element.
```JavaScript
// 2. Give us an array of the inventors' first and last names
const fullNames = inventors.map( e => `${e.first} ${e.last}`);
```
#### `array.sort([compareFunction])`
- The `sort()` method sorts the elements of an array in place and returns the sorted array.
```JavaScript
// 3. Sort the inventors by birthdate, oldest to youngest
const oldToYoung = inventors.sort((a, b) => a.year - b.year);

// 7. Sort the people alphabetically by last name
const orderedPeople = people.sort((a, b) => {
  const [firstA, lastA] = a.split(', ');
  const [firstB, lastB] = b.split(', ');
  return lastA > lastB ? 1 : -1;
});
```
#### `arr.reduce(callback[, initialValue])`
- The `reduce()` method executes a reducer function on each element of the array, resulting in single output value.
```JavaScript
// 4. How many years did all the inventors live?
const totalYear = inventors.reduce((years, e) => years + e.passed - e.year, 0);

// 8. Sum up the instances of each of these
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];
const countData = data.reduce((count, key) => {
  if (!count[key]) {
    count[key] = 0;
  }
  count[key]++;
  return count;
}, {});
```

## day5 flexible layout
![image](https://user-images.githubusercontent.com/26381972/71702092-d704ec80-2e10-11ea-9fa3-d088feacdd03.png)
The flex layout aims at providing a more efficient way to align and distribute space among items in a container, even when their size is unknown and/or dynamic. _(a W3C Candidate Recommendation as of October 2017)_
#### flex items in same ratio
```HTML
<div class="container">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
</div>
```
```CSS
.container {
  display: flex;
}
.item {
  flex: 1;
}
```
#### more properties for a Flex Container
| property | value |
|:---:|:---:|
`display` | defines a flex container.
`flex-direction` | establishes the main-axis of flex items.
`flex-wrap` | sets how to wrap flex items. `nowrap (default)` \| `wrap` \|  `wrap-reverse`
`flex-flow` | is shortcut of `flex-direction` and `flex-wrap`.
`justify-content` | defines the alignment along the main axis.
`align-content` | defines the alignment along cross axis. (more than 2 line)
`align-items` | defines the alignment along cross axis. (1 line)

#### more properties for Flex Item
| property | value |
|:---:|:---:|
`order` | controls the order of flex item in the flex container.
`flex` | is a shortcut of `flex-grow`, `flex-shrink`, `flex-basis`
`flex-grow` | defines the ability for a flex item to grow if necessary.
`flex-shrink` | defines the ability for a flex item to shrink if necessary.
`flex-basis` | defines the default size of a flex item before the remaining space is distributed.
`align-self` | defines the alignment of Item along a cross axis.

- reference
  - [A Complete Guide to Flexbox (EN)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
  - [CSS Flex(Flexible Box) 완벽 가이드 (KR)](https://heropy.blog/2018/11/24/css-flexible-box/)

## day6 Typeahead
![image](https://user-images.githubusercontent.com/26381972/71693228-42d65d80-2def-11ea-895d-1cec75fa5ff1.png)

#### Fetching Data
- [`fetch(resource[, init])`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch)
- The `fetch()` method starts the process of fetching a resource from the network, returning a promise which is fulfilled once the response is available.
```JavaScript
const cities = [];
const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';

fetch(endpoint)
  .then(blob => blob.json())
  .then(data => cities.push(...data));
```

#### Regular Expression in JS
##### [`new RegExp(pattern[, flags])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- The `RegExp` constructor creates a regular expression object for matching text with a pattern.
- `flags`
  - `g`: global match; find all matches rather than stopping after the first match.
  - `i`: ignore case; if u flag is also enabled, use Unicode case folding.
  - `m`: multiline; treat beginning and end characters (^ and $) as working over multiple lines.
  - `s`: "dotAll"; allows . to match newlines.
  - `u`: Unicode; treat pattern as a sequence of Unicode code points. (See also Binary strings).
  - `y`: sticky; matches only from the index indicated by the lastIndex property of this regular expression in the target string (and does not attempt to match from any later indexes).
```JavaScript
const findMatches = (wordToMatch, cities) => {
  const regex = new RegExp(wordToMatch, 'gi');
  return cities.filter(e => e.city.match(regex) || e.state.match(regex));
}
```

- To create a regular expression can calling the constructor function of the `RegExp` object, as above.
- Using the constructor function provides runtime compilation of the regular expression.
- Use the constructor function when you know the regular expression pattern will be changing, or you don't know the pattern and are getting it from another source, such as user input.

##### [`/pattern/modifiers;`](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)
- To create a regular expression can using literal, which consists of a pattern enclosed between slashes.
- Regular expression literals provide compilation of the regular expression when the script is loaded.
- If the regular expression remains constant, using this can improve performance.

```JavaScript
const numberWithCommas = x => x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.');

function displayMatches() {
  const regex = new RegExp(this.value, 'gi');
  const matched = findMatches(this.value, cities);
  const html = matched.map(e => {
    const cityName = e.city.replace(regex, `<span class='hl'>${this.value}</span>`);
    const stateName = e.state.replace(regex, `<span class='hl'>${this.value}</span>`);
    return `
      <li>
        <span class='name'>${cityName}, ${stateName}</span>
        <span class='population'>${numberWithCommas(e.population)}</span>
      </li>
    `;
  }).join('');
  suggestions.innerHTML = html;
}
```
| Metacharacter | role |
|:---:|:---:|
|`\B`|to find a match which is not present at the beginning or end of a word. If a match is found it returns the word else it returns NULL.
|`\d`|to search digit characters. It is same as `[0-9]`.

| Quantifier | role |
|:---:|:---:|
|`p+`| to find match any string containing one or more p.
|`?=p`|to find match any string which is followed by a specific p.
|`?!p`|to find the match of any string which is not followed by a specific p.
|`p{N}`| to find match any string containing a sequence of N times p.

- reference
  - [MDN - Regular_Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
  - [W3S - RegExp Literal grammar](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)
  - [tp - RegExp Literal grammar](https://www.tutorialspoint.com/javascript/javascript_regexp_object.htm)

## day7 Array Methods 2
#### [`array.some(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
- tests whether at least one element in the array passes the provided callback function.
- returns a Boolean value.
```JavaScript
// is at least one person 19 or older?
const currentYear = new Date().getFullYear();
const oneAdult = `
  ${people.some(e => e.year >= currentYear - 19)
    ? 'At least one person'
    : 'No one'
  } over 19.
`;
```
#### [`array.every(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
- tests whether all elements in the array pass the provided callback function.
- returns a Boolean value.
```JavaScript
// is everyone 19 or older?
const allAdult = `
  ${people.every(e => e.year >= currentYear - 19)
    ? 'All'
    : 'Not all'
  } people are over 19.
`;
```
#### [`array.find(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
-  returns the value of the first element in the provided array that satisfies the provided callback function.
```JavaScript
// find the comment with the ID of 823423
const comment = comments.find(e => e.id === 823423);
```
#### [`array.findIndex(callback[, thisArg])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
- returns the index of the first element in the array that satisfies the provided callback function.
- if no element passed the test, it returns -1.
```JavaScript
// find the index with the ID of 823423
const idx = comments.findIndex(e => e.id === 823423);
```
#### [`array.slice([begin[, end]])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
- returns a shallow copy of a portion of an array into a new array object selected from begin to end - 1.
```JavaScript
// create new array without a comment at comments[idx]
const newComments = [
  ...comments.slice(0, idx),
  ...comments.slice(idx+1)
];
```
#### [`array.splice(start[, deleteCount, item1, item2, ...])`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
- changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
  - `start`: The index at which to start changing the array.
  - `deleteCount`: The number of elements to remove.
  - `item`: The elements to add to the array.
```JavaScript
// delete a comment at comments[idx]
comments.splice(idx, 1);
```
## day8 HTML5 canvas

![image](https://user-images.githubusercontent.com/26381972/71877839-7c032a80-316d-11ea-9ac1-736ec895da7a.png)

#### [`<canvas>`](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial)
`<canvas>` is an HTML element which can be used to draw graphics via scripting. This can, for instance, be used to draw graphs, combine photos, or create animations.

#### 1. define canvas element
```HTML
<canvas id="draw" width="800" height="800"></canvas>
```
- `<canvas>` has only two attributes, `width` and `height`. These are both optional.

#### 2. access the rendering context
```JavaScript
const canvas = document.querySelector('#draw');
const ctx = canvas.getContext('2d');
```
- [`RenderingContext`](https://developer.mozilla.org/en-US/docs/Web/API/RenderingContext) is a WebIDL typedef which can refer to any one of the interfaces that represent a graphics rendering context within a `<canvas>` element.

#### 2. set properties of rendering context

```JavaScript
ctx.strokeStyle = '#BADA55'
ctx.linejoin = 'round';
ctx.lineCap = 'round';
```

property | about
:---:|:---:
`ctx.lineCap`| is a shape of the stroke, `round` \| `butt` \| `square`
`ctx.lineJoin`|  determines the shape used to join two line segments where they meet, `bevel` \| `round` \| `miter`
`ctx.lineWidth`| specifies the thickness of lines
`ctx.strokeStyle`| specifies the color, gradient, or pattern to use for the strokes (outlines) around shape. The default is `#000` (black)
`ctx.fillStyle`| specifies the color, gradient, or pattern to use inside shapes. The default is `#000` (black)

#### 2. use methods to draw stroke

Method| about
:---:|:---:
`ctx.beginPath()`| starts a new path by emptying the list of sub-paths. Call this method when you want to create a new path.
`ctx.moveTo()`| begins a new sub-path at the point specified by the given (x, y) coordinates.
`ctx.lineTo()`| adds a straight line to the current sub-path by connecting the sub-path's last point to the specified (x, y) coordinates.
`ctx.stroke()`| strokes the current or given path with the current stroke style.

```JavaScript
let isDrawing = false;
let lastX = 0;
let lastY = 0;
let direction = true;

function draw(e) {
  if(!isDrawing) return;
  ctx.beginPath();
  ctx.moveTo(lastX, lastY);
  ctx.lineTo(e.offsetX, e.offsetY);
  ctx.stroke();
  lastX, lastY = [e.offsetX, e.offsetY]
  ctx.lineWidth = ctx.lineWidth < 500 ? ctx.lineWidth + 1 : 500;
}

canvas.addEventListener('mousedown', (e) => {
  lastX, lastY = [e.offsetX, e.offsetY];
  ctx.lineWidth = 10;
  isDrawing = true;
});
canvas.addEventListener('mousemove', draw);
canvas.addEventListener('mouseout', () => isDrawing = false);
canvas.addEventListener('mouseup', () => isDrawing = false);
```

#### `hsl()`
The **HSL** is the **H**ue - **S**aturation - **L**ightness model.

Hue|Saturation|Lightness
:---:|:---:|:---:
an angle of the color circle|a percentage of saturation|a percentages lightness
`0` \| `360` is red|`100%` \| `1` is full saturation|`100%` \| `1` is white
`120` is green|`50%` \| `0.5` is half saturation|`50%` \| `0.5` is normal
`240` is blue|`0%` \|`0` is achromatic|`0%` \| `0` is black


#### Draw a rainbow in a stroke
```JavaScript
let hue = 0;

function draw(e) {
  if(!isDrawing) return;
  ctx.strokeStyle = `hsl(${hue}, 20%, 50%)`;
  ctx.beginPath();
  ctx.moveTo(lastX, lastY);
  ctx.lineTo(e.offsetX, e.offsetY);
  ctx.stroke();
  lastX, lastY = [e.offsetX, e.offsetY]
  ctx.lineWidth = ctx.lineWidth < 500 ? ctx.lineWidth + 1 : 500;
  hue = hue > 360 ? 0 : hue + 1;
}
```

## day9 dev tools and console tricks

#### [DOM change BreakPoint](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints#dom)
![image](https://user-images.githubusercontent.com/26381972/71986218-6f66fb00-326f-11ea-967a-8f29f030e23a.png)
Use DOM change breakpoints when you want to pause in code that changes DOM nodes or their children.

type|about
:---:|:---:
**Subtree modifications** | Triggered when a child element of the currently selected node is deleted or added, or when the child element's content changes. It is not triggered when the attributes of the child element nodes change or when the currently selected node changes.
**Attributes modifications** | Triggered when adding or deleting attributes to the currently selected node, or when attribute values ​​change.
**Node Removal** | Triggered when the currently selected node is deleted.

## day10 forEach and MouseEvent

![image](https://user-images.githubusercontent.com/26381972/72051797-46924480-3307-11ea-89b8-46025ef53e05.png)

#### forEach()
- Looping through check boxes, checking all boxes between last checked box and the currently checked box.
```JavaScript
function handleCheck(e) {
  let inBetween = false;
  if (e.shiftKey && this.checked) {
    checkboxes.forEach(checkbox => {
      if (checkbox === this || checkbox === lastChecked) {
        inBetween = !inBetween;);
      }
      if (inBetween) {
        checkbox.checked = true;
      }
    });
  }

  lastChecked = this;
}
```
- In fact, we don't need to check since the current checked box, so exiting the loop is more efficient.
- can not use `return` `break` `continue` for a `forEach()` loop.

```JavaScript
function handleCheck(e) {
  let inBetween = false;
  if (e.shiftKey && this.checked) {
    for (let i = 0; i < checkboxes.length; i++) {
      if (checkboxes[i] === this) {
        break;
      }
      else if (checkboxes[i] === lastChecked) {
        inBetween = !inBetween;
      }
      else if (inBetween) {
        checkboxes[i].checked = true;
      }
    }
  }
  lastChecked = this;
}
```

#### [MouseEvent()](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent)
- The MouseEvent interface represents events that occur due to the user interacting with a pointing device (such as a mouse).

property|about
:---:|:---:
**MouseEvent.altKey**|Returns true if the alt key was down when the mouse event was fired.
**MouseEvent.ctrlKey**|Returns true if the control key was down when the mouse event was fired.
**MouseEvent.metaKey**|Returns true if the meta key was down when the mouse event was fired.
**MouseEvent.shiftKey**|Returns true if the shift key was down when the mouse event was fired.
**MouseEvent.button**|The button number that was pressed (if applicable) when the mouse event was fired.
**MouseEvent.buttons**|The buttons being depressed (if any) when the mouse event was fired.
**MouseEvent.clientX**|The X coordinate of the mouse pointer in local (DOM content) coordinates.
**MouseEvent.clientY**|The Y coordinate of the mouse pointer in local (DOM content) coordinates.
**MouseEvent.x**|Alias for MouseEvent.clientX.
**MouseEvent.y**|Alias for MouseEvent.clientY
**MouseEvent.movementX**|The X coordinate of the mouse pointer relative to the position of the last mousemove event.
**MouseEvent.movementY**|The Y coordinate of the mouse pointer relative to the position of the last mousemove event.
**MouseEvent.offsetX**|The X coordinate of the mouse pointer relative to the position of the padding edge of the target node.
**MouseEvent.offsetY**|The Y coordinate of the mouse pointer relative to the position of the padding edge of the target node.
**MouseEvent.pageX**|The X coordinate of the mouse pointer relative to the whole document.
**MouseEvent.pageY**|The Y coordinate of the mouse pointer relative to the whole document.
**MouseEvent.screenX**|The X coordinate of the mouse pointer in global (screen) coordinates.
**MouseEvent.screenY**|The Y coordinate of the mouse pointer in global (screen) coordinates.
**MouseEvent.region**|Returns the id of the hit region affected by the event. If no hit region is affected, null is returned.
**MouseEvent.relatedTarget**|The secondary target for the event, if there is one.

## day11 Custom Video Player
![image](https://user-images.githubusercontent.com/26381972/76519471-6b8c6a80-64a4-11ea-9ece-ff7e42b217fb.png)
#### <video></video>
- you can provide many sources for a video to support various browser
```html
<video class="player__video viewer">
  <source src="652333414.mp4" type="video/mp4">
  <source src="another-source" type="other-type4">
</video>
```
#### querySelector()
- we use query selector to get html element.
- `const video = player.querySelector('.viewer');` return an element which has the class name `veiwer`.
- `const skipButtons = player.querySelectorAll('[data-skip]');` return elements which has the attributr `data-skip`.

## day12 KONAMI CODE
![image](https://user-images.githubusercontent.com/26381972/76598507-5ff18000-6546-11ea-89de-d392db63843c.png)
### .splice() with negative index
`array.splice(start[, deleteCount[, ...elements to add])`
- `0 < start` => Delete elements as mush deleteCount from array[start] & Add elements from array[start] 
- `0 > start` => -1 means starts from end
- `start > array.length` => no element will be deleted & will behave as an adding function
- `0 >= deleteCount` => no elements will be deleted

```JavaScript
const pressed = [], secretCode = 'hon9g';
window.addEventListener('keyup', e => {
  pressed.push(e.key);
  // If pressed.length exceeds secretCode.length delete the first element at position -6
  pressed.splice(-secretCode.length -1, pressed.length - secretCode.length);
  if (pressed.join('') === secretCode) {
    cornify_add();
  }
});
```
## day13 Slide in on Scroll
![DS_20200313-202117_](https://user-images.githubusercontent.com/26381972/76616954-8b856200-6568-11ea-88b0-3c1014a150cb.gif)
#### property of a window interface
- `window.innerHeight` the interior height of the window in pixels, including the height of the horizontal scroll bar, if present.
- `window.ScrollY`  the number of pixels that the document is currently scrolled vertically.
#### property of a HTML element
- `HTMLElement.offsetTop` the distance of the current element relative to the top of the offsetParent node.
- `img.height` specify the height of the image in pixel.

## day14 Reference vs Copy
```JavaScript
const arr = [1,2,[3]], obj = {name:'h', located: 'seoul'};
```
This is Reference
```JavaScript
const ref1 = arr, ref2 = obj;
```

This is Shallow Copy
```JavaScript
const copyArr1 = [...arr], // <- new in ES6 === ES2015
      copyArr2 = [].concat(arr),
      copyArr3 = arr.slice(),
      copyArr4 = Array.from(arr);
      
const copyObj1 = {...obj}, // <- new in ES9 === ES2018
      copyObj2 = Object.assign({}, obj);
```

This is Deep Copy
```JavaScript
const deepCopy1 = JSON.parse(JSON.stringify(arr));
const deepCopy2 = JSON.parse(JSON.stringify(obj));
```
- or use `lodash.clonedeep`

## day15 LocalStorage and Event Delegation
`localStorage` and `sessionStorage` which were added from HTML5 store data as `key - value` on the client side
#### Window.localStorage
- Data stored in localStorage has no expiration time.
```JavaScript
localStorage.setItem('key', 'val');
localStorage.getItem('key');
localStorage.removeItem('key');
localStorage.clear();
```
#### Window.sessionStorage
- Data in sessionStorage is cleared when the page session ends.
- A page session lasts as long as the browser is open, and survives over page reloads and restores.
- Opening a page in a new tab or window creates a new session with the value of the top-level browsing context, which differs from how session cookies work.
- Opening multiple tabs/windows with the same URL creates sessionStorage for each tab/window.
- Closing a tab/window ends the session and clears objects in sessionStorage.
```JavaScript
sessionStorage.setItem('key', 'value');
sessionStorage.getItem('key');
sessionStorage.removeItem('key');
sessionStorage.clear();
```
#### Event Delegation
Attach a single event listener on parent node instead dynamicly added nodes.

## day16 Mouse Move Shadow
![DS_20200319-034020_](https://user-images.githubusercontent.com/26381972/76995721-9c343e80-6993-11ea-9749-6ce7442fd09c.gif)

## day17 Sort Without Articles
```JavaScript
const strip = name => name.replace(/^(a |the |an )/i, '');
bands.sort((a,b) => strip(a) > strip(b) ? 1 : -1);
```
#### Regular Expression
- literal: `let re = /ab+c/;`
- calling constructor function: `let re = new RegExp('ab+c');`

## day18 Adding Up Times with Reduce
```JavaScript
const seconds = timeNodes.reduce((totalTime, node) => {
      const [mins, secs] = node.dataset.time.split(':').map(parseFloat);
      return totalTime + (mins*60) +secs;
      }, 0);
```
