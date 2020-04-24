##jQuery
* `<script src="jquery.min.js"></script>`
* Accessing DOM
    * `jquery("tag_name");` 
    * `$("tag_name");` returns all "tag_name" tags
    * `$("#id_name");` returns element that has "id_name" as id. 
    * `$(".class_name");` returns elements that has class of "class_name".
    * `$("#id_name tag_name");` or `$("#id_name").find("tag_name");` returns all tags inside element that has "id_name" as id.
    * `$("li").first("li").parent();` returns ul element.
    * `$("#id_name > tag_name");` returns all direct children tags of element that has "id_name" as id. (not children's children). 
    * `$("#id_name, .class_name");` returns all elements with the class of "class_name" or id of "id_name" all together. 
    * `$(".className").filter(".className2");` returns all object has 'className1' and 'className2'. 
    * `$('#id_name').parent()` or `$('#id_name').child()` returns parent/child node
    * `('#id_name').parents('.class_name')` returns first object's all parents that has class of "class_name". 
    * `('#id_name').closest('.class_name')` returns first object's closest parent that has class of "class_name".
    * `$('h1').addClass('className')` or `$('h1').removeClass('className')` or `$('h1').toggleClass('className')` add/remove/toggle class from that object. 
    * `$("h1").text();` returns text of that element.
    * `$("h1").text("new text");` replaces text of that element.
    * To be able to run code when DOM is ready (onload in JS)
    ```jquery
    jQuery(document).ready(function(){
    <code>
    });
    ```
* Working with DOM
    * Creating DOM node `var price = $('<p>100 TL</p>');`
    * Adding DOM node 
        * `$(".class_name").before(price);` or `price.insertAfter($('.class_name'));`
        * `$(".class_name").after(price);` or `price.insertBefore($('.class_name'));`adds it after with same level 
        * `$(".class_name").prepend(price);` or `price.prependTo($('.class_name'));` add it as first child.
        * `$(".class_name").append(price);` or `price.appendTo($('.class_name'));`
add it as last child.
    * Removing `$(".class_name").remove();`

* Listeners ( `.on(<event>, <event handler>)` )
    * `$('button').on('click', function(){ $('button').remove(); });` Runs when any button clicked and removes all buttons.
    * `$('button').on('click', function(){ $(this).remove();});` Runs when any button clicked and removes only the button that clicked.
    * `$('.vacation').on('click' ,'button', function(){ $(this).remove();});` Runs when a button that has "vacation" class clicked.  
    * EVENTS 
        * Mouse:`click` `dblclick` `focusin` `focusout` `mousedown` `mouseup` `mousemove` `mouseout` `mouseover` `mouseleave` `mouseenter` 
        * Keyboard `keypress` `keydown` `keyup` 
        * Form `blur` `select` `change` `focus` `submit`
        * ` event.stopPropagation(); event.preventDefault();`
    * jQuery Object Methods
        * `slideUp` `slideDown` `slideToggle` 
        * `fadeIn` `fadeOut` `fadeToggle`


    * Example
    ```javascript
    //HTML  >>>  
    <li class="vacation onsale" data-price="300"> <button></button> </li>
    //JS-jQ >>> 
    $('button').on('click', function(){
         var amount = $(this).closest('.vacation').data('price'); //returns 300
         var price = $('<p>Prices start from $'+amount+'</p>');
        $(this).closest('vacation').append(price);
    });



    //Show/hide images when the button is clicked
    $(document).ready(function() { 
        $("#tour").on('click', 'button', function() { 
            $('.photos').slideToggle(); //'slideUp' 'slideDown' 'slideToggle'
        });
    });
   
    ```

* Styling
    * CSS
        * `.css(<attr>, <value>);`  
            >>> `$(this).css('color', '#252b30');`
        * `.css(<object>);`
            >>> `$(this).css({'background-color': '#252b30', 'border-color': '1px solid #967'});`
        * `.show()` and `.hide()` methods == `.css('display', 'block')` 
    * Animation
        * `.animate(<object>);` applies this css as animation (slowly)
        * `.animate(<object>,<speed>);`
        * `$("#p1").css("color","red").slideUp(1900).slideDown(1700);` first it changes color to red then slide up then slide down.
   
   
* **AJAX**
    * 
    ```
    $.ajax('.../sample.html',{
        success: function(response){
         //things to do when request successfully responded
        },
        error: function(request,errorType, errorMessage){
            alert('Error: '+ errorType + ' with message: '+ errorMessage);
        },
        timeout: 3000, //how log request should wait
        beforeSend: function(){
            //things to do before ajax request like loaing screen
        },
        complete: function(){
            runs after both success and error
        }

    });
    ```
    * or
    ```
    $.get('.../sample.html',function(response){
         //things to do when request successfully responded
    });
    ```



