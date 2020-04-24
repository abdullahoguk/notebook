##Meteor JS
* **Installing**
    * Install `NODE` and `METEOR`
    * Create project with 
    ```
    $ meteor create project_name
    $ cd project_name
    $ meteor
    ```
* Creating Template (in html file)
```
<template name="hello">
  <button>Click Me</button>
  <p>You've pressed the button {{counter}} times.</p>
</template>
```
* Using template (in html file) `{{> hello}}`
* Creating template helper (in JS file) 
    ```
    if(Meteor.isClient){
        Template.body.helpers({
          
        })
    }
    ```
