**Note:** This repository is specific to JavaScript.

### Table of Contents

| No. | Questions |
| --- | --------- |
|   | **Javascript Fundamentals** |
|1  | [Given var a = "String" and var b = new String("String"). What is a==b and a===b? Explain](#Given-var-a=-"String"-and-var-b-=-new-String("String").-What-is-a==b-and-a===b?-Explain) |
|2  | [What will be the output of following code and why?](#What-will-be-the-output-of-following-code-and-why?) 
|
    console.log(muliply(2,3))
    console.log(add(2,3))

    function muliply(a, b){
        return a*b;
    }
    var add = (a, b)=> a+b;


|  |  |
| --- | --------- |
|3  | [What does **this** keyword refers to? Object or Method?](#What-does-**this**-keyword-refers-to?-Object-or-Method?) |
|4  | [What is the use of **use strict**?](#What-is-the-use-of-**use-strict**?) |

## Answers


1. ### Given var a = "String" and var b = new String("String"). What is a==b and a===b? Explain

    **a==b** will check the value of the variable, where **a===b** will check the object storage reference, a is stored in the pool where b is stored in the heap


   **[⬆ Back to Top](#table-of-contents)**


2. ### What will be the output of following code and why?

        console.log(muliply(2,3)) 
        // output: 6 

        console.log(add(2,3))
        // output: TypeError: add is not a function

        function muliply(a, b){
            return a*b;
        }
        var add = (a, b)=> a+b;

    Because of javascript hoisting, the normal function definition will get hoisted and will have it's initial value as it's definition. 
    Which is the case for **multiply()** function

    But for ***var add = (a, b)*=> a+b** is a normal variable, which will be hoisted first with asigned value ***undefined*** and ***undefined(a,b)*** is not a function 


   **[⬆ Back to Top](#table-of-contents)**

3. ### What does **this** keyword refers to? Object or Method?

    **this** keyword refers to the object under which, the method is defined. If there is no object the **this** keyword autmatically refer to **window** or **global** object for **browser** and **node** respectively. 


   **[⬆ Back to Top](#table-of-contents)**


4. ### What is the use of **use strict**?

    Using **use strict** will not allow a ***this*** keyword to refer to window or global object (browswer and node respectively), instead it will be undefined or { } respectively, if the method is directly under widnow or global object.

    *Point to note that, in arrow function although strict mode is on it will refer to global or window object*
    Arrow function doesn't have **this**.


   **[⬆ Back to Top](#table-of-contents)**