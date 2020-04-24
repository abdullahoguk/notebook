# ES6/ES2015	

* `babel` is js compiler
* create `node` project
  * edit `package.json` file
  * `babel-cli`
  * `babel-preset-es2015`
  * create `.babelrc` file

  ```json
  {
  "presets" : [
  	"es2015"	
  ]
  }
  ```
* create `src` folder
  * create `main.js`

* create `dist` folder (compiled file will be here)
* ...edit package json 
* ​
---
* Declare variable `let test = "hello";`
  * if you redeclare a variable with `let` , it's value will be available in its scope.	

  * Create class(so similar with java php ... inheritence ...)

```javascript
class User{
	register(){
	...
	}
}
```

* Template Strings (use back ticks ` when defining  string to use them with multiple line)	

```javascript
let template = `<h1>Hello</h1>
<p>this is template</p>`

document.getElementById("template").innerHTML = template;
```

* ​

​		