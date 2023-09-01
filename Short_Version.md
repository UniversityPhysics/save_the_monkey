Web VPython 3.2
# Inputs
v0=30.0         # dart velocity
delta_t=0.1    # time step in calculation
g=9.81          # acceleration of gravity
tree_distance=50.0
tree_height=20.0

# Draw scene
scene=canvas(width=900, height=800)
person=cylinder(pos=vec(-tree_distance/2.0,0,0),axis=vec(0,2.0,0),color=color.yellow) 
# the ground is a long flat cylinder. It could have been a thin box.
ground=cylinder(pos=person.pos,axis=vec(tree_distance,0,0),height=0.2)

# Create a monkey and a dart
skip_points = 3    # don't leave a trail at every time step
monkey=sphere(pos=vec(+tree_distance/2,tree_height,0),color=color.red,make_trail=True,
trail_type="points", interval = skip_points)

# The dart is a sphere. Turn on make_trail.
dart=sphere(pos=person.pos+person.axis,make_trail=True,trail_type="points",interval = skip_points)
monkey.velocity=vec(0,0,0)
monkey.acceleration=vec(0,-g,0)

# Calculate a vector called "aim" that points from the current dart position to the monkey 
aim=monkey.pos-dart.pos
aimhat=norm(aim)
dart.velocity=v0*norm(aim)
dart.acceleration=vec(0,-g,0)

# Calculate the time ”tmax” when the dart reaches the monkey
tmax=(monkey.pos.x-person.pos.x)/dart.velocity.x #this calculated time is a hint, but it is not complete
print(tmax)

# Physics engine
scene.waitfor('click')           ## wait for a mouse click
t=0
while t<tmax:
    rate(1.0/delta_t) #slow the execution of the loop down so it runs every delta_t seconds
    #update velocities 
    dart.velocity = dart.velocity + dart.acceleration*delta_t
    monkey.velocity = monkey.velocity + monkey.acceleration*delta_t
  
    #update positions
    dart.pos=dart.pos + dart.velocity * delta_t
    monkey.pos=monkey.pos + monkey.velocity * delta_t
    
    t=t+delta_t
    
    
print("distance=",mag(monkey.pos-dart.pos)," m")
````

Checkpoint the code should compile correctly.


## Update dart.velocity

Use the net force on the dart to update the dart velocity.

Checkpoint: the dart should start to trace a parabola

## Update monkey.pos and monkey.velocity

Inspect the code. If you were to update the monkey velocity using the net force on the monkey, would the monkey position update? Make both the position and velocity update. 

Checkpoint: the monkey should fall too

## fix the calculation of tmax
The code has a hint on how to use python to calculate the time it takes for the dart to reach the monkey. Finish the calculation in 
````
tmax=(monkey.pos.x-0)/dart.velocity.x
````

Checkpoint: the dart should reach the monkey

## Choose smaller step sizes until the final distance converges
We are performing a numerical summation to approximate an integral. In the limit that the time step size goes to zero, the answer should converge to a well-defined limit. The distance between the monkey and the dart at tmax is displayed. Decrease the time step in units of 0.01s to find the largest time stp for which the final distance is less than 10 cm. 
