---
layout: post
title: Javascript Learnings - Wes Bos 30 Days of Javascript
date: 2018-7-10
tags: ["javascript"]
---

Here's my top 3 learnings from the first few days of Javascript 30, a video course created by Wes Bos. If you're looking to level up your front end skills, this is a great place to go! He discusses newer features such as flex, array and object destructuring, ES6 syntax, canvas and more. <!--break--> These tutorials are recorded live coding videos - he makes some mistakes and voices how he reasons about fixing them, and it's super helpful to see an experienced developer code.

If you haven't checked this course out, you can find it [here](https://javascript30.com/)

# 1. Display more readable output with Console.table() + friends

Many people have used console.log() at some point. However, the console family has had some recent additions that you might not know about. This is not an exhaustive list, just my favourites!

## console.table()

This is something I didn't know existed! It's a great way to view your JSON objects in particular, and even works for arrays, and arrays of arrays! Using it for more than this can get a little hairy though.

```javascript
const dogs = [{ name: 'Snickers', age: 2 }, { name: 'hugo', age: 8 }];

console.table(dogs)
```

![screenshot of console.table](/assets/console_table.png){: .img-responsive}

## console.group()

This one allows you to have nicely grouped logging statements, and you can have as many nested statements as you please.

All you need to do is explicitly state when the grouping should finish. If you're not a fan of expanding everything all in one go, you can set everything to be collapsed instead with `groupCollapsed`.

```javascript
dogs.forEach(dog => {
      console.group(`${dog.name}`); // you can also use groupCollapsed
      console.log(`This is ${dog.name}`);
      console.log(`${dog.name} is ${dog.age} years old`);
      console.log(`${dog.name} is ${dog.age * 7} dog years old`);
      console.groupEnd(`${dog.name}`);
});
```

![screenshot of console.group](/assets/console_group.png){:class="img-responsive"}

## console.assert()

If the given boolean condition is true, nothing is printed. But if it's false, it'll print out a good reason if you give it one! (*whoops* is not a great example of an error message).

```javascript
console.assert(5 % 2 === 0, 'whoops');
```

![screenshot of console.assert](/assets/console_assert.png){: .img-responsive}

More information about the fam [here](https://developer.mozilla.org/en-US/docs/Web/API/Console/table).

# 2. Easily access DOM node data with the "data-" prefix

*data-* attributes are available in HTML5, and are a useful way to store data on HTML elements without having to store extra properties on the DOM (or setting user data on the DOM).

So long as your attribute name has a *data-* prefix, it will be accessible under the the element's *dataset* value. 

The `<kbd>` element is used to identify text that represents user keyboard input, and is used in the following example.

In this example, we define a keycode to look for. When the user types that key on the keyboard (A), and we have a matching key on our audio tag (65) it will play a sound. 

##### HTML
```html
<div data-key="65" class="key">
    <kbd>A</kbd> <!-- user-defined html tag-->
    <span class="sound">clap</span>
</div>

<audio data-key="65" src="sounds/clap.wav"></audio>
```

##### JAVASCRIPT
```javascript
function playSound(e) {
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
    if (!audio) {
      return;
    }
    audio.currentTime = 0;
    audio.play();
    key.classList.add('playing');
  }
```

More information about using data attributes in your divs can be found [here](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes).

# 3. Flex your functional muscles! Reduce with object aggregates!

If you've used some functional javascript before, such as the map or filter functions, you might also have come across reduce. It's nice way of converting many values to one value, such as summing up multiple values or getting the average.

Reduce functions need a few things:
1. A list of items
1. A reducer function
1. An aggregate starting value* 

*unless you have a list of Numbers, in which case it defaults to 0

```javascript
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];

const vehicleFrequency = data.reduce( (frequencyMap, vehicle) => {
    if (frequencyMap[vehicle]) {
        frequencyMap[vehicle]++;
    } else {
        frequencyMap[vehicle] = 1;
    }
    return frequencyMap;
}, {});
// lets use our new console.table for this!
console.table(vehicleFrequency);
```
![screenshot of reduce table](/assets/reduce_table.png){: .img-responsive}

That's about it from me! If you found any of these suprising, definitely check out the [Wes Bos course](https://javascript30.com/)!
