# Intro to TypeScript

So what is TypeScript you might ask?  It's another thing all the cool kids are using these days, so you'd better wise up and learn this thing too!

All jokes aside, TypeScript is a new way to write JavaScript, and one that is a bit more precise when it comes to declaring variables, functions, classes and more.   

If you've ever used another language like `C#` or `Java`, you know that those languages are a bit more strict about variable declaration.   This strict declaration is sometimes known as *static typing*.  JavaScript, by default is a *loosely typed* language.

While this is okay in JavaScript:
```javascript
str = "Hello World";
console.log(str);
```
It's definitely not in C#, we aren't being strict enough about the type:
```csharp
str = "Hello World";
Console.WriteLine(str);
```

![](images/typescript-no-good.JPG "Hello Fail")

This fails in `C#` because we haven't given the variable declared, aka `str` a **type**.  In most programming languages like C#, you need to specify if the variable being declared is of a type of `Integer`, `Float`, `String`, `Boolean`, `Array`, `List` or something else.

A **type** helps the program know what kind of space in memory to allocate for the variable being declared.  In JavaScript, we can get away without declaring a type for the variable, because JavaScript's engine behind the scenes manages our type and memory allocation for us.  

However, in other programming languages, this is not the case -- we need to be specific otherwise we can run into errors later with our program.  

## It's All About Portability And Minimizing Errors

If you're a company like Microsoft, you probably write a lot of C#.  (Windows is a heavy C# language).  Hence, being able to write code in C# and port to JavaScript fast is a dream come true.   Yet, JavaScript doesn't work like C#.  It's got its own rules and quirks developers often have to figure out.  (Functions create objects anyone?)  This causes headaches for many of the developers, and as a result -- TypeScript was created to alleviate some of their pain.

## Do I Need to Learn TypeScript to Be A JavaScript Developer?

At the moment you don't.  Most applications are written in regular JavaScript, and with the new EcmaScript 6 syntax available, you probably don't need to add more complexity to your toolset just yet.   

That said, if you want to be able to use modern JavaScript frameworks like Angular, TypeScript is a requirement.  So it does you some good to learn the syntax eventually.

## Is TypeScript Easy to Learn?

Yes, it's relatively straightforward if you've got a grasp on basic JavaScript fundamentals like being able to declare variables, write and use functions, if/else statements, loops and work with the command line.

## Quick Tutorial

If you want to try out TypeScript right now, the best way to get started is to go to <https://www.typescriptlang.org/> to download the latest version of TypeScript to your computer.  

You can also use Node Package Manager `npm`, if you are a fan of Node.js to download TypeScript, with the command:

```console
npm install -g typescript
```
> This command installs the TypeScript language and compiler globally for your computer.

If all goes well, you should be able to write TypeScript code in your favorite coding editor and use the command line to compile it down to regular JavaScript with the `tsc` command.

### Let's Do An Example Together

After you download TypeScript, open up your favorite editor and let's type in the following code.  

> Note for all my examples, I will be using the latest in JavaScript syntax, aka EcmaScript 6 (ES6).  Not familiar with ES6?  Get my book: [Survive Programming: A RoadMap to EcmaScript 6 - The Latest Version of JavaScript](https://www.amazon.com/Survive-Programming-RoadMap-Version-JavaScript-ebook/dp/B07RXGGQJ5/ref=sr_1_3?keywords=learn+es6&qid=1559086204&s=gateway&sr=8-3)

```js
let myAge: number = 36
let isEmployed: boolean = true
let myName: string = `Vijay is ${myAge} years old and ${ isEmployed : 'is working' : 'is currently broke' }`
```

Save this code in your editor as a TypeScript file, with the extension `.ts`, (so something like myTypeScript.ts).  After that, run the following command in your command line.

```console
tsc myTypeScript.ts
```
If all goes well, you can look at your project folder where your `myTypeScript.ts` file is and see a new file called `myTypeScript.js`.  Congrats! You just compiled your TypeScript code to regular JavaScript code!

```js
var myAge = 36;
var isEmployed = true;
var myName = "Vijay is " + myAge + " years old and " + (isEmployed ? 'is working' : 'is currently broke');
```
You should see this as your output.

### Breaking it Down

Okay, that was cool, but now I'm sure you are wondering what all the `:` stuff means.  Let's break it down.  Remember, JavaScript doesn't have type declarations -- at least explicitly like other languages do.

With TypeScript, we can define what `type` our variable should be with the syntax as follows.

```js
let myAge:number = 36
//this declares a variable of type Number in JavaScript
//in JS, all Number types are float types behind the scenes

let isEmployed:boolean = true;
//declares a boolean (true or false variable) in JavaScript

let myName: string = `Vijay is ${myAge} years old and
${ isEmployed : 'is working' : 'is currently broke' }`;
//this declares a variable of type String in JavaScript
```

So basically, we declare the `type` of the variable after the variable name has been declared, but before the value is set with the `=` assignment operator.  Using TypeScript is a bit more verbose, but as you can see from the example we did, our declarations do look more precise.  If you're good so far, let's move on.

## Arrays & Tuples

We can define our variables as Arrays and Tuples as well.  You may be familiar with an Array, denoted by the `[]` syntax, but Tuples might be new to you unless you've dabbled in a language like Python.  A Tuple is like an Array, but cannot have its values changed after they have been set.

```js
let myArr:number[] = [1,2,3,4,5]
let myArr:Array<String> = ['yolo', 'whazzup', 'rad', 'lol']
```
In both these cases above, we are defining a variable of type Array (either with `[]` syntax or `Array` syntax, specifying the `type` in each case -- `number`, `string`)

```js
let myTuple:[string, number] = ["hello", 2]
```
With a tuple, we must use the same types as the order of definition, meaning we cannot define `myTuple` as such:

```js
myTuple = [10,20];
//Type 'number' is not assignable to type 'string'
```

You also cannot use `string` methods on `number` types and vice versa for values in tuples.

```js
myTuple[0].substr(0,1)
myTuple[1].substr(0,1)
//Property 'substr' does not exist on type 'number'
```
The `substr` method is only available for values declared of type `string`, not of type `number`.

## Functions

Functions can be written for TypeScript as well.  Let's look at an example.

```js
const getEvenNums = (num: number): number[] => {
  let arr = [];

  if (num < 2) return [];

  for (let i = 2; i <= num; i += 1) {
    if (i % 2 === 0) {
      arr.push(i);
    }
  }
  return arr;
};
```

Here we have an example from a member of our [Discord channel](https://discordapp.com/invite/h2568CQ) via #practice, who wrote a function in TypeScript to get all the even numbers between 2 and the `num` passed to the `getEvenNums` function.   

Breaking it down we can see that this function `getEvenNums` takes a single parameter `num` which is of type `number`.  After the `:` we indicate we want a return type of `number[]`, which means a number type array.   So we want to return from this function an array of number types.

The rest of the function body goes inside the curly brackets, feel free to try compiling this code to see what it eventually looks like.

## `any` and `void`

Often with JavaScript, you may work with an older library, not compatible with your shiny new ES6 and TypeScript code.  It's possible you may not know the `type` of values being retrieved from said older library.  In these cases, you can use the type `any` to store the data.

```js
let val: any = $(".result").text()
//get the result from this DOM element, is it a number? a string?
```

With `void`, this is useful whenever we come across a function that does not have a return value.  In regular JavaScript, when a function does not return a value, behind the scenes the compiler returns `undefined` automatically.   

This is why when you use something like `console.log` in your development tools, you see `undefined` appear after logging something.  

The `void` keyword is used mainly in other languages like C# and C to indicate that a function does not have a return value, so for using `void` in TypeScript we can be more helpful to others reading our code to emphasize that our function does not return a value.

```js
let log = (message: string): void => { console.log(message); }
```
Here we create a new function `log` that takes a parameter of `message`, which is of type `string`.  After the parentheses, we see a `:` mark, which indicates what return `type` this function should give us back, aka `void` here (we do not expect a return type other than `undefined`).  

The `=>` and `{}` looks similar to what we already know about fat arrow functions, basically we place our own code inside the brackets.  In this case, we drop in the `console.log` function and pass it our `message`.  Hey it's easier to write `log` than `console.log` right?

## Enums

When I first heard the word `enum`, I was immediately turned off.  "It sounds so ugly, of course it must be complicated to learn", I thought.

The good news is it's not complicated at all, just an ugly name.  If you know how to use an `object` or an `array` in JavaScript, you can pretty much get the gist of an `enum` too.  

An `enum` is just a way to declare a group of datatypes together into something more meaningful.  For example, we could declare a JavaScript object that stores the days of the week like so:

```js
let daysOfWeek = {
  "Mon",
  "Tues",
  "Wed",
  "Thurs",
  "Fri",
  "Sat",
  "Sun"
}
console.log(daysOfWeek[0]) //Mon
```

An `enum` works similarly.

```js
enum DaysOfWeek {
  Monday,
  Tuesday,
  Wednesday,
  Thursday,
  Friday,
  Saturday,
  Sunday
}

let day: string = DaysOfWeek[0]
console.log(day)
//Monday
```
The main differences between a standard JavaScript `object` and an `enum` are:

- enums don't hold values like strings and numbers
- enums hold basically *aliases* for index values starting from `0`
 - `Monday`, `Tuesday` and so on are placeholder aliases for indicies `0` and `1`.
- We can change the index starting order in an `enum`, but not an `object`. We can also change individual indicies if we wish in the `enum`.

Here's an example illustrating that last point.

```js
enum DaysOfWeek {
  Monday = 1,
  Tuesday,
  Wednesday,
  Thursday,
  Friday = 10,
  Saturday,
  Sunday
}
let day: string = DaysOfWeek[10]
console.log(day)
//Friday
```
As you can see enums are a bit more meaningful and customizable than regular JavaScript objects, and help other developers know exactly what to expect when they have a function take in an `enum` parameter versus an `object` parameter.

## Interfaces

If you've got the hang of enums, you pretty much can get interfaces too.

An interface is a way to describe each property's type on an `object`.  So for example, we could write in plain JS:

```js
let car = {
  name: "Toyota",
  model: "Prius",
  wheels: 4,
  engine: "electric",
  odometer: 1000
}
```
While this object is okay, the types on each property like `name`, `model`, `odometer` aren't defined. If we use this object with a function and don't pass in all the properties, we can get some garbage values instead which may throw off our program. We can do better to prevent garbage data by using TypeScript to define an `interface` for our object.

```js
interface Car {
  name: string,
  model: string,
  wheels: number,
  engine: string,
  odometer: number
}

let myCarDataInfo = (car: Car):string => {
  `You drive a ${car.name} ${car.model}.
   It has ${car.wheels} wheels, an ${car.engine} engine
   and has a mileage of ${car.odometer}.`
}

let car = {
  name: "Toyota",
  model: "Prius",
  wheels: 4,
  odometer: 1000
}

console.log(myCarDataInfo(car))
/* Property 'engine' is missing in type
'{ name: string; model: string;
wheels: number; odometer: number; }'
but required in type 'Car'. */
```
Did you catch the error?  We are missing the engine property in our `car` object, so TypeScript's compiler let us know that this object was no good, we need to fix the error before we can use it with our function.  

You can see why using an `interface` is so much more helpful for flagging errors we may not notice on first pass!

## Webpack Integration

If you're tired of using the command line to type out `tsc` each time with your filename, you can wire up your project folder with [Webpack](https://webpack.js.org/) to automatically watch and compile your TypeScript code each time you save.  Let's do a quick example here.

### Install webpack

Using the command line, go ahead and run the following commands:

```console
mkdir ts-test
cd ts-test
mkdir src
mkdir dist
touch src/index.ts
touch index.html
npm init -y
```
We've created our project folder and run the command `npm init -y` which just basically initializes our project folder with an `index.html`, the folders `src` and `dist` (we'll talk about in a minute), an `index.ts` file as an entry point for our project folder's TypeScript code in `src`, and a bare-bones `package.json` file for use with Node.js.

Next let's add a few dependencies to our project, namely the `typescript` module and the `awesome-typescript-loader` loader (to transpile our Typescript code) for Webpack.  Finally we need `webpack` to build our project's `src` folder files and drop them into the `dist` folder as a `bundle.js` file our `index.html` can resource.

Run the following:

```console
npm i typescript awesome-typescript-loader webpack --save-dev
```

While that downloads, let's update our `index.html` file to look like:

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <p id="result">Result goes here</p>
    <script type="text/javascript" src="dist/bundle.js"></script>
  </body>
</html>
```

Create two config files, one for TypeScript and one for Webpack.  In the console type:

```console
touch webpack.config.js
touch tsconfig.json
```

Now let's modify each file.  Starting with `webpack.config.js` update it to look like the following:

```js
module.exports = {
  entry: "./src/index.ts",
  output: {
    filename: "bundle.js",
    path: __dirname + "/dist"
  },
  resolve: {
      extensions: ['.ts', '.js']
  },
  watch:true,
  module: {
    rules: [
      {
        test: /\.ts?$/,
        loader: 'awesome-typescript-loader'
      }
    ]
  }
};
```
Breaking it down, we're saying to webpack that we want our `entry` to be our `src/index.ts` file (our main TypeScript file).  The build from webpack should go to our `dist` folder via `output: { filename: 'bundle.js', 'path:__dirname + "/dist"'}`.

We want webpack to `resolve` file extensions .ts and .js in our project, and then add a `watch` parameter (set to `true`) so webpack will watch our code as we change and recompile (hence saving you from typing `tsc`).

Finally we config the `module` area with `rules` that we want to use the `awesome-typescript-loader` to transform any `.ts` files in our project.

Next, we need to update our `tsconfig.json` file.  Let's do that.  Here, I just modified a configuration from the [TypeScript handbook](https://www.typescriptlang.org/docs/handbook) but we can break it down.

```js
{
    "compilerOptions": {
        "outDir": "./dist/",
        "module": "commonjs",
        "target": "es6",
    },
    "include": [
        "./src/**/*"
    ]
}
```
With a `tsconfig.json` file, we are essentially telling webpack and our compiler that we are using TypeScript, and where essentially we want our files to be sent to in the `compilerOptions` property.   

We have some standard options including `"ourDir"`, which is our `dist` folder, `module` development style we want to use, aka `commonjs`, and `target:"es6"` so our compiler can transpile the latest ES6 features. For more info on additional properties visit <https://www.typescriptlang.org/docs/handbook/compiler-options.html>

One more thing before we can get to the fun part.

Let's update our `package.json` so we can run webpack from the console using just the `webpack` command.

In your package.json look for the `"scripts"` region and update it to look like so:

```js
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "webpack": "node_modules/.bin/webpack"
},
```
Great, now let's write some TypeScript. Go to your `src` folder, then open the `index.ts` file and plug in some TypeScript code, e.g. the following:

```js
let message: string = `Hello World`

document.getElementById('result').innerText = message
```

From your command line, run `webpack`.  You should see webpack start to build and finish.  If there are any errors with your TypeScript, it will tell you in the console so you can fix.  If all is successful, you can open your `index.html` file with your favorite browser to see the result in your `<p id="result"></p>` tag.  

This `index.html` has properly loaded the `bundle.js` file from your `dist` folder, which you can check to see your transpiled TypeScript to plain JavaScript code.

From here, you can keep playing with your TypeScript code and adding more complexity and you should be able to refresh this page with the changes without having to type more commands in your command line.  To finish using webpack, simply hit `Ctrl-C` on your keyboard twice to end the program.  

## Summary on Webpack

Obviously with webpack you can do even more than what was mentioned here including creating a `webpack-dev-server` with `hot-module-reloading` (to create a simple server that loads your page and reloads it on each save), but that discussion is outside of the scope of TypeScript.  (Maybe at a later time, I'll write up an example).  For now, let's keep it simple as we've already covered a lot of material.

## Wrapping it up

Hope this mini guide on TypeScript has been useful to you.  Perhaps this guide motivated you to learn C# as well.  (It is a popular language especially for game development).  If you are still interested in learning more on TypeScript, you can check out the [official handbook](https://www.typescriptlang.org/docs/handbook) on Microsoft's TypeScript website, which gives a lot more detailed examples.  You can also learn all about C# via [Microsoft's C# Programming Guide](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/).

You can also check out a talk by [James Earle of Microsoft](https://www.youtube.com/watch?v=HkR474Y3tVg) who gave a talk at our group on the subject as well via this video.  

[![](http://img.youtube.com/vi/HkR474Y3tVg/0.jpg)](https://www.youtube.com/watch?v=HkR474Y3tVg)

Be sure to subscribe to our [YouTube channel](https://youtube.com/javascriptla) for more videos from our group!  (We record all our meetups).   Thanks for reading!
