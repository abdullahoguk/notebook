#Notes for "Deep JS Foundations" course by Frontend Masters(Kyle Simpson)
##Scope and Closures (Nested Scope, Hoisting, Closure, Modules)
- Scope: where to look for things(where variable,identifier etc. belongs to)
- JS runs in at least two passes (first pass ~compile, second pass run)
- Scoping happens in first pass
- JavaScript has function scope only*
###Example
```js
var foo = "bar";

function bar() {
    var foo = "baz";
}

function baz(foo) {
    foo = "bam";
    bam = "yay";
}
```
---
- first pass (look for formal declerations(`var` `function` `parameters` etc. ) by asking scope managers and arrange them. answers are `yes` or `no`) 
    - ask `global scope` for foo(line1). answer:no
    - put that foo to `global bucket`

    - ask `global scope` for bar(line3). answer:no
    - put that bar to `global bucket`
    - go to bar and enter `bar scope`
    - ask `bar scope` for foo(line4). answer:no 
    - put that foo to `bar bucket`

    - ask `global scope` for baz(line7). answer:no
    - put that baz to `global bucket`
    - go to baz and enter `baz scope`
    - ask `baz scope` for foo parameter(line7). answer:no
    - put that foo to `baz bucket`
    - no information about bam(line9) (don't have `var` keyword) it is not a decleration, look into that later. 
---
- Executing (second pass) (no more var and function keywords. look for `LHS`>assignment and `RHS`>reading or value by asking scope managers. Answers are `yes` or `No, look elsewhere`)
    - ask `global scope` for foo(line1) LHS. answer: yes
    - find value on the right("bar") and assign it to that foo.
    - bar and baz functions haven't called anywhere. exit.
    
    if functions called, that will continue like > 

    - bar called
    - ask `bar scope` for foo LHS. answer: yes
    - find value on the right("baz") and assign it to that foo.

    - baz called (with no parameters lets assume)
    - ask `baz scope` for foo LHS. answer: yes
    - find value on the right("bam") and assign it to that foo.
    - ask `baz scope` for bam LHS. answer: no look elswhere
    - go to one scope level up(`global scope`) and ask for bam LHS. answer: no but I can create (because global is the end and there is nowhere else to go)
    - create global variable bam on `global scope` and assign right value ("yay") to.
---
- declaring variables without `var` is not recommended
- On using strict mode(by adding `"use strict"` on top), undeclared variables like bam throws error(Reference error:bam is not defined.). 
- Use strict mode.
     


