## My Work
I have a few different types of projects, both personal and through work. I'll walk you through some of them.

### [cli-weather](https://github.com/apizzimenti/cli-weather) (personal - software/web)
This is by far my most personal project. Before winter break 2015-2016, I was feeling a little burned out after a lot of
schoolwork and poor time management. So I decided to take on a medium-scale node module project.

I was really starting to get into JavaScript and learning quite a bit about the nitty-gritty of the language. Then, I
discovered `Node.js` and immediately fell in love. I could write command line tools in my favorite language? Never thought
it'd be possible.

I immediately started thinking of things to do in the command line that'd make people's lives easier. I thought for days,
thinking about cli text editors, automatic README generators, things like that. I took a bunch of walks, and I realized
that I check the weather wayyyyy more often than I needed to and it took a long time to navigate to wunderground every
single time. [cli-weather](https://github.com/apizzimenti/cli-weather) is a super easy-to-use cli weather interface that
automatically grabs your location and gets the current conditions and a 4-day forecast.

I used an OOP model for the modules in the project so that each had easily accessible and mutable properties rather than 
a bunch of function collections and callback hell. The OOP model makes JavaScript that much easier to write and organize.

**Status**: _production version(s) completed_
**Due for Completion**: _none_

### Planet Z (work - web)
This project was fun for me because I got to write a video game. Not the engine, of course, because Phaser took care of
that. I used the isometric plugin to make a 2.5-d gameplay window. The physics and model interactions were really tough
because of how the isometric plugin interacts with the existing physics system (I'll find a video of the glitches later).
Because I got this job earlier in my JavaScript career, I didn't write it in an OOP format (although I'm working on it).
The rest of the interactions are all in Angular, and so it's a really slick SPA.

**Status**: _in progress_
**Due for Completion**: _April 2016_

### Sounds of Speech (work - mobile)
I got to work with Jerry Moon, a speech pathologist and ref in my hockey league. This was a fun app to help with on
the tail end, especially with being able to navigate the JavaScript object hierarchy. I discovered that, incidentally,
if there is no `order` property on an object, Chrome renders the properties in alphabetical order. And, because of this,
I had to figure out a way to effectively get through the properties of an object and their subproperties but retain order.
Turns out that sets are cool, so I changed some things over to arrays and modified this code (written by another developer
who shall remain nameless):

```
for (var headingGroup in myData.menu) {
        for (var interactions in myData.menu[headingGroup]) {
            for (var i = 0; i < myData.menu[headingGroup][interactions].sections.length; i++) {
                for (var section in myData.menu[headingGroup][interactions].sections[i].items) {
                    myData.menu[headingGroup][interactions].sections[i].items.forEach(function (item) {
                        all.push(item);
                    });
                }
            }
        }
    }
```

I'm horrified that I had to write it, but sometimes hardcoding is the best answer. I worked out a recursive method to map
the objects correctly, but it was too dependent on small properties of the data:

```
function setValues(object, stack) {
    for (var property in object) {
        if (typeof(object[property] === 'object' && Object.keys(object[property])[0] !== 0)) {
            // assign value to map, self-call
            setValues(object[property], stack + '.' + property.toString());
        } else {
        	// prints property tree
        	console.log(stack);
        }
    }
}
```

The app is now working in its entirety, and is available on both the App Store and the Google Play Store. Bravo.

**Status**: _complete_

### Bongo-Signage (work - web)
This is a site that pulls data from the eBongo Bus Service api for the two major bus stops outside the UCC and displays
them. This page also has a moving Phaser Isometric city, replete with animations and weather replication (falling snow!).
Now, the challenge with this project is that I have to engineer it to run on an old Intel Compute Stick. Very little CPU
and memory capacity is on that little thing, so I'm going to try and use WebWorkers to lighten the load.

**Status**: _near completion, branching_
**Due for Completion**: _February 2016_

### NHL Playoff Predictor (personal - data/software)
Last year I wrote a rudimentary NHL Playoff Predictor to try and determine the winner of the NHL Stanley Cup Playoffs. It
predicted the first-round matchups with a ~50% accuracy rate, but I didn't really take an algorithmic approach to it. I'll be
doing it in Python this time around because it's better for data manipulation and I want to learn it.

**Status**: _planning_
**Due for Completion**: _by the first game of the playoffs_