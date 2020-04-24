##CSS

* type `<link rel="stylesheet" type="text/css" href="style_file.css" />` to head of html file that you want to customize

* 	```css
	html_Tag
	{
		properties
		color : green;
	...
	}
	```
   
* Open comment with `/*` then close with `*/`
* Id Selector: to create a style to use just once. 
	type that tag in html file as 
	```html
	<p id="firstPrgrph">this is different</p>
	```
    
	then create style to be able to use just for that fieled 

	```css
	#firstPrgrph {color : blue;}
	```   
* Class Selector: pretty same with id selector. Class using to apply style to more than one tag.  
	```html
	<p class="firstclass">I am different</p>
	<h2 class="firstclass">me too</h2>
	```
    
	then create style to be able to use just for that fieled 

	```css
	.firstclass {color : yellow;}
	``` 

* to custimize a child tag where is inside a tag.
	`parentTag.classNameofParentTag child_tag`
	```html
	<nav class= "c1">
		<p>Paragraph<p>
	</nav>
	```
     
     ```css
     nav.c1 p{style...}
     ```
 * for global decleration `*`
 	```css
 	* {
 		font-family: sans-serif;
 	}
 	```
* **Colors**   
`aqua` `black` `blue` `fuchsia` `gray` `green` `lime` `maroon` `navy` 
`olive` `purple` `red` `silver` `teal` `white` `yellow`    
or from `#000000` up to `#FFFFFF`
   
* **Background** 
	* Color > `background-color: blue;`
	* Image > `background-image: url('bg.jpg');`
	* Repeating > `no-repeat` , `repeat-x` , `repeat-y` or `repeat` 
		```
		background-image: url('bg.jpg')
		background-repeat: no-repeat;

		```
	* Position > `top left` , `center right` , `bottom right` ... or `x% y%` as `background-position: x% y%`
	* You can use whole image as bg and image can be scrolled. `background: url('bg.jpg') no-repeat scroll;`
    
* **Text**  
	* Text Alignment
		```CSS
		text-align: left;
		text-align: center;
		text-align: right;
		text-align: justify;
		```
	* Text Decoration
		```CSS
		text-decoration: none;
		text-decoration: underline;
		text-decoration: overline;
		text-decoration: line-through;
		text-decoration: blink;
		```
	* Text Transformation
		```CSS
		text-transform: uppercase;
		text-transform: lowercase;
		text-transform: capitalize;
		```
	* Text Indentation: to arrange indentation in paragraphs.
		`text-indent: 75px;`
		* Heigth between lines: `line-height: 25px;`
		* Space between letters: `letter-spacing: 13px;`
		* Space between words: `word-spacing: 12px;`
		* Direction of text (left or right): `direction: rtl;` , `direction: ltr;`

* **Fonts**
	* Custom font
		`font-family: "Monospace", Times, serif;`
	* Font style
		`font-style: italic;` , `font-style: oblique;` or `font-style: normal;`
	* Font size
		`font-size: 13px;`
	Other
		`font-variant: small-caps` makes all letters uppercase
		`font-weight: bold;` makes all letters bold

* **Links**
	* to customize not visited link `a:link`
	* to customize visited link `a:visited`
	* to customize style when hovering on link `a:hover`
	* to customize style when click on link `a:active`

* **Lists**   
	List Styles (`list-style-type`) 
	* Ordered Lists   
		 `armenian`, `decimal`, `decimal-leading-zero`, `georgian`, `lower-alpha`, `lower-greek`, `lower-latin`,  `lower-roman`, `upper-alpha`, `upper-latin`, `upper-roman`   

			```CSS
			ol {
			list-style-type: lower-alpha;
			}
			```   
	* Unordered Lists   
		`none`, `disc`, `circle`, `square`  or for external image `list-style-image: url('image.png');`

			```CSS
			ul {
			list-style-type: square;
			}
			```   
* **Tables**

