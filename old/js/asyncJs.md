#AJAX

#Promise

```js
result = fetch(url);//fetch returns promise
```
* **Promise states**
    * `pending`
    * `resolved`
    * `rejected`

* Functions 

```js
result = fetch(url);//fetch returns promise

result
    .then(aFunction) //will run when resolved
    .then(anotherFunction)
    .catch(errFunction) //will run when in rejected state catches errors in all promises above
```

​	* `then` functions are chainable if previous then function (`aFunction`) returns a promise

​	* Example from [Coding train](https://github.com/CodingTrain/website/blob/master/Tutorials/P5JS/16_promises/11_promises/sketch.js)

```js
fetch(wordnikAPI)
    .then(response => response.json())
    .then(json => {
      createP(json.word);
      return fetch(giphyAPI + json.word);
    })
    .then(response => response.json())
    .then(json => {
      createImg(json.data[0].images['fixed_height_small'].url);
    })
    .catch(err => console.log(err));    
```

* **Create Promise**

  ```js
  function delay(time) {
    return new Promise((resolve, reject) => {
      if (isNaN(time)) {
        reject(new Error('delay requires a valid number.'));
      } else {
        setTimeout(resolve, time);//resolve after that amount of time
      }
    });
  }
  ```

* ​

# async/await (ES8)

* `await` only runs inside `aysnc` function
* `async` function returns promise


* Same example with async/await

  ```js
  async function wordGIF(num) {
    let response1 = await fetch(wordnikAPI + '&minLength=' + num + '&maxLength=' + num);
    let json1 = await response1.json();
    let response2 = await fetch(giphyAPI + json1.word);
    let json2 = await response2.json();
    let img_url = null;
    try {
      img_url = json2.data[0].images['fixed_height_small'].url;
    } catch (err) {
      console.log('no image found for ' + json1.word);
      console.error(err);
    }
    return {
      word: json1.word,
      img: img_url
    }
  }

  ```

* `Promise.all`Waits until **all** promises in given array to resolve and returns a promise

  ```js

    let promises = [];
    for (let i = 2; i < 10; i++) {
      promises.push(wordGIF(i));
    }
    Promise.all(promises)
      .then((results) => {
        for (let i = 0; i < results.length; i++) {
          createP(results[i].word);
          if (results[i].img !== null) {
            createImg(results[i].img);
          }
        }
      })
      .catch((err) => console.log(err));
  ```

* `Promise.race` Waits until **one** promise in given array to resolve and returns a promise