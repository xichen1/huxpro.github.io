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
        * Since let has no function of hoisting, when the same variable is decleared twice in two global script blocks, it will throw the error while var will not because it is hoisted and combained with the other ones.
        * typeof and try/catch cannot check if one variable has been decleared by let because it will create a block and the new let is inside the block.
        * when we use var to define the i in the loop, the i outside of the loop block will be the end i in the loop while i will be undefined if it is let.
    - const
        * const is similar to let, but it can only be initialized when it is decleared. Also changing its value will cause the runtime error.
        * We cannot change the value of the variable, however, we can modify properties inside the object.
        * const cannot be used in for loop. In some kinds of for loop, const can be used because the loop will not change it value.
3.  Data type
    - There are six simple data types and one complex data type. The simple ones are: undefined, null, boolean, number, string and symbol. The complex one is object, it is a list of name-value pairs.
    - Use typeof operator to check which type is assigned. (typeof aaa/ typeof(aaa)) typeof is an operator so the parentheses are not required.
    - undefined variable
        - The undefined variable has only one value which is undefined.
        - The undefined variable is different with the variable which was not decleared at all. Use the back one directly will cause error. However, when applying typeof operator to a variable which is not decleared, it will return "undefined" and typeof is the only useful operation to this kind of variable.
        - The undefined variable is falsy. So it behave like false and the if statement treats it as false.
    - null type
        - a null value is an empty object pointer so typeof will return "object" it the value is null.
        - The valu undefined is the derivative of null and (null==undefined) will return true.
        - null value is falsy, so same as undefined, it can be used in conditional statement and it is treated as false.
    - Boolean type
        - The true is not equal to 1 and false is not equal to 0. However, any number except 0 is treated as ture in the condition judgement, while 0 is treated as false.
        - That is because all other types can be converted into the boolean type by the function Boolean(...). Any nonempty str and any nonzero number are converted into true while all empty string, 0 and NaN are converted into false.
    - Number type
        - To use/represent a octal number, add a 0 in front of the number. If there exists any number out of 0-7 it will remove the 0 and treat it as decimal. Octal literals are invalid in strict mode.
        - When there is no number after the decimal point, or it is 0 after the point, js converts it auto to a int variable.
        - Because of IEEE 754, the numbers are operated in binary format and that will cause very small difference compared to the real result. For example, 0.1 + 0.2 will result 0.30000000000000004. So avoiding using opeartion in flow control.
        - The smallest number that can be represented in js is stored in Number.MIN_VALUE and the largest is Number.MAX_VALUE. The number out of the range is Infinity and -Infinity. We can use the function isFinity to check if a number is in range or not.
        - NaN is short for *Not a Number*. It is used to indicated that an opeartion failed to return a number. But it is different to the error. For example, when divide some number by 0, NaN will be returned. Any opeartion involving NaN always returns NaN. NaN is not equal to any value including itself NaN.
        - The function isNaN() tries to convert the argument to number. When it recive NaN and any string which is not a number str, it returns true. For the other situations like reciving a number, a number str and a boolean, it will return false.
        - Three functions to convert to number: Number(), parseInt() and parseFloat().
    -String type
        - ", ' and ` can be used to delineate strings, but they cannot be mixed to usd.
        - There are some string literal: \n, \t, \b...
        - Two ways to convert a value to a string: method toString() and the function String(). The difference is the null and undefined variable has not toString attribute and String() can convert them into "null" and "undefined".
        - Template literals is introduced in ES6. New line break in the string is seen as the \n so it can be used to define HTML easily without any \n.
        - Template literals can be used for interpolation. The js expression is inside ${}. For example `${value} to the ${exponent} power is ${value * value}``; The value being interpolation will be converted using toString(). And string can also be interpolated.
