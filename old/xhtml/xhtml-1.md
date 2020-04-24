##XHTML and HTML
* Opening tag: `<tag_name>` , closing tag: `</tag_name>`
* in xhtml, tags are case sensitive but, in html they are not.
* Example
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">

    <head>
       	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
   
     	<title>Title of page</title>
    </head>

    <body>
   		<p>All content in body will appear on the page</p>

  	</body>
</html>
```
* Every open tag must have been closed
* `<html>` tells browser in which language the code has written.
* `<head>` 
* `<body>` all content that appear on the page.
* `<p>` create paragraph
* `<blockquote>` to create quote. quote style can be defined in CSS.
* `<br />` end of line (to continue to paragraph from new line)
* `h1` `h2`... `h6` create header
* `<hr />` create horizontal line
* `<!-- "Comment" -->`
* `<pre>` Text will appear like how it is written in the code
* `&nbsp` extara space   
* customizing text ("p", "h1"..."h6", "div", "pre", "address", "fieldset", "ins", "del")
	* `<strong>` 
	* `<big>`
	* `<small>`
	* `<i>` italic
	* `<sub>` 
	* `<sup>`
* link    
	* `<a href="example.com" title="title of link"> text </a>`  ("p", "h1"..."h6", "div", "pre", "address", "fieldset", "ins", "del")
	* to go somewhere in the page
	type `<a name="xyx"></a>` to destination   
	to add link to that destination type `<a href="#xyz"> text </a>` 
	* to be opened in new tab, add `target="_blank"`    
		`<a href="example.com" title="title of link" target="_blank"> text </a>`
	* to link a html file called `asd.html`
		* if asd.html and your file are in same directory, you can type name of file to href field. `asd.html`
		* if asd.html is in a folder, you can type directory to href field. `folder1/folder2/asd.html`
		* if asd.html is in up of current directory, type `..` to go up. `../asd.html`       
	   

* image `<img src="image url" alt="loading failed height=  300px" title="title" />`
* link to image `<a href="url"> <img src="image url" alt="loading failed" title="title" /></a>`
   
* **Tables**
	* `<table>` Define table (`<table border="1" cellpadding="10" cellspacing="10">`)
		* border
		* cell padding: padding between cell border and text.
		* cell spacing: space between cells.
	* `<tr>` Define a row in a table
	* `<td>` Define a cell in a table
	* `<th>` Define a header cell in a table

	* `<caption>` Define a table caption
	* `<td rowspan="3">` to define cell that has 3 row heigth
	* `<td colspan="3">` to define a cell that has 3 column width
   
* **Div**
	* `<div style="height: 200px; width: 250px; border: 1px solid black; margin-bottom: 20px;">`
	* `<span style="color: green;">BOX </span>` 
   
* `<ul>` Unordered List. to add sth to list `<li>` eg: `<li>HTML</li> ...`.   
* `<ol>` Ordered List. to add sth to list `<li>` eg: `<li>HTML</li> ...`.    
* `<dl>` Definition List. to add  definition `<dt>`, to add description `<dd>`
   
* **Forms**
	* Input `<input type="name" name="namefield" />` (type should be name new input fields can have different names)
	* Radiobutton `<input type="radio" name="name" />`(type should be radio and new radio buttons should have same names)
	* Check box `<input type="checkbox" name="name" />` (type should be checkbox new input fields can have different names)
 	* Button `<input type="submit" value="Send" />` (type should be button or submit)
 	* Text area `<textarea rows="5" cols="40"></textarea>`
 	* Drop Down Menu
```
<select name="Nameofmenu">
<optgroup label="Label 1">
<option value="op1" >Option 1 </option>
<option value="op2" >Option 2 </option>
<optgroup label="Label 2">
<option value="op3" selected="selected" >Option 3 </option>
<option value="op4" >Option 4 </option>
```   
opt3 will be shown by default.
	* If you want to run check box or radio button by clicking text, add text and Radio Button/Checkbox in `</label>` tag
	* to add frame, add components in `<fieldset>` tag. (`<legend>` tag can be used inside fieldset tag.)
   
* **Head & Meta tags**   
`<head>` things that will not apperar in page.   tags in below should used inside head tag.
	* `<title>` title of site that will appear on the top of browser or tab    
		`<title>This is a Page</title>`
	* `<base>` default location to use files in that directory directly.    
		`<base href="http://www.siteurl.com/filename" />`
	* `<link>` to define relationship between html file and a file.   
		`<link rel="stylesheet" media="screen" type="text/css" href="style.css">` 
	* `<meta>` where keywords can defined in to be used by search engines.   
		`<meta name="Keywords" content="keyword1, keyword 2">`
   
* Vaildate your website from http://validator.w3.org

* **HTML 5**
	* Redirect page in 3 sec  `<meta http-equiv="refresh" content="3; url=redirect.html"/>`
	* To run a pdf or html in part of the page.
```
<object data="file.pdf" type="application/pdf" 
width="750" height="400"></object>

<object data="file.html" type="text/html" 
width="750" height="400"></object>
```

asassdadsasdsdaMonday, 17. October 2016 10:00pm 
