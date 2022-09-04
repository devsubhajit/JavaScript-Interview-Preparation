**Note:** This repository is specific to JavaScript.

### Table of Contents

| No. | Questions |
| --- | --------- |
|   | **Javascript Fundamentals** |
|1  | [Given var a = "String" and var b = new String("String"). What is a==b and a===b? Explain](#question-one) |
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
|8 |[Does arrow function has *arguments* keyword?](#Does-arrow-function-has-arguments-keyword)|
|9 |[What is the difference between shallow copy and deep copy for javascript objects?](#What-is-the-difference-between-shallow-copy-and-deep-copy-for-javascript-objects?)|
|10 |[What is short circuit?](#What-is-short-circuit?)|
|11 |[From this below example can you reurn 0 using short circuit?](#From-this-below-example-can-you-reurn-0-using-short-circuit?)|

    console.log(0 || 10)

|    |      |
| --- | ----------------------- |
|12 |[What is higher order function in javascript?](#What-is-higher-order-function-in-javascript?)|
|13 |[How to remove duplicate values from array?](#How-to-remove-duplicate-values-from-array?)|
|14 |[What is partial application?](#What-is-partial-application?)|
|15 |[What is TDZ?](#What-is-TDZ?)|



## &nbsp;
## &nbsp;

## Answers


1. ### [Given var a = "String" and var b = new String("String"). What is a==b and a===b? Explain](#question-one)

    **a==b** will check the value of the variable, where **a===b** will check the object storage reference. When we create a primitive data, it's value get stored in the call stack at a particular memory location.

    When we say 
    
        var a = "javascript"
        var b = "javascript"
    Javascript engine checks the value for both and if the value is same, it points to the same memory allocation, it doesn't create new memory allocation. 

    But in case of 

        var c = new String("javascript")
    This is created from *String* object, and objects are not primitve data types, so it will be stored in Heap memory and the memory location of heap will be refered as the value of *var c* in the callstack memory allocation. 

    So when we are checking

        a === b // from the question
    Its basically checking memory location, which is in this case is not same.

    That's why it returns **false**


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

9. ### [What is the difference between shallow copy and deep copy for javascript objects?](#What-is-the-difference-between-shallow-copy-and-deep-copy-for-javascript-objects?)

    Shallow copy copies an object on the first level only, if the object is having nested object, shallow copy method cannot copy that object and cannot create new object reference in the heap storage, instead it points to the same child object reference. Lets understand this through an example:

        const team = {
            name:"blue",
            size:4,
            members:["Arun", "Rajesh", "Aparna", "Deepak"] // array object
        }

        const teamCopy = {...team}
        teamCopy.name = "red";
        teamCopy.members[0] = "Rajendra";

        console.log(team)
        console.log(teamCopy)

    In this above example the output will be:

        1. {name:"blue", size:4, members:["Rajendra", "Rajesh", "Aparna", "Deepak"]}
        2. {name:"red", size:4, members:["Rajendra", "Rajesh", "Aparna", "Deepak"]}
    team name is different as we have changed, that is okay. But look at the *members* object. Although we have changed only in *teamCopy*, but the effect is same in the *team* object also. 

    Shallow copy couldn't create a new Object reference for nested object. Here the solution comes from the deep copy.

        const team = {
            name:"blue",
            size:4,
            members:["Arun", "Rajesh", "Aparna", "Deepak"] 
        }

        const teamCopy = JSON.parse(JSON.stringify(team))
        teamCopy.name = "red";
        teamCopy.members[0] = "Rajendra";

        console.log(team)
        console.log(teamCopy)
    
    And the output are:

        1. {name:"blue", size:4, members:["Arun", "Rajesh", "Aparna", "Deepak"]}
        2. {name:"red", size:4, members:["Rajendra", "Rajesh", "Aparna", "Deepak"]}

    As you can see, we got our expected result here. What is happening here is, we are converting object to a string, which is a primitive data type, it allocates a new call stack memory and store the string value there, later wiht the *JSON.parse()* method we are creating an object and storing in heap memory, and the reference is getting pointed to the call stack variable value with a new memory allocaton.



   **[⬆ Back to Top](#table-of-contents)**

10. ### [What is short circuit?](#What-is-short-circuit?)  

    Javascript short circuite is nothing but the same conditional operators to be used to return any data type instead of boolean data. To understand this in more details lets first know how the **&&** and **||** operators works in programming.

    | A | B  | A and B | A or B |
    | --- | ------- | ------- | ------- |
    | T | T | True | True|
    | T | F | False | True|
    | F | F | False | False|
    | F | T | False | True|

    Form the above table we got these RULES
    1. If any value is false inside **&&** operator=, result will be false
    2. If any value is true inside **||** operator, the result will be true
    3. To get true from **&&** operator, all must be true
    3. To get false from **||** operator, all must be false. 
    5. Wherever it gets it's desired value, will not check next conditions

    So in short circuiting process javascript only return the first truth value (if any) for OR operator and first false value for the & operator

    Example 1:

        console.log(0 || 7) // return 7, 0 is falsy value
        console.log(7 || 9) // return 7, rule number 5 
        console.log(0 || "javascrip") // return javascript

    In the above code, these are correct as any value is true, it will return true, in this case the truth value

    For **and** operator it will do exact oposite of **or** operator.

        console.log(0 && 7) // return 0
        console.log(7 && 9) // return 9 
        console.log(0 && "javascrip") // return 0

    This is also correct, if any value is false, it will return the first falsy value

    **[⬆ Back to Top](#table-of-contents)**

11. ### [From this below example can you reurn 0 using short circuit?](#From-this-below-example-can-you-reurn-0-using-short-circuit?)

    Using **nulish** opertor we can return 0. 

        console.log(0 ?? 10) // returns 0
    
    Because it will only check nullish values, which are *null* and *undefined*.
    So in this case 0 becomes a truth, it returns 0 without checking next element.

    **[⬆ Back to Top](#table-of-contents)**

12. ### [What is higher order function in javascript?](#What-is-higher-order-function-in-javascript?)
    A higher order function is a function which takes another function as a parameter or which has a callback function. We can pass any function as an argument, because in javascript functions are also **first class citizen**. It means it stores value like other variables. And the value type of functions in javascript is object. 

    Lets take an example of HOF (Higher-Order Function)

        const upperFirstWord = function (str){
            const [first, ...others] = str.split(' ');
            return [first.toUpperCase(), ...others].join(' ');
        };
    The above line of code will return any **string** with first word all in capital letters. 
    
    Now lets write the HOF

        const transformer = function(str, fn){
            // fn is a callback function
            // fn has object values, as it is first class citizen
            // fn.name will be the function name.
            console.log(`Transforming by: ${fn.nam}`); 
            return fn(str);
        }
    
    Now lets perform the HOF

        const firstUpper = transformer("Javascript is  awesome", upperFirstWord); 
        console.log(firstUpper);
    
    We will get to logs in browser console

        1. Transforming by upperFirstWord
        2. JAVASCRIPT is awesome. 

    **transformer** function took **upperFirstWord** function as a callback function, **trnasformer** is a Higer-Order Function.

    **[⬆ Back to Top](#table-of-contents)**

13. ### [How to remove duplicate values from array?](#How-to-remove-duplicate-values-from-array?)

    The algorithm behind this problem is to iterate each items of the array and check if it's position or index is repeating or not. 

    It means if an item is at 0 index, and the duplicate of the same item is at 8th index, on search of index of 8th positioned item will return 0. In this case the item on 8th position is duplicate item.

    Lets try on code:

        const arr = ["Ramesh","Pooja", "Arijit", "Ramesh", "Pooja"]
        const newArr = [];
        for(const name of arr){
            if(newArr.indexOf(name) == -1){
                newArr.push(name);
            };
        };
    
    Using **filter()** method:

        const arr = ["Ramesh","Pooja", "Arijit", "Ramesh", "Pooja"];
        const newArr = arr.filter((name, index)=>  arr.indexOf(name) === index);

    Using **set()** method:

        const arr = ["Ramesh","Pooja", "Arijit", "Ramesh", "Pooja"];
        const newArr = [...new Set(arr)];

    **Set** is a new data type, introduced in ES6. The main advantage of **set** is, it always returns an unique value of sets, it means it cannont contain duplicat value, just like other programming languages such as **Python**



    **[⬆ Back to Top](#table-of-contents)**

14. ### [What is partial application?](#What-is-partial-application?)    

    When the parts of the arguments are specified beforehand, this common pattern is known as partial application. 

    Lets understand from this below code:

        const itcHotels = {
            hotel:"ITC Royal",
            code:"ITC",
            bookings:[],
            book(roomNum, name){
                let bookingObj = {hotel:`${this.code}${roomNum}`,name};
                this.bookings.push(bookingObj);
            }
        }
        const tajHotels = {
            hotel:"Taj Bengal",
            code:"TAJ",
            bookings:[]
        }

    Above on the code we have two hotel objects, but only **ITC** has the **book** method. Now we will **bind** booke method to **TAJ** hotel object.

        const book = itcHotels.book; // storing the value of book method
        const tajBook = book.bind(tajHotels);  
    
    Till now the code is a normal bind method. It's not yet **partial application**

        const tajBook101 = book.bind(tajHotels, 101);
    
    In this bind method, **tajBook101**, the **roomNum** argument is specified. It is basically means that a part of the arguments of the original function **itcHotels.book** are already applied. So **tajBook101** is a *partial applicaton*
    
    

    **[⬆ Back to Top](#table-of-contents)**
15. ### [What is TDZ?](#What-is-TDZ?)
    Temporal Death Zone or TDZ is a feature of javascript hoisting.
    To understand that lets see the Javascript Hoisting Table below. 

    |  | Hoisted  | Initial Value | Scope |
    | --- | ------- | ------- | ------- |
    | function declaration | Yes | actual function | block|
    | var variables | Yes | undefined | function|
    | let and const variable | No | uninitialized, TDZ | block|
    | funciton expressions and arrows |  | Depends on variable type | |

    From the above table, if we declare a variable either with **let** or **const** and try to access it before it will throw error as it was not hoisted. So this will create a temoral death zone.

    Lets understand with code:

        console.log(x)
        let x = "javasript"
    
    **x** is being called before it's initialization, this code is an example of **TDZ**

    **[⬆ Back to Top](#table-of-contents)**