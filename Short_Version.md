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

#Specify conditions
monkey.mass=9.9
monkey.velocity=vec(0,0,0)
dart.mass=0.023
#Calculate a vector called "aim" that points from the current dart position to the monkey 
#norm(aim) is a unit vector in the direction of aim
aim=monkey.pos-dart.pos
dart.velocity=v0*norm(aim)

t=0

tmax=(monkey.pos.x-0)/dart.velocity.x #this calculated time is a hint, but it is not complete
while t<tmax:
  rate(1.0/delta_t) #slow the execution of the loop down so it runs every delta_t seconds
  #update velocity
  Fnet=monkey.mass*g*vec(-1,0,0)
  dart.velocity = dart.velocity
 
  #update position
  dart.pos=dart.pos + dart.velocity * delta_t
  t=t+delta_t
  print(t,dart.pos)
````

Checkpoint the code should compile correctly.

## fix the calculation of tmax

Checkpoint: the dart should reach the monkey

## Update dart.velocity

Checkpoint: the dart should trace a parabola

## Update monkey.velocity

Checkpoint: the monkey should fall
