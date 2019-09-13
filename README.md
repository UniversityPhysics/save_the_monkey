# Save the monkey!

Please read Matter & Interactions chapter 1 section 11 before doing this activity. The first chapter is freely available online. 



# Draw 3D shapes in VPython

We will use the visual package for Python, referred to as ``VPython''. There is a lot of helpful reference material and tutorial videos available at VPython.org. 

You don't need to install anything! Just use GlowScript.com. Southern students can log in with their southern email. 
Draw a cylinder representing a person, a sphere representing a monkey, and a flattened cylinder representing the ground (for reference).

```
# First, see how easy it is to make a 3D scene in VPython!
tree_distance=40.0
person=cylinder(pos=vec(-tree_distance/2,0,0),axis=vec(0,2.0,0),color=color.blue)
monkey=sphere(pos=vec(tree_distance/2,10.0,0.0),radius=1, color=color.red)
ground=cylinder(pos=person.pos,axis=vec(tree_distance,0,0),height=0.1)

```

Run the code to see your scene. Use control-mouse to pan and zoom. 

# Next, learn to draw a vector (use object properties)

```
aim=arrow(axis=monkey.pos-person.axis,pos=person.axis)
dart=sphere(pos=person.axis)

```

# Now, define an initial value of vector r and apply the update equation in a loop


