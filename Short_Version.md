# Short version

##Starter code
Paste in this code to get started. It's possible that tab characters won't paste correctly.

````
GlowScript 3.1 VPython
v0=30.0
delta_t=0.1

g=9.81

#All inputs to this code go up at the top, not buried deep inside the code
v0=30.0
tree_distance=40.0

#Draw scene
person=cylinder(pos=vec(-tree_distance/2.0,0,0),axis=vec(0,2.0,0),color=color.yellow) #person is 2m tall, head is in +y direction
monkey=sphere(pos=vec(+tree_distance/2,10.0,0),color=color.red)

ground=cylinder(pos=person.pos,axis=vec(tree_distance,0,0),height=0.2) #cylinder is flattened
dart=sphere(pos=person.pos+person.axis,make_trail=True)

monkey.mass=9.9
monkey.velocity=vec(0,0,0)
monkey.weight=monkey.mass*vec(-g,0,0)

dart.mass=0.023
dart.weight=dart.mass*vec(-g,0,0)
#Calculate a vector called "aim" that points from the current dart position to the monkey 
aim=monkey.pos-dart.pos
aimhat=norm(aim)
dart.velocity=v0*norm(aim)

t=0
tmax=(monkey.pos.x-0)/dart.velocity.x #this calculated time is a hint, but it is not complete
while t<tmax:
    rate(1.0/delta_t) #slow the execution of the loop down so it runs every delta_t seconds
  
    #update velocities
    dart.Fnet = dart.mass*vec(0,-g,0) 
    dart.velocity = dart.velocity 

    monkey.velocity = monkey.velocity 
  
    #update positions
    dart.pos=dart.pos + dart.velocity * delta_t
    monkey.pos=monkey.pos
    
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
