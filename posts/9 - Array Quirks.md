**September 9, 2016**

### In-Place
Recently I've been working on a side project that is somewhat of an extension to lodash
and the `Array` prototype (but I wouldn't dare extend it myself). Many of my daily 
tasks require manipulating or managing data, especially with my
[isometric-features](https://github.com/apizzimenti/isometric-features) project. There
are a _ton_ of `Array` objects in this massive system, and with that comes some
frustrations.

By default, JavaScript has no method of removing a specific index from an array - this
makes sense, as an array is meant to serve as a _collection_, not a list. In fact,
JavaScript hovers half-and-half between a true array and a list, somewhat like Python.
The `Array` prototype has methods for reducing, filtering, mapping, etc. borrowed from
the functional programming paradigm; they are essentially wrapper functions that operate
on an input array and return a value; whether that returned value is an array, a number,
or something else, the original array remains intact - akin to Java or C.

However, there are some methods that operate on the array in-place, making it less
of a collection and more of a list; these include `sort()`, `pop()`, `unshift()`, and
the like. These make it somewhat troublesome to deal with Arrays, as their lengths
aren't fixed, and are actually _mutable_. That's right, folks, `Array.length` is *not*
an immutable property. So, `Array`s, again, are half-and-half.

Operating on an array's length in JavaScript will get you this:

```
var ar = [1, 2, 3, 4, 5];
ar.length = 3; // [1, 2, 3];

ar.length = 7; // [1, 2, 3, , , ,];
ar[10] = 2; // [1, 2, 3, , , , , , , 2];
```

This lets everyone know that Arrays are a collection object, but are backed by a
linked list; being able to remove a specific index (which is possible, as you'll see)
is simply deleting properties of the `Array` object, each of which is an object with
`value` and `reference` properties. If this were not the case, Arrays would behave
like in Java, where each Array has a specific set of allocated memory in which to
store its pointers.

From the ECMA-262 spec: 
 > The value of the length property is numerically greater than the name of every 
 property whose name is an array index; whenever a property of an Array object is 
 created or changed, other properties are adjusted as necessary to maintain this 
 invariant.
 
Take a look at my [method for removing indices](https://github.com/apizzimenti/funk/blob/master/lib/functions/removeIndex.js).
It utilizes the reserved `delete` word, which operates only on Object properties.

Messing with this is somewhat fun, as you can see by the code example above; the values
are just spaced by seemingly empty property assignments. However, modifying the `length` property
does **not** add properties, it can only delete them. Also from the ECMA-262 spec:

> Specifically, whenever a property is added whose name is an array index, the length
property is changed, if necessary, to be one more than the numeric value of that array
index; and whenever the length property is changed, every property whose name is an 
array index whose value is not smaller than the new length is automatically deleted.

The length, when changed to a value greater than the array's current length, does
not tack on values or even add allocated memory, but simply changes an integral property.
However, when changed to a value _less_ than the current length, the indices at values greater than the new length are
deleted in order to maintain the integrity of the `length` property and its ability
to accurately reflect the number of contained hierarchical values.

In summary: `Array`s have easily mutable properties which can either make your life
extremely easy or extremely hellish. The fact that the `Array.length` property is mutable
is one of JavaScript's biggest quirks. You can move things around in Arrays just like
you would any other `Object`, just be aware that JavaScript interpreters treat Objects
of class `Array` differently than they do regular objects.

Next time, we'll take a look at `undefined`, `null`, `NaN`, `infinity`, and other
fun JavaScript things. Cheers!
