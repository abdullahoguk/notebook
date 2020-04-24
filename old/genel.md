#JS30 (WesBos) [source code](https://github.com/wesbos/JavaScript30) 
1. JavaScript Drum Kit
- html data attributes

```html
<div data-key="65" class="key">
      <kbd>A</kbd>
      <span class="sound">clap</span>
    </div>

  <audio data-key="65" src="sounds/clap.wav"></audio>

```

- Query Selector 

```javascript
    //document.querySelectorAll('.key')
    const keys = Array.from(document.querySelectorAll('.key'));
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    const key = document.querySelector(`div[data-key="${e.keyCode}"]`);
```

- audio play

```javascript
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    audio.play();
```

2. JS and CSS Clock
3. CSS Variables
- defining in css 
```css
:root {
      --base: #ffc600;
      --spacing: 10px;
      --blur: 10px;
    }
```

- using ins css
```css
img {
      padding: var(--spacing);
      background: var(--base);
      filter: blur(var(--blur));
    }
```

- munipilating from js
name of css the variable should be same with "name" attribute of input dom element.

```html
<label for="spacing">Spacing:</label>
    <input id="spacing" type="range" name="spacing" min="10" max="200" value="10" data-sizing="px">
```

```js
    const inputs = document.querySelectorAll('.controls input');
    function handleUpdate() {
      const suffix = this.dataset.sizing || '';
      document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
    }
    inputs.forEach(input => input.addEventListener('change', handleUpdate));
    inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
```

4. Array Cardio Day 1
    
```js
const inventors = [
      { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
      { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
      { first: 'Max', last: 'Planck', year: 1858, passed: 1947 },
      { first: 'Hanna', last: 'Hammarström', year: 1829, passed: 1909 }
    ];
```

- Array Methods
    - **Filter** Filter elements of array according to given function

    ```js
        const fifteen = inventors.filter(inventor => (inventor.year >= 1500 && inventor.year < 1600));
    ```

    - **Map** create new array from current by muniplating its elements of according to given function 

    ```js
        const fullNames = inventors.map(inventor => `${inventor.first} ${inventor.last}`);
    ``` 

    - **Sort** 
        given a and b respectively
        - return -1 to place "a" first (or any negative number)
        - return 1 to place "b" first (or any positive number)
        - return 0 to unchange

    ```js
        const ordered = inventors.sort((a, b) => a.year > b.year ? 1 : -1);
    ```

    - **Reduce** 
    ```js
    const totalYears = inventors.reduce((total, inventor) => {
      return total + (inventor.passed - inventor.year);
    }, 0);
    ```

5. Flex Panel Gallery
- Flexbox, transitions, transiton end events

6. Ajax Type Ahead
- Fetch data with browsers Fetch API
    
    ```js
    const endpoint = 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json';

    const cities = [];
    //spread array with "..." (ES6)
    fetch(endpoint)
      .then(blob => blob.json())
      .then(data => cities.push(...data));
    ```

- finding mathes with regex
    ```js
    function findMatches(wordToMatch, cities) {
      return cities.filter(place => {
        const regex = new RegExp(wordToMatch, 'gi');
        return place.city.match(regex) || place.state.match(regex)
      });
    }

    ```

7. Array Cardio Day 2
- Array Methods
    - **Some** returns true if given functions specs are satisfied for at least one element
    ```js
    const isAdult = people.some(person => ((new Date()).getFullYear()) - person.year >= 19);
    ```
    - **Every** returns true if given functions specs are satisfied for all elements
    - **Find** find the exact element you are looking for 
    ```js
    const comment = comments.find(comment => comment.id === 823423);
    ```
    - **Find Index** find the index of an element you are looking for 
    ```js
    const index = comments.findIndex(comment => comment.id === 823423);
    ```
    - **Splice** remove elements from an array by giving index and num of items to delete starting from tha index.
    ```js
    comments.splice(index, 1);
    ```
    - **Slice** Create new sub array by giving index and num of items to add starting from tha index(offset).
    ```js
    //Removing with slice
    const newComments = [
      ...comments.slice(0, index),
      ...comments.slice(index + 1)
    ];
    ```

8. Fun with HTML5 Canvas
JS30(wesbos)-8(canvas) https://codepen.io/abdullahoguk/pen/odWxra 

9. 14 Must Know Dev Tools Tricks
```js
    //Styled
    console.log('%c I am some great text', 'font-size:50px; background:red; text-shadow: 10px 10px 0 blue');

    // warning!
    console.warn('OH NOOO');

    // Error :|
    console.error(':((((');

    // Info
    console.info('Crocodiles eat 3-4 people per year');

    // Testing
    const p = document.querySelector('p');
    console.assert(p.classList.contains('ouch'), 'That is wrong!');

    // clearing
    console.clear();

    // Viewing DOM Elements
    console.log(p);
    console.dir(p);

    // Grouping together
    dogs.forEach(dog => {
      console.groupCollapsed(`${dog.name}`);
      console.log(`This is ${dog.name}`);
      console.log(`${dog.name} is ${dog.age} years old`);
      console.log(`${dog.name} is ${dog.age * 7} dog years old`);
      console.groupEnd(`${dog.name}`);
    });

    // counting
    console.count('Wes');
    console.count('Wes');
    console.count('Steve');
    console.count('Steve');
    console.count('Wes');
    console.count('Steve');
    console.count('Wes');
    console.count('Steve');
    console.count('Steve');
    console.count('Steve');
    console.count('Steve');
    console.count('Steve');

    // timing
    console.time('fetching data');
    fetch('https://api.github.com/users/wesbos')
      .then(data => data.json())
      .then(data => {
        console.timeEnd('fetching data');
        console.log(data);
      });

    console.table(dogs);
```

10. Hold Shift and Check Checkboxes
```js
const checkboxes = document.querySelectorAll('.inbox input[type="checkbox"]');
let lastChecked;
function handleCheck(e) {
  // Check if they had the shift key down
  // AND check that they are checking it
  let inBetween = false;
  if (e.shiftKey && this.checked) {
    // go ahead and do what we please
    // loop over every single checkbox
    checkboxes.forEach(checkbox => {
      console.log(checkbox);
      if (checkbox === this || checkbox === lastChecked) {
        inBetween = !inBetween;
        console.log('Starting to check them inbetween!');
      }
      if (inBetween) {
        checkbox.checked = true;
      }
    });
  }
  lastChecked = this;
}
checkboxes.forEach(checkbox => checkbox.addEventListener('click', handleCheck));
```

11. Custom HTML5 Video Player
```html
 <input type="range" name="volume" class="player__slider" min="0" max="1" step="0.05" value="1">
 <input type="range" name="playbackRate" class="player_slider" min="0.5" max="2" step="0.1" value="1">

<script>
function handleRangeUpdate() {
  video[this.name] = this.value; 
    //if name is volume > "video.volume = this.value"
    //if name is playbackRate > "video.playbackRate = this.value"
}

ranges.forEach(range => range.addEventListener('change', handleRangeUpdate));
ranges.forEach(range => range.addEventListener('mousemove', handleRangeUpdate));
</script>
```

12. Key Sequence Detection

13. Slide in on Scroll

14. JavaScript References VS Copying   
- arrays and objects will be referenced when assigning to another var   
- values of Int, Strings ... will be copied   
- to copy arrays    

```js
players.slice()
const team3 = [].concat(players);
const team4 = [...players];
const team5 = Array.from(players);
```
- To copy objects (one level)   

```js
const person = {
  name: 'Wes Bos',
  age: 80
};
const cap2 = Object.assign({}, person, { number: 99, age: 12 });

//for multi level but not recomeneded
const dev2 = JSON.parse(JSON.stringify(wes));

```

15. LocalStorage
```js
//Form with class "add-items"
const addItems = document.querySelector('.add-items');

//div to show items as list
const itemsList = document.querySelector('.plates');

//items array (if items array (as string) exist in local storage, assign it, if does not, assign it to an empty array)
const items = JSON.parse(localStorage.getItem('items')) || [];

//Runs when submit event happened  
function addItem(e) {
    //to prevent page from loading again by default after submiting form
    e.preventDefault();

    //get value from the text field in the form
    const text = (this.querySelector('[name=item]')).value;
    
    //ES6 >> the firstline "text," ~ to "text: text,"
    const item = {
      text,
      done: false
    };

    items.push(item);
    
    //render list
    populateList(items, itemsList);
    
    //add items array as string to local storage
    localStorage.setItem('items', JSON.stringify(items));

    //make form field empty after submitting
    this.reset();
}

//creates html code of list. plates is the items array, platesList is the div we want to show them as a list 
function populateList(plates = [], platesList) {
    platesList.innerHTML = plates.map((plate, i) => {
        return `
        <li>
          <input type="checkbox" data-index=${i} id="item${i}" ${plate.done ? 'checked' : ''} />
          <label for="item${i}">${plate.text}</label>
        </li>
      `;
    }).join('');
}

//save checked state of checklist items (event delegation)
//when new itens added, event listeners will be gone
//to prevent this, add event listener to parent
//this will fire events for all children (label, input, li)
function toggleDone(e) {
    if (!e.target.matches('input')) return; // skip this unless it's an input
    const el = e.target;
    const index = el.dataset.index;
    items[index].done = !items[index].done;
    localStorage.setItem('items', JSON.stringify(items));
    populateList(items, itemsList);
}


addItems.addEventListener('submit', addItem);
itemsList.addEventListener('click', toggleDone);
populateList(items, itemsList);
```

16. CSS Text Shadow Mouse Move Effect

17. Sorting Band Names without articles
```js

function strip(bandName) {
  return bandName.replace(/^(a |the |an )/i, '').trim();
}

const sortedBands = bands.sort((a, b) => strip(a) > strip(b) ? 1 : -1);
```

18. Tally String Times with Reduce
```html
.
.
.
    <li data-time="1:56">
      Video 57
    </li>
    <li data-time="4:04">
      Video 58
    </li>
</ul>
```

```js
const timeNodes = Array.from(document.querySelectorAll('[data-time]'));

const seconds = timeNodes
    .map(node => node.dataset.time)
    .map(timeCode => {
      const [mins, secs] = timeCode.split(':').map(parseFloat);

      return (mins * 60) + secs;
    })
    .reduce((total, vidSeconds) => total + vidSeconds);

    let secondsLeft = seconds;
    const hours = Math.floor(secondsLeft / 3600);
    secondsLeft = secondsLeft % 3600;
    const mins = Math.floor(secondsLeft / 60);
    secondsLeft = secondsLeft % 60;
    console.log(hours, mins, secondsLeft);
```

19. Unreal Webcam Fun

20. Native Speech Recognition
```js
//firefox and chrome
window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

const recognition = new SpeechRecognition();
recognition.interimResults = true;
recognition.lang = 'en-US';
  
let p = document.createElement('p');
const words = document.querySelector('.words');
words.appendChild(p);


recognition.addEventListener('result', e => {
    const transcript = Array.from(e.results)
      .map(result => result[0])
      .map(result => result.transcript)
      .join('');

      const poopScript = transcript.replace(/poop|poo|shit|dump/gi, '💩');
      p.textContent = poopScript;

      //to prevent replacing paragraph after started speaking again
      if (e.results[0].isFinal) {
        p = document.createElement('p');
        words.appendChild(p);
      }
  });

//restart recognition when stopped speaking
recognition.addEventListener('end', recognition.start);

recognition.start();
```

21. Geolocation based Speedometer and Compass
```js
const arrow = document.querySelector('.arrow');
    const speed = document.querySelector('.speed-value');
    navigator.geolocation.watchPosition((data) => {
      console.log(data);
      speed.textContent = data.coords.speed;
      arrow.style.transform = `rotate(${data.coords.heading}deg)`;
    }, (err) => {
      console.error(err);
    });
```

22. Follow Along Links
`getBoundingClientRect`

```js
const triggers = document.querySelectorAll('a');
const highlight = document.createElement('span');
highlight.classList.add('highlight');
document.body.appendChild(highlight);

function highlightLink() {
    const linkCoords = this.getBoundingClientRect();
    console.log(linkCoords);
    const coords = {
      width: linkCoords.width,
      height: linkCoords.height,
      top: linkCoords.top + window.scrollY,
      left: linkCoords.left + window.scrollX
    };

    highlight.style.width = `${coords.width}px`;
    highlight.style.height = `${coords.height}px`;
    highlight.style.transform = `translate(${coords.left}px, ${coords.top}px)`;
  }

triggers.forEach(a => a.addEventListener('mouseenter', highlightLink));
```

23. Speech Synthesis

24. Sticky Nav
```js
const nav = document.querySelector('#main');
let topOfNav = nav.offsetTop;

//toggle class of "fixed-nav" in each scroll
function fixNav() {
    if (window.scrollY >= topOfNav) {
        //prevent not taking up space when using "position: fixed" in CSS
        document.body.style.paddingTop = nav.offsetHeight + 'px';
        document.body.classList.add('fixed-nav');
      } else {
        document.body.classList.remove('fixed-nav');
        document.body.style.paddingTop = 0;
      }
}

//run fix nav in each scroll
window.addEventListener('scroll', fixNav);
```

25. Event Capture, Propagation, Bubbling and Once
```html
<body class="bod">
  <div class="one">
    <div class="two">
      <div class="three">
      </div>
    </div>
  </div>

<script>
  const divs = document.querySelectorAll('div');
  const button = document.querySelector('button');
  function logText(e) {
    console.log(this.classList.value);
    e.stopPropagation(); // stop bubbling!
    // console.log(this);
  }
  divs.forEach(div => div.addEventListener('click', logText, {
    capture: false,
  }));

  button.addEventListener('click', () => {
    console.log('Click!!!');
  }, {
    once: true
  });
</script>
</body>

```

26. Stripe Follow Along Dropdown (https://codepen.io/mattj/pen/mmXydj/)

27. Click and Drag to Scroll
```js
const slider = document.querySelector('.items');

let isDown = false;

//isDown start position
let startX;

//initial scroll positon of div when isDown started
let scrollLeft;


slider.addEventListener('mousedown', (e) => {
    isDown = true;
    slider.classList.add('active');
    startX = e.pageX - slider.offsetLeft;
    scrollLeft = slider.scrollLeft;
});

slider.addEventListener('mouseleave', () => {
    isDown = false;
    slider.classList.remove('active');
});

slider.addEventListener('mouseup', () => {
    isDown = false;
    slider.classList.remove('active');
});

slider.addEventListener('mousemove', (e) => {
    if (!isDown) return;  // stop the fn from running
    e.preventDefault();
    const x = e.pageX - slider.offsetLeft;
    const walk = (x - startX) * 3;
    slider.scrollLeft = scrollLeft - walk;
```

28. Video Speed Controller UI

29. Countdown Clock
```js
let countdown; //interval var (will be cleared when countdown finished)

//DOM Elements
const timerDisplay = document.querySelector('.display__time-left');
const endTime = document.querySelector('.display__end-time');
const buttons = document.querySelectorAll('[data-time]');

//timer runner function (calculete time left, call show functions and stop when finished)
function timer(seconds) {
  // clear any existing timers
  clearInterval(countdown);

  //calculate due time
  const now = Date.now();
  const then = now + seconds * 1000;

  //show time left once before, interval will start to run after given interval
  displayTimeLeft(seconds);
  
  displayEndTime(then);//due time

  //set interval to global var
  countdown = setInterval(() => {
    const secondsLeft = Math.round((then - Date.now()) / 1000);
    // check if we should stop it!
    if(secondsLeft < 0) {
      clearInterval(countdown);
      return;
    }
    // display it
    displayTimeLeft(secondsLeft);
  }, 1000);
}

//display time left on page
function displayTimeLeft(seconds) {
  const minutes = Math.floor(seconds / 60);
  const remainderSeconds = seconds % 60;
  const display = `${minutes}:${remainderSeconds < 10 ? '0' : '' }${remainderSeconds}`;
  document.title = display;
  timerDisplay.textContent = display;
}

//diplay due on page 
function displayEndTime(timestamp) {
  const end = new Date(timestamp);
  const hour = end.getHours();
  const adjustedHour = hour > 12 ? hour - 12 : hour;
  const minutes = end.getMinutes();
  endTime.textContent = `Be Back At ${adjustedHour}:${minutes < 10 ? '0' : ''}${minutes}`;
}


function startTimer() {
  const seconds = parseInt(this.dataset.time);
  timer(seconds);
}

buttons.forEach(button => button.addEventListener('click', startTimer));

//add events to form with "customForm" name attr
document.customForm.addEventListener('submit', function(e) {
  //prevent reloading page on submit
  e.preventDefault();

  const mins = this.minutes.value;
  console.log(mins);
  timer(mins * 60);
  this.reset(); //clear form field 
});
```





