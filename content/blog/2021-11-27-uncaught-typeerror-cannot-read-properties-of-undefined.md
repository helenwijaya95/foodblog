---
layout: blog
title: "Uncaught TypeError: Cannot read properties of undefined "
date: 2021-11-27T13:19:50.933Z
---
![Uncaught TypeError](/images/upload/type-error.jpg "Uncaught TypeError")

Hey ho Javascript Ninjas, have you encountered such an error when accessing an object properties?

You're not alone. It happens because you're referencing a non-existent property. Let's jump on to an example.

`const obj = {
    name:'Solar',
    contact:{
        address: 'Seoul',
        phone:'08939'
    },
    age: 30
}`

It's a usual nested object initiation, we're not there yet.

`console.log(obj.contactNumber.phone);`

Do you see something's wrong?

It targets an **undefined key**, 'contactNumber', so you will get the 'TypeError' message in the browser.

In this case, we can just fix the code to remove the error.

`console.log(obj.contact.phone); // output: 08939`

Pretty simple so far. But let's see a more usable example in below function:

`function displayGreetings(){
   const phoneNumber = obj.contactNumber.phone;
   return Hi ${obj.name}, please confirm if this is your phone number ${phoneNumber}
}`

What will happen if we call the function?

Yes, the code execution will stop at the phoneNumber initiation because contactNumber is a non-existent key. In this case, it's better to put a kind of a 'checker' before accessing a deep level key. What's actually is a checker? Please continue to the next section.

## How to Prevent Accessing an Undefined Object Key

### **1. Create a Conditional**

In the previous example, the obj object is 2-levels deep. By assuming the obj is not null or undefined, we can just put a ternary like this

***ES6 syntax***

`const phoneNumber = obj.contactNumber ? obj.contactNumber.phone : '';`

***or Conventional Way***\
\
`var phoneNumber;`\
`if(obj.contactNumber){`\
   `phoneNumber = obj.contactNumber.phone;`\
`} else {`\
   `phoneNumber = '';`\
`}`

It's to ensure the contactNumber property exist in obj. That way, the function will just return empty string when trying to target an undefined one.

### **2. hasOwnProperty()**

It's a Javascript method which returns a boolean value. It receives a a String as paramater. As its name implies, hasOwnProperty() checks whether an object has a specified property (reff:[ MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty#using_hasownproperty_to_test_for_an_own_propertys_existence)). In our case, it can be used like this:

`const phoneNumber = obj.hasOwnProperty('contactNumber') ? obj.contactNumber.phone : '';`

By setting the key as the parameter ('contactNumber), it will return false if the specified key not found.

This method has many other useful functions, please check more interesting example in the official documentation.

## 3. in Operator

It's a less common used Javascript method to check object properties. It has the similar function as hasOwnProperty() but with exception, it also returns true for any inherited properties. For example, by console.log the obj, it will show all the inherited properties:

![object base properties](/images/upload/object-base-props.jpg "object base properties")

then  when calling these 2 methods it results in: 

1. `'constructor' in obj; // ``true`
2. `obj.hasOwnProperty('constructor'); // ``false`

See the difference? 

So basically, to check whether an object contains certain keys, it's more common to use hasOwnProperty() than 'in Operator'. 

All above methods are compatible with major browsers, including Internet Explorer. (except the ES6 syntax, you need Babel for transpiling your code! [Explore the magic of Babel here](https://babeljs.io/repl/).)

On the next post, I will share another interesting way to check object property. If you have a different way, please share it to my contact which can be found here: http://helenwijaya.com/. Thank you!