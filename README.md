**Note:** This repository is specific to JavaScript.

### Table of Contents

| No. | Questions |
| --- | --------- |
|   | **Javascript Fundamentals** |
|1  | [Given var a = "String" and var b = new String("String"). What is a==b and a===b? Explain](#Given-var-a=-"String"-and-var-b-=-new-String("String").-What-is-a==b-and-a===b?-Explain) |
|2  | [What will be the output of following code and why?](#What-will-be-the-output-of-following-code-and-why?) |
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
|5  | [What will be in the log output for this code below?](#What-will-be-in-the-log-output-for-this-code-below?) |
    "use strict"
    var name ="subhajit";
    function getName(){
        console.log(this.name);
    }
    getName();

|  |  |
| --- | --------- |
|6 |[In the below code why does **getStatus()** returns value while **getDeadLine()** becomes *undefined*?](In-the-below-code-why-does-getStatus()-returns-value-while-getDeadLine()-becomes-undefined?)|

    const project = {
        status: "in progress",
        deadline:"March 2023",
        getStatus: function(){
            console.log("get status: ", this.status);

        },
        getDeadLine: ()=>console.log("Project deadline is: ", this.deadline)
    }
    project.getStatus();
    project.getDeadLine();

|   |    |
| --- | ---------- |
|7 |[What is the problem for the below code example and what are the solutions for it?](#What-is-the-problem-for-the-below-code-example-and-what-are-the-solutions-for-it) |

    const project = {
        status: "in progress",
        getStatus: function(){
            const manageProject = function() {
                if(this.status === "in progress"){
                    console.log("Recruite Employees")
                }
            }
            manageProject()
        },
    }
    project.getStatus();


|   |    |
| --- | ---------- |
|8 |[Does arrow function has *arguments* keyword?](#Does-arrow-function-has-arguments-keyword)

## &nbsp;
## &nbsp;

## Answers


1. ### [Given var a = "String" and var b = new String("String"). What is a==b and a===b? Explain](#Given-var-a=-"String"-and-var-b-=-new-String("String").-What-is-a==b-and-a===b?-Explain)

    **a==b** will check the value of the variable, where **a===b** will check the object storage reference, a is stored in the pool where b is stored in the heap


   **[⬆ Back to Top](#table-of-contents)**


2. ### [What will be the output of following code and why?](#What-will-be-the-output-of-following-code-and-why?)

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

3. ### [What does **this** keyword refers to? Object or Method?](#What-does-**this**-keyword-refers-to?-Object-or-Method?)

    **this** keyword refers to the object under which, the method is defined. If there is no object the **this** keyword autmatically refer to **window** or **global** object for **browser** and **node** respectively. 


   **[⬆ Back to Top](#table-of-contents)**


4. ### [What is the use of **use strict**?](#What-is-the-use-of-**use-strict**?)

    Using **use strict** will not allow a ***this*** keyword to refer to window or global object (browswer and node respectively), instead it will be undefined or { } respectively, if the method is directly under widnow or global object.

    *Point to note that, in arrow function although strict mode is on it will refer to global or window object*
    Arrow function doesn't have **this**.


   **[⬆ Back to Top](#table-of-contents)**

5. ### [What will be in the log output for this code below?](#What-will-be-in-the-log-output-for-this-code-below?)

        "use strict"
        var name ="subhajit";
        function getName(){
            console.log(this.name);
        }
        getName();
    
    Output will be *"Uncaught type error: cannot read properties of undefined (reading "name")"*. This is because we are using *use strict*, so the *this* inside getNam() function is undefined.
    If we remove the *use strict* it will not be undefined anymore


   **[⬆ Back to Top](#table-of-contents)**

6. ### [In the below code why does **getStatus()** returns value while **getDeadLine()** becomes *undefined*?](In-the-below-code-why-does-getStatus()-returns-value-while-getDeadLine()-becomes-undefined?)
        const project = {
            status: "in progress",
            deadline:"March 2023",
            getStatus: function(){
                console.log("get status: ", this.status);

            },
            getDeadLine: ()=>console.log("Project deadline is: ", this.deadline)
        }
        project.getStatus();
        project.getDeadLine();

    It's happening because of the  rules of *this* in javascript. 
    1. **Arrow functions don't have this**
    2. **This is only for regular methods under object**
    3. **In Arrow function mentioning *this* will get the value from parent scope**
    In the above code, for **getDeadLine** method, the parent scope is not the object block, it's window, so the *this* is refering to *window* only, and in *window*, it couldn't find **deadline** key, that's why its returning *undefined*


   **[⬆ Back to Top](#table-of-contents)**

7. ### [What is the problem for the below code example and what are the solutions for it?](#What-is-the-problem-for-the-below-code-example-and-what-are-the-solutions-for-it)

        const project = {
            status: "in progress",
            getStatus: function(){
                const manageProject = function() {
                    if(this.status === "in progress"){
                        console.log("Recruite Employees")
                    }
                }
                manageProject()
            },
        }
        project.getStatus();

    Problem from the above code is the *this* keyword inside **manageProject** function is *undefined*, that's why it will throw an error saying *Cannot read properties of undefined (reading 'status')*. 
    It is *undefined* because **manageProject** is a regular function definition although it's inside a method, and as per the rule of javascript
    
    **In regular function definition the "this" must be undefined**

    **Solution - 1: The old way**
    In older javascript structure to solve it, in the **getStatus** scope we will declare an another variable asigning *this* to it, and inside the **manageProject** function instead of using *this* we will use that newly created variable name.

        getStatus: function(){
                const self = this;
                const manageProject = function() {
                    if(self.status === "in progress"){
                        console.log("Recruite Employees")
                    }
                }
                manageProject()
            },
    **Solution - 2: Arrow Function**
    In morder javascript, we will use arrow function instead of regular function. Because the rule of javascript says

    **Arrow function don't have this keyword in it's scope**
    
    So it will look to it's first lexical scope which is **getStatus** method and it will solve the problem.

        getStatus: function(){
            const manageProject = ()=> {
                if(this.status === "in progress"){
                    console.log("Recruite Employees")
                }
            }
            manageProject()
        },

   **[⬆ Back to Top](#table-of-contents)**

8. ### [Does arrow function has *arguments* keyword?](#Does-arrow-function-has-arguments-keyword)

    No, like regular functions, arrow function don't have *arguments* keyword

   **[⬆ Back to Top](#table-of-contents)**