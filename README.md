# Save the monkey!

It must be seen to be believed. If a veteranarian aims a dart gun upwards at a monkey hanging in a tree and the monkey drops the instant the dart gun is fired, the dart will always hit the monkey.

## Our development environment
We will use the visual package for Python, referred to as VPython. There is a lot of helpful reference material and tutorial videos available at http://VPython.org. 

You don't need to install anything! Just use http://GlowScript.com. Southern students can log in with their southern email. To submit your assignment this time, you will simply paste in a URL to your glowscript code. Make sure you see PUBLIC and not PRIVATE, to be sure that it is not hidden from me in a private folder. Eventually, you will learn to submit your codes through Github, a valuable professional skill.

## Position update form of average velocity equation
Please read Matter & Interactions chapter 1 section 11 before doing this activity. The first chapter is [freely available online here](https://matterandinteractions.org/wp-content/uploads/2016/07/Chapter1-InteractionsandMotion.pdf). Read their excellent explanation of how the definition of average velocity can be written in "update form". Instead of defining a new position vector at each update, a computer program can simply store the updated postion `r+v*delta_t` in the old position using the assignment statement `r=r+v*delta_t`. As the authors explain, this is not a mathematical statement! This is an instruction to calculate `r+v*delta_t` and store the result in the memory address for `r`. This statement works just as well if `r` and `v` are vector objects.

Apply what you have learned to update the position of a sphere representing a dart, such as in the code sample below.

```

v0=30.0

dart = sphere()
vhat=vec(1,0,0)

delta_t=0.1
t=0
velocity=v0*vhat
while t<3:
  rate(1.0/delta_t) #slow the execution of the loop down so it runs every delta_t seconds
  dart.pos=dart.pos + velocity * delta_t
  t=t+delta_t
  print(t,dart.pos)
```

See if this code will run without errors.


## Draw 3D shapes in VPython

Draw a cylinder representing a person, a sphere representing a monkey, and a flattened cylinder representing the ground (for reference). The top part of your code should now look something like this. 

```
#All inputs to this code go up at the top, not buried deep inside the code
v0=30.0
tree_distance=40.0

#Draw scene
person=cylinder(pos=vec(-tree_distance/2.0,0,0),axis=vec(0,2.0,0),color=color.blue) #person is 2m tall, head is in +y direction
monkey=sphere(pos=vec(+tree_distance/2,10.0,0),color=color.red)
ground=cylinder(pos=person.pos,axis=vec(tree_distance,0,0),height=0.2) #cylinder is flattened
dart=sphere(pos=monkey.pos*2+person.pos)
```

`person` is a cylinder "object", and it has "object properties" which are vectors that can be accessed as `person.pos` and `person.axis`. Similarly, `monkey` is a sphere object with property `monkey.pos`. Since these properties are vectors, we can directly calculate new vectors using vector math, such as `dart=sphere(pos=monkey.pos*2+person.pos)`. Correct the position of the dart sphere object using vector math.

Run the code to see your scene and verify that the dart position is at the top of the person. Use control-mouse to pan and zoom. 

## Next, learn to draw a vector (use object properties)
Draw a vector arrow from the dart position to the monkey. The "tail" of the arrow should be at position `dart.pos`. The axis property is the actual vector, which should point from the dart position to the monkey position. Add this arrow object below to your code, and correct the axis property using vector math.
```
aim=arrow(pos=dart.pos, axis=monkey.pos-dart.pos, shaftwidth=0.5)
```
Run the code to see if the `aim` arrow points from the dart toward the monkey. Can you see why the vector needs to point in the direction `monkey.pos-dart.pos`, rather than just `monkey.pos`?

This arrow is useful because it tells us which direction the initial velocity of the dart should be aimed. Lets calculate a unit vector `vhat` from the vector `aim.axis`. It's common to denote unit vectors with a "hat", such as $$\hat{v}$$, which people pronounce "v-hat". Using the unit vector `vhat`, correct the velocity before the loop:
```
vhat=aim.axis/mag(aim.axis)
velocity=v0 * vhat
```

An equivalent way to calculate a unit vector is to use `vhat=norm(aim.axis)`. This way doesn't complain if the vector happens to be zero.

Run your code and verify that the dart velocity is in the correct direction. Modify time t_max so that the loop stops when the dart is approximately at the monkey position. Alternatively, you could do something like `while dart.pos.x < monkey.pos.x :`.

## What about gravity?

Just as the average velocity relationship can be written in position update form `r = r + velocity * delta_t`, the average acceleration can be written in velocity update form `velocity = velocity + acceleration * delta_t`, where acceleration is a vector. How does the acceleration vector of the dart compare to the monkey?

Before your time loop, define the acceleration `acceleration = vec(0,-9.8,0)` and *after* the position update statement, add a statement that updates velocity.

Run the code to see if the dart follows the expected parabola.

## But isn't the monkey position and velocity changing too?

Yes, we also have the monkey position and velocity to update, in addition to the dart position. Let's first clean up our notation by taking advantage of the ability to assign a new property to an object. Modify your code to define a new velocity property of dart, like this.
`dart.velocity = v0 * vhat`
Remove all references to a lonely `velocity` and verify that your code still runs. 

Now create a `velocity` property of the monkey object.
```
monkey.velocity = vec(0,0,0)
```

Add similar lines of code to update `monkey.pos` and `monkey.velocity` in your code. Run your code to verify that it behaves as expected.

Congratulations! You saved the monkey!

## Extension: what about air resistance?

The force of air resistance can be written as F=1/2*CdA*v^2 and it's always in the opposite direction of `vhat`. So to take air resistance into account, you could simply update `vhat` and update acceleration as `F_air/m+vec(0,-9.8,0)`. Computational skills make such "impossible" tasks quite simple!

## Extension: what about relativistic speeds?

Simple. Just read to the end of Chapter 1 and update gamma.


