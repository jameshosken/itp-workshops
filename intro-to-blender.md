# Blender Workshop

## What is Blender?
[Blender](blender.org) is an open source 3d creation tool.

## Housekeeping & User Prefs
* Version 2.79B or C
* If you have __no numpad__, _File > User Prefs > Input > Emulate Numpad_
* If you have __no 3 button mouse__, _File > User Prefs > Input > Emulate 3 button mouse_
* __Save user preferences__
* Windows CUDA? Enable in User Preferences > System.
* Change render engine to cycles: Info Panel (top) > change __Blend er Render__ to __Cycles__
* I use windows, so when I say 'Alt' I mean 'Option' on the mac, and when I say 'Control' it will usually mean 'Command'

## Interface
* Single Window
* Fully Customisable
* 'Editor Panel' based

### Panel Adjustment
* Click and drag the edges of a panel to adjust its size
* Use the triangle icons on the top right and left of each panel to create/collapse panels
* Use the 'Editor Type' buttons (top or bottom right of each panel) to change the content of the panel. Our most useful panel types at this stage are:
  * 3D view
  * Properties
  * Outliner

[_Challenge: Collapse the Timeline_]

## Navigating 3D space
* Check user prefs
* MMB to orbit (Emulation: Alt + LMB)
* Shift + MMB to pan (Emulation: Alt + Shift + LMB)
* Scroll to move in/out (Emulation: Alt + Ctrl + LMB)
* Shift + 'F' to enter __Camera Mode__
* Ctrl + '.' to View Selected
* Shift + 'C' to View All
* X,Y,Z Axis & bottom left-hand widget

### Aligning views
Aligning views can be helpful to get different perspectives of your model. By default numpad is used, but if you have no numpad (and have changed your user prefs), you can use numeric keys.

* 1, 3, 7 for Front, Left, Top
* Shift 1, 3, 7 for Back, Right, Bottom
* 5 for __orthographic__ camera.
  * Orthographic means parallel lines irl actually appear parallel on camera.
  * This is not a concept that is easy to just 'get', so if this is foreign to you DON'T PANIC. Just remember that if the perspective of your model looks ~weird~ perhaps it's because you're in orthographic mode.

That's the end of the "Troubleshooting Guide" - if your camera or interface looks weird you now know how to investigate what is wrong...

## Objects

### The 3D Cursor
Perhaps _the_ least intuitive aspect of Blender for beginners is the Right Mouse Button selection. If feels weird. It is weird. But, once you get used to it it makes a lot of sense. I have found myself, especially after a Blender power session, right clicking to select in other programs to...

Left mouse button will move the 3D cursor. The 3D cursor has many applications and one of them is to determine where new objects are placed. To reset the 3D cursor hit __Shift + 'S'__ and select Cursor to Center.

### Creating objects
* Add > Mesh > [type], __OR__ Shift + 'A' > Mesh > Type

[_Challenge: Create a few objects in different locations around your scene_]

### Manipulating Objects
The fundamentals of 3D space: __Position, Scale, Rotation__

#### The Three Transformations: Position, Scale, Rotation of objects:
* Pivot Point 
* 'G' (Grab) to __move__
  * You may also click each axis arrow to move along that axis
* 'R' (Rotate) to __Rotate__
* 'S' (Scale) to __Scale__

Pressing the desired key will enable enable a 'preview' of the intended change. 
* To APPLY the change, hit __Enter__ or __Left Mouse Button__
* To CANCEL the change, hit __Right Mouse Button__


#### Axis Locking
Unconstrained, these changes can be a real pain. There are tools to help us narrow down the manipulation of an object:
* Press 'X', 'Y', or 'Z' to lock the change to that axis (e.g make a tower)
* Press Shift + 'X', 'Y', or 'Z' to exclude that axis from the change (e.g. make a floor)

#### Precision
Instead of moving the mouse around, you can type number values after hitting manipulation keys.

#### Global vs Local
Objects remember their original rotation. You can use this to your benefit when moving objects around in space, at angles different to the world axis
* Transform Panel

[_Challenge: Make a face_]

### Editing Shape
Up until now we've been in what's called 'Object Mode'. This tells Blender we're dealing with objects as a whole. When you move, rotate, or scale an object you do it to the whole object.

But we can do more than that, we can change the actual geometry of an object. We can put a hole in something, or turn a cube into a sphere, stretch out certain parts, add detail, the list is literally endless. To do that we must be in __Edit Mode__

#### Edit Mode
* Adjust actual geometry of object
* Grab, Rotate, Scale: Vertices, Edges, Faces (Ctrl + Tab to switch selection modes)

#### Edit Mode Tools
So many more tools than we can cover here, I will show two:
* Extrude
* Inset

## Lighting and Rendering

### Add some lights
* Same way as you add meshes.

### Add some colour
* Introduce the properties panel
	* Some of these data sets don't change, some of them change depending on the object selected.
* Change the background colour of the world
	* Use the "World" data set
* Change the material colour of your object
	* Use the "Materials" data set
* Shift + Z to render your image in viewport


