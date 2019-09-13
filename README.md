# Save the monkey!

## Our development environment
We will use the visual package for Python, referred to as VPython. There is a lot of helpful reference material and tutorial videos available at http://VPython.org. 

You don't need to install anything! Just use http://GlowScript.com. Southern students can log in with their southern email. 

## Position update
Please read Matter & Interactions chapter 1 section 11 before doing this activity. The first chapter is [freely available online here](https://matterandinteractions.org/wp-content/uploads/2016/07/Chapter1-InteractionsandMotion.pdf). 

$$\vec{v}=\frac{\vec{r}_2-\vec{r}_1}{\Delta t}, \vec{a}=\frac{\vec{v}_2-\vec{v}_1}{\Delta t}$$
This equation can be solved for the next position $\vec{r}_2$ in terms of the previous position and velocity:
$$\vec{r}_2=\vec{r}_1+\vec{v}\Delta t$$

In computer language





# Draw 3D shapes in VPython

Draw a cylinder representing a person, a sphere representing a monkey, and a flattened cylinder representing the ground (for reference).

```
# First, see how easy it is to make a 3D scene in VPython!
tree_distance=40.0
person=cylinder(pos=vec(-tree_distance/2,0,0),axis=vec(0,2.0,0),color=color.blue)
monkey=sphere(pos=vec(tree_distance/2,10.0,0.0),radius=1, color=color.red)
dart=sphere(pos=person.axis)
ground=cylinder(pos=person.pos,axis=vec(tree_distance,0,0),height=0.1)
```

Run the code to see your scene. Use control-mouse to pan and zoom. 

# Next, learn to draw a vector (use object properties)
Draw a vector arrow from the top of the person to the monkey. The top of the person is at the tip of a vector from the origin to `person.pos+person.axis`, so that's what we should set the `aim.pos` property equal to:
```
aim=arrow(pos=person.pos+person.axis, shaftwidth=0.5)
aim.axis=monkey.pos
```
The property `aim.axis` is the magnitude and direction of the vector. Calculate this vector from properties of monkey and person, replacing the line `aim.axis=`

The "tail" of the arrow is the vector property `arrow.pos`. 
The part of the arrow that represents a vector (magnitude and direction, not the position of the tail) is 
`arrow.axis`.
Make an `arrow()` object with a property `arrow.axis` 

```
aim=arrow(axis=monkey.pos-(person.position+person.axis),pos=person.axis)
```

# Now, define an initial value of vector r and apply the update equation in a loop


