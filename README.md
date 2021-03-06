# Groupy
A python script (and aspirational library) that allows you make and perform computations with finite groups. I have tried to craft a back end that is flexible and robust enough for users to construct group elements, groups and be a sandbox that allows users to mess around with these objects with python taking care of the computation.

This has started as a personal passion project, but I would be interested in seeing what other mathematicians would like to get out of this and see how far this project can go.


## Getting Started

### Using pip
The package is hosted on test.pypi. To install the groupy package using pip use

```pip install --index-url https://test.pypi.org/simple/ --no-deps groupy```

using your python interpreted or choice with version >= 3.

You should now be able to use ```import groupy as gp``` and use the Gel, GroupLike and Group classes, along with the supplementary functions I have created.


### Using clone
To get started you currently just need to copy the script onto your local machine via clone. Once cloned, use

``` from groupy import groupy as gp ```

to import the logic for different objects I have created.


## First time user
For first time users I recommend using the ```gp.constructGroup()``` function to start with some basic groups, maybe the Klein four-group by typing ```V4 = gp.constructGroup('Klein Group')```. You can now call the elements of this group by either using ```V4[i]``` for some integer i or using the group elements name as a string (e.g. ```V4['(1 2)']```).


## How does it work
One you've played around with that, it's worth understanding the back end to this code which runs it all. This whole project is founded on Cayley's theorem: every group G is isomorphic to a subgroup of the symmetric group acting on G. Fundamentally, we can think of every finite group as a subset of the symmetric group. A group element, or 'Gel' for short is thus a symbollic element (e.g. 'g') which has some analogue to a cycle from the symmetric group. Thus we input ```g = gp.Gel('g', <tuple>)``` to represent this group element.

Ok, but what is this magical tuple? Well, if you only care about groups, then you may never have to worry about that (or at least in some future state of this library). The representation of this element will just be the string you have chosen to name it by and multiplying it with other elements will cause those strings to concatenate with other group elements to form 'words' from your group.

But I really want to know what this magical tuple is! Ok, great! I love your enthusiasm. I'll start with an example: imagine you want to create the group of rotations of a triangle. That is, the elements of this group represent rotation by 0, 120 and 240 degrees. What tuple does rotation by 120 degrees correspond to? Well, I can do this a couple of ways.

  1) I know the cycle (1 2 3) can represent 120 degree roatation, that (1 2 3)(1 2 3) = (1 3 2) and (1 2 3)(1 2 3)(1 2 3) = e the indentity. I can simply input the tuple (2,3,1) to represent this. Think of this as the image of each index in the tuple. 1 goes to 2, 2 goes to 3 and 3 goes to 1. Likewise, the tuple (2,4,3,1) sends 1 to 2, 2 to 4, 3 to 3 and 4 to 1.
  
  2) If I write down the Cayley table for my group, I can number each element of my group.
  For example, if I order my group \[0, 120, 240\], I'll end up with the Cayley table \[\[0,120,240\],\[120,240,0\],\[240,0,120\]\]. We can think of the i^{th} row as representing what the i^{th} group element does to reshuffle the group under multiplication and hence the tuple we would enter for rotation by 120 degrees would be (2,3,1).
  
This may be somewhat mistifying but the advantages are that it is easy for the user to define what the binary operation of the group is without having to express it with formulae. In fact, to define a group you can simply input the Cayley table for your group using the ```gp.mat_to_group()``` function.

## Authors
Luke Keating Hughes
