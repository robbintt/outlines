
### Laser Cutters and 3D Printers

How to use Python to build stuff to be laser cut or 3d printed.
Talk: https://github.com/vishnubob/pycon2016
Speaker: Giles Hall


###### Additional Resources:
* https://github.com/vishnubob/pyscad
* https://github.com/vishnubob/rockit
* https://github.com/vishnubob/snowflake

#### Laser Cutters

##### Process

1. Select material (wood, plastic, etc.)
2. Size
3. Build design (vector graphics allows scaling without losing fidelity eg svg)
    * Determine which lines are cut
    * Determine which lines are etched
4. Lay out material on laser bed
5. Upload your design and begin to cut.

The individual processes above are defined by the particular laser cutter and its software.

Can use PDF, EPS, etc. But preferred is SVG:

Path is a great way to specify a zigzaggy line in your SVG.


##### So how do we use Python to generate our SVG for our laser cut image?

We'll cut 2D shapes and assemble them into a 3D shape.

His cube is a really great sample of using one huge single cut to make six interlocking pieces.

This cube was cut with wood and you can see the burns on the edges of the wood from the laser.

I could easily modify this to build the cups I want to make for tea.

Really just need to know the guts of the SVG path specification, the N commands and L commands that let you specify a complex set of line segments.

Then we get more complex by etching onto the sides of the teacups. He uses fermat's spiral, but I could do anything or free draw something, or get a raster/pixelart off the web and convert to svg circles.

Maybe skyrim mug


#### 3D Printers

Most common are fuse deposition models.

Cut 3d object into 2d slices and build a model up.

Extruders extrude plastic to do this. Uses XY plane for each layer, Z advances to the next 2D slice.

Generate STL file
Produce GCODE

STL is very hard to generate by hand. Not great way to think about 3d designs (mesh of triangles).

##### There must be a better way to design!!

Most 3D modelling tools are expensive, difficult, or run in windows or all three.

OpenSCAD -> 
* open source, 
* uses constructive solid geomoetry.

Drinking glass can be constructed with two cylinders.
1. Describe outside surface.
2. Describe negative space inside, slightly smaller radius, slightly offset from bottom.

```
# very easy to build a drinking glass, nested cylinders
difference()
{
  cylinder(r=20, h=80);
  translate([0,0,1]])
  {
    cylinder(r=18, h=90);
  }
}

```

###### We can very easily generate OpenSCAD from Python using PythonSCAD!

How about a Flower Pot?

It's a cone but we call that a cylinder in scad with 2 different radiuses on each end.

Lip at the top.

A few different Python Libraries:  PythonSCAD written by the Speaker.

You can accomplish with the other alternative libraries but we use his here.


``` python
"""
PythonSCAD Sample of a flowerpot.
"""
class FlowerPot(SCAD_Object):
    radius_ratio = 0.6 # from flowerpots in his house
    collar_height_raidus = 0.2
    height = inch2mm(2.5)
    thickness
    # ...
    # theres more but he moved on


def scad(self):
    outer_pot = Cylinder(r1=self.bottom_radius, r2=self.top_radius)
    # ...
    # theres more but he moved on


# this is all the code!
```    

###### Other things to check out in PythonSCAD

Translate math from "Modeling a Snow Flake...." research document into Python.

They used this to make snowflakes 3D printed.

The math used a complex automata and was computationally expensive - done in the cloud.
The program provides a raster of the automata cells and then is converted to SVG.
Two SVGs are merged, one of the densest bands of automata another of the outline.
Then sent to the 3D printer (laser cutter?).
