**February 28, 2017**

This spring, my university's chapter of the ACM is having a competition. Whoever makes the coolest Raspberry Pi project will win $250 and some Microsoft stuff. In the words of Stanley Hudson:

### Game on.

My team consists of my friends David, Colin, Jiahua, Jacob, Christian, and myself. We've split into two groups: software (Jiahua, Jacob, me) and hardware (David, Colin, Christian).

## The Idea

Most of us like to play pool, so we came up with an idea that helps novice pool players. Here we go:

The Pi will serve as a "shot-caller" for both 8- and 9-ball. It will take a still image of the table, read which balls are on which team (or in the case of 9-ball, the ball which needs to be contacted next) and calculate your easiest shot. It will then shine a laser on the edge of a rail to represent where you should aim the cue.

## Making it Happen

The Pi will be mounted above the table on a lightweight, collapsible rack, and will automatically calibrate based on the first image the camera takes. Then, using image processing libraries and a bit of Python, we can generate a virtual grid, allowing us to do the necessary math for the physics of each possible shot.

After the physics part, we'll algorithmically rank each shot based on a few criteria, including:

* distance
	* from cue to object ball
	* from object ball to pocket
* severity of angle from object ball to pocket
* number of kicks
* proximity to 8 ball (but only in 8-ball -- in 9-ball, if you pocket the 9 on any combination, you win)

It's exciting to begin building everytihng, and we only have about two weeks to do it.