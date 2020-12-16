---
layout: post
title:      "Beginner Tips: Async/Await"
date:       2020-12-11 10:52:40 -0500
permalink:  beginner_tips_async_await
---


As a Flatiron student, one of my projects involved making a single page application that utilized a Rails API backend with a Javascript, CSS and HTML frontend. I ended up making a (simplified) version of the Korean card game Hwatu, also known as Hanafuda in Japanese. Little did I know at the beginning of the project, I would soon be diving head first into the world of async/await. Hopefully the knowledge I gained through my struggles will be of use to future students and aspiring software engineers. 

# What is Async/Await?
Async is simply syntactic sugar for promises. If you’re unsure about what promises are, here is a very helpful article [https://iainjames88.medium.com/javascript-promises-cheat-sheet-65778316dabb](http://).
You can create an async function by prepending a function with async.

```
const someAsyncFunction = async () => {
  console.log('Hello!');
};
```

With async added to the function you can then use the await keyword to wait for a fulfilled promise before continuing with the function.
Please note that await must be added **before** a function that returns a promise (in other words, another async function). 

```
const sayHello = async () => {
  console.log('Hello!');
};

const greeting = async () => {
  // Pause the execution of greeting() until sayHello() fulfills
  await sayHello();
  console.log('How are you?');
};

greeting();

Outputs ➜ 
Hello!
How are you?
```

# Async Cannot Be Used With .forEach
One of the first issues I ran into was using async with .forEach. Unfortunately, it took me awhile to realize that they are not compatible. This is due to the fact that .forEach only **invokes** a function, which means it does not wait for the function to end before moving on with the next iteration. There are a few options when it comes to remedying this. One option is to use .reduce.

```
const timeout = async (t) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(), t);
  });
}

const arr = [1, 2, 3];

const printInOrder = async (asyncFunction, array) => {
  await array.reduce(async (asyncFunction, currentValue) => {
	  await asyncFunction;
	  console.log(currentValue);
  }, undefined);
  console.log("Hello")
}

Outputs ➜ 
1
2
3
Hello!
```

Reduce allows you to iterate through an array, call an async function on a given element, **wait** for that to resolve, then continue with the iteration.

# Await Does Not Block The Execution Stack
Await only pauses the code inside the function it was used in. It does not block all the way up the call stack. What does this mean? Let's take a look by refactoring the first code block.

```
const timeout = async (t) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(), t);
  });
}

const sayHello = async () => {
  await timeout(4000);
  console.log('Hello!');
};

const greeting = async () => {
  await timeout(4000);
  console.log('How are you?');
};

const sayHelloAndGreet = async () => {
  await sayHello(); 
  greeting();
};

sayHelloAndGreet()
  .then(() => console.log('Finished saying hello and greeting!'))
  .catch(e => console.error(e));


Outputs ➜ 
Hello!
Finished saying hello and greeting!
How are you?
```

Does the output order surprise you? This occured because **await** was not used before calling greeting() in sayHelloAndGreet(). Because there is no await, sayHelloAndGreet() simply invokes greeting() but does not wait for it to fulfill its promise.

The order of operations can be understood as below:
1. The function begins by calling **await sayHello()**. This tells Javascript to wait for sayHello() to fulfill its promise before moving on with the rest of the code.
2. When sayHello() begins, it first executes **await timeout(4000)**. After 4 seconds have passed it prints out "Hello!", fulfilling its promise.
3. Now that sayHello() has finished, sayHelloAndGreet() can continue executing code. The next line invokes greeting(). However, because there is no await before greeting() it does not wait for greeting() to complete and interprets greeting() as  **Promise {pending}**. (Remember that this does not mean greeting() stops executing!)
4. With everything complete in sayHelloAndGreet(), the following **.then** is executed printing out "Finished saying hello and greeting!".
5. However, greeting() is still executing in the background! Once it finishes it then prints "How are you?" to the console. 






