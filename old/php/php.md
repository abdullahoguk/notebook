##PHP & MYSQL
* All PHP codes should be inside of `<?php [PHPcode]  ?>` tag.
* Extension of file should be `.php`.
* `echo` outputs code to html . `echo "Hello<br/>World"`
* `.` concatenates two strings. (like `.` in Java) `echo "Hello" . "World!";` 
* `//` or `#` for single line comments.
* `/* Comment*/` for multiple line comments.
* Php codes pocesses by apache and can not be shown in page source in browser.
* **Variables**
    * to define variable name `$var_nam e` `echo "Hello $user"` = `echo "Hello {$user}"`
    * variable names are case sensetive (`Var` and `var` are different.)
    * Don't use `-` and multiple `_` when defininig variable `$like-that` `$__like that`
    * `gettype($var)` returns type of variable.
    * Reserved words    
        `abstract` `and` `array` `as` `break` `case` `catch` `class` `clone` `const` `continue` `declare` `default` `die` `do` `echo`, `else`, `elseif` `empty` `enddeclare` `endfor` `endforeach` `endif` `endswitch` `endwhile` `eval` `exit` `extends` `final` `for` `foreach` `function` `global` `goto` `if` `implements` `include` `include_once` `instanceof` `insteadof` `interface` `isset` `list` `namespace` `new` `or` `print` `private` `protected` `public` `return` `static` `switch` `throw` `trait` `try` `use` `var` `while` `xor`  and for more at http://php.net/manual/en/reserved.php
    * `.=` is concatenate equals.
    * `strtolower("String")`, `strtoupper("String")`, `ucfirst("String")`, `ucwords("String")`
    * `trim(" Str ing ")` deletes spaces in beginning and ending.
    * `strlen("String")` returns the length of the string. 
    * `str_replace("replace this ", "with that")`.
    * `strstr("string","find")` finds "find" in "string".
    * `str_repeat($var, 4)` repeats $var 4 times.
    * `rand()` or `rand(min,max)` returns random number.
    * `is_int($integer)` , `is_float($float)`, `is_numeric($var)`
    * Boolean returns "1" as string when it is true, returns nothing when it not true.
    * `null` or `NULL` is nothing and if a variable has been not set, its value is `NULL`     
    `is_null($var)` `is_set($var)`
    * `empty($var)` returns true when $var is empty and in PHP `""`, `null`, `0`, `0.0`, `"0"`, `false` and `array()` considered as empty.     
    * `settype($var, "type")`  or `(type)$var` converts  var to type.
        (Type => `string`, `int`, `integer`, `float`, `array`, `bool`, `boolean`)
    * `define("VAR_NAME", value)` defines a constant.

 
* **Arrays**
    * `$array_name = array();` defines empty array.   
      `$mixed = array(6 ,"str", "dog", array(1,2,3))`
    * `$array_name[] = 1` adds number 1 to the end of array.
    * in PHP 5.4 you can define array as `$array=[E1,e2,e3]`
    * Associative array `$assocArray = array("first_name" => "John", "last_name"=>"Stevens");` and we can get name with `$assocArray[first_name]`
    * `print_r($array)` returns whole array to output.
    * `count($array)` returns number of items in array.
    * `max($array)` and `min($array)` returns max/min values in array. 
    * `sort($array)` and `rsort($array)` sorts array ascending/descending order. 
    * `implode("seperator",$array)` returns array as string that we want.
        more at https://secure.php.net/manual/en/ref.array.php

* **Control Structures**
    * **If** `if (logical_exp){statment}`
    * **If-Elseif-Else** 
    ```php
    if (logical_exp){
    statment}
    elseif(logical_exp){
    statment}
    else{
    statment}
    ```
    * `==` means equal and `===` meas idendical.
    * `>`, `<`, `>=`, `<=`, `<>`, `!=`, `!==`, `&&`, `||`, `!`
    

    * **Switch-Case**
        ```php
        switch($var){
        case value1: statement; break;
        case value2: statement; break;
        case value3: case value4: statement; break;
        ...
        default: statement; break;
        }
        ```

    * **While loop**
    ```php
    while(expression){
    statements;
    }
    ```
    * **For loop**
    ```php
    for(initial; control; each){
    statements
    }
    ```
    * **Foreach loop**
    ```php
    foreach($array as $value)
    statements; 
    ```
    current element in the array assigns to $value
    ```php
    foreach($array as $key => $value)
    statements; 
    ```
    * `continue();` skips current. (continue() == continue(1) 1 is the level of loop, if there is a loop inside loop and if it is 2, it skips current state of both loops.)
* Array Pointer `next($array)`, `current($array)`, `reset($array)` 
* Assigments are also a regular experession. If variable succesfully asigned then it returns true.
```php
while($var = current($array)){
    Statements;
}
``` 
this loops run until it gets end of the array

* **Functions**
    * 
    ```php
    function func_name(parameters_optional=defaultvalue){
    statements;
    return value_optional;
    }
    ```
    * Functions can be used before it is defined.

* **Building Web Pages with PHP**
    * Making link in html `<a href="page.php">CLICK HERE</a>`
    * Sending a value to another page with query parameter.
    For example PHP stores category and page id for this URL (`page.php?category=7&page=3`) in an associative array named `$_GET`
    and we can access these ids with `$_GET['category']` and `$_GET['page']`   
    and we can and more than one parameter by seperating  them with `&` 

    * Reserved characters in URLs
    `!` `#` `$` `%` `&` `'` `(` `)` `*` `+` `,` `/` `:` `;` `=` `?` `@` `[` `]`
    to be able to use these characters in the URL, we must encode them with `urlencode($string)` (spaces become `+`) function, or `rawurlencode($string)`(spaces become `%20`) function. 
        * `rawurlencode` is most compatible, and mostly using for characters before `?`.
        * `urlencode` mostly using for characters after `?`. 

    ```php
    <?php $link_name = "Second Page"; ?>
    <?php $id= 2;?>
    <?php $company= "Johnson & Johnson";?>
    <a href="second_page.php?id=<?php echo $id;?>&company=<?php echo $company;?>"><?php echo $link_name; ?></a>

    ```
    * Reserved characters in HTML
    `<` `>` `&` `"` to be able to use these characters in page, we must encode them with `htmlspecialchars($string)` or `htmlentities($string)`(also encode high level ascii chars like €,§,™ ...) in PHP. 
    
    * To include another php file `include("file.php")`
    * `require("file.php")` is same with include, but it will throw error when file not found.
    * Headers should be set in the very top of the code.
    `header("content")`
    * Redirecting to a link.`header("Location: path.php");exit;`
    ```php
    <?php 
    function redirect_to($new_location)
    header("Location: ".$new_location);
    exit;
     ?>
    ```   

* **Working with Forms and Form Data**
    * Like `$_GET` in links, php keeps all form data in an associative array that we can access by `$_POST`
    * There is two pages; the one that has the form that shoud be filled and the one that access that form data. Both are either be same pages or different. 
    * Forms can be created like below. `action` is the file that we want to access data in. We can access data with name parameters.`$_POST["username"]`
    ```html
    <form action="form_process.php" method="post">
        Username: <input type="text" name="username" value=""/><br/>
        Password: <input type="password" name="password" value=""/><br/><br/>
        <input type="submit" name="submit" value="Submit"/> 
    </form>
    ```
    * Validating form values
        * `if(!isset($value)||empty($value))`
        * String Length `if(strlen($value)<$min)` or `if(strlen($value)>$max)`
        * Type `if(!is_string($value))` or `if(!in_array($value, $array))` or ...
        * Format `if(!preg_match("reg_exp", $string))`
        * Check databese for uniqeness.
        * eg. `if(strpos($value,"@)" === false)` controls that e mail address is valid or not.  
   

* **Working with Cookies and Sessions**
    * Setting cookie `setcookie($name, $value, $expire)`    
    (eg. `$name="test"` `$value=40` `$expire=time()+(60*60*24*7)` time() returns current time and this cookie has 7 days lifetime)
    * Setting cookie is adding a header to the page. We should set in the very top of the page unless output buffering is turned on.
    
    * Getting value from cookie `$_COOKIE[$name]`
    * Unsetting cokie `setcookie($name, null)`
    * Sessions


* **MySQL Basics**
    * Accessing  MYSQL via terminal `mysql -u username -p` 
    * Show databases with ` SHOW DATABASES;`
    * Creating `CREATE DATABASE db_name;`
    * Using `USE db_name;`
    * Dropping database `DROP DATABASE db_name;`
    * Giving permission to a user to acces databese. 
    ```mysql
    GRANT ALL PRIVILEGES ON db_name.* 
    TO 'username'@'localhost' 
    IDENTIFIED BY 'password';
    ```
    * Showing privileges `SHOW GRANTS FOR 'username'@'localhost';`
    * Showing tables in database we are working on. `SHOW TABLES;`
    * Creating table 
    ```mysql
    CREATE TABLE table_name(
    column_name1 definition,
    column_name2 definition,
    colomn_name3 definition,
    options
    );
    ```
    * Showing columns `SHOW COLUMNS FROM table_name;`
    * Dropping table `DROP TABLE table_name;`
    * eg. 
    ```mysql
       CREATE TABLE subjects ( 
    -> id INT(11) NOT NULL AUTO_INCREMENT,
    -> menu_name VARCHAR(30) NOT NULL, 
    -> position INT(3) NOT NULL,
    -> visible TINYINT(1) NOT NULL,
    -> PRIMARY KEY(id)
    -> );
    ```
    * **CRUD** (Create, Read, Update, Delete)
        * SQL SELECT (read)(last two line is optional)
        ```mysql
        SELECT *
        FROM table
        WHERE column = 'some_text'
        ORDER BY column1 ASC;
        ```

        * SQL INSERT (create)
        ```mysql
        INSERT INTO table (column1, column2, column3)
        values (val1, val2, val3);
        ```

        * SQL UPDATE (update)
        ```mysql
        UPDATE table
        SET column1 = 'some_text'
        WHERE id = 1;
        ``` 


        * SQL DELETE (delete)
        ```mysql
        DELETE FROM table
        WHERE id = 1;
        ``` 
   
* **Using PHP to Access MySQL**
    * APIs > `mysql`, `mysqli` and `PDO`
    * Creating database connection
        * assign `mysqli_connect($dbhost, $dbuser, $dbpass, $dbname)` to a variable.
        * `mysqli_connect_error()` and `mysqli_connect_errno()` shows errors. 
    * Performing database query.
    `mysqli_query($connection_name, $query)`
    * Using returned data
    `mysqli_fetch_row($returned_data)`  results are in a standard array and keys are integers.   
    `mysqli_fetch_assoc($returned_data)` results are in a associative array and keys are column names.     
    `mysqli_fetch_array($returned_data)` results are in either or both types of arrays.   
    ```
    while ($row = mysqli_fetch_row($result)){
    var_dump($row);
    echo "<hr />";
    }
    ```
    * Releasing returned data. 
    `mysql_free_result($result)`

    * Closing database connection
    `mysqli_close($connection_name)`

    * Other Functions
        * `mysqli_affected_rows($connection)` returns number of rows that were affected by last change. 
        * `mysqli_real_escape_string($connection, $string)` adds backslashes in proper places to avoid sql injection.
        ...


* **Building a Content Management System (CMS)**

* **Using Site Navigation to Choose Content**

* **Application CRUD**

* **Building the Public Area**

* **Regulating Page Access**
