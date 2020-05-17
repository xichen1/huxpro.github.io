---

layout:     post
title:    "js study note"
subtitle:   
date:     2020-05-16
author:     "rick"
header-img: 
tags:
- Book note
---
### This is the study note for the book "Professional JS for web developer".

## <u>Chapter 2 JS in HTML</u>
### How to use the \<script> element in HTML.
1. Use the attribute src to interprete the external file.
    * While using the src attritube, the code between \<script> and \</script> will be ignored.
    * src attribute can also get the js file from outside domains by sending a GET request to the path and get the returned file.
    * Without the defer and async attribute, the scripts will be interpreted in order.
2. Where to put the \<script> tag
    * Traditionally, all such elements were put in the head element.
    * However, it may couse the problem which leads the page process the code before the page begins rendering.
    * So the modern way is to put the tag in the end of the body element and after the content in body.
3.  defer attribute
    * By setting the defer attribute, and putting the script tag in the head element, the browser will download the script immediately but will not run the code until the whole page is parsed. (They will not be excuted until the \</html> tag).
    * defer only works for the external script.
    * Compared with the defer attribute, it is a better practice to put the script at the bottom of the page.
4.  Asynchronous scripts (async attribute)
    * The attribute async is similar with defer, it only applies to the external code and let the browser to download and not run the code.
    * The difference is it will not guarantee the order if there are two such script with the attribute.
    * Another difference is whenever the script is downloaded completely, the process to the HTML will suspend and start to run the script. Only when the script is excuted the process will continue.
    * This is also not a good practice.
5.  Dynamic script loading
    // TO DO
6.  Inline code versus external files
    * It's generally a better practice to include JS in the external files
    * Reason 1: It has the better maintainability
    * Reason 2: Browsers cache all external files. So when two pages are using the same external files, it will be downloaded once. 

## <u>Chapter 3 Language Basic</u>
1.  Strict Mode
    * From ES5, the strict mode is introduced. It can show some erratic behavior and errors are thrown.
    * To enable the strict mode for the whole stript, include "use strict"; at the top of the file.
    * It can also be used in a single function by putting it at the top of the function
2.  Variables
    - var
        * JS variable are loosely typed, which means one variable can hold any type of data.
        * There are three keywords used to declare the variable: var(all versions), let(ES6) and const(ES6).
        * We can define and set the value for the variable at the same time: var message = "hi";.
        * JS supports to change the data type of one var by overwriting but it's not recommended.
        * Variable defined by var is the local variable, which means after leaving current function, it will be destoried and it cannot be called outside the function. By removing the keyword *var*, it can become the global variable but it is not recommended.
        * When the variable is defined in a fucntion, the defination will be "hoisted" to the top of the function automatically. The order to use and to define does no matter.
    - let
        * *let* is similar with *var*, the difference is that *let* is block scoped.
        * So *let* can only work in one block like if statement, for loop while *var* can be used in the whole function.
        * *let* does not allow the redundant declarations in a block scope. So we cannot define the same variable more than once using let.
        * *let* and *var* cannot be used to define the same variable.
        * *let* has no function of hoisting. So it will not be defined first when it is put behind.