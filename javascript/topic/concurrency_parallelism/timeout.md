1-  Is Javascript a synchronous language?

Yes, It can be defined as a synchornously executed language. 

- The main reasons is that all the functions are executed thorugh a call stack structure.
- Call stack has LIFO data strucutre and can execute only function at a time.
- Although, there are several techniques to make javascript flow/executions defined as async.

2- What is Javascript Engine.

Javascript runtime environment is composed of four main code containers and an event loop, which together form modern JavaScript runtime environment. Those containers are

- Heap
- Stack
- Browser specific APIs
- Callback queue

Goal of former is to read the code and execute it, Where as Event Loop performs a synchronization b/w Javascript engine and functions executed in browser APIs.

3- setTimeout()

```
// example #01
// register timeoUt()
setTimeout(function(){
  console.log('third');
}, 1000);

function executeFirst(){
  console.log('first');
};

function executeSecond(){
  console.log('second');
};

executeFirst();
executeSecond();

// output

"first"
"second"
"third"


// example #02
// register timeoUt()
setTimeout(function(){
  console.log('third');
}, 0);

function executeFirst(){
  console.log('first');
};

function executeSecond(){
  console.log('second');
};

executeFirst();
executeSecond();

// output

"first"
"second"
"third"

// still the output is same, Let's understand how the javascript runtime works

```
As we know there are Four Components Heap, Stack, Callback Queue, WebAPI

#### Start 
Heap|Stack|WebAPI|Callback Queue
--|--|--|-
.|.|.|.
.|.|.|.

Heap|Stack|WebAPI|Callback Queue
--|--|--|-
.|.|.|.
.|setTimeout(1000)|.|.

Heap|Stack|WebAPI|Callback Queue
--|--|--|-
.|.|.|.
.|.|setTimeout(1000)|.

`As setTimeout() will register an event on WebAPI container, Which will wait for a specified time, and push the callback function to Callback Queue`

Heap|Stack|WebAPI|Callback Queue
--|--|--|-
executeSecond()|.|.|.
executeFirst()|.|.|callback()

`it register two functions executeFirst, executeSecond on the heap, after that it calls to executeFirst and this push it to Stack and executes immediately and then executeSecond.`

Heap|Stack|WebAPI|Callback Queue
--|--|--|-
.|.|.|.
executeSecond()|executeFirst()|.|callback()

Heap|Stack|WebAPI|Callback Queue
--|--|--|-
.|.|.|.
.|executeSecond()|.|callback()

Heap|Stack|WebAPI|Callback Queue
--|--|--|-
.|.|.|.
.|.|.|callback()

`as stack is empty, callback will be pushed`

Heap|Stack|WebAPI|Callback Queue
--|--|--|-
.|.|.|.
.|callback()|.|.

**NOTE** : `.` represent empty.
