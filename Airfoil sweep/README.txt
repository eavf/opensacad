                   .:                     :,                                          
,:::::::: ::`      :::                   :::                                          
,:::::::: ::`      :::                   :::                                          
.,,:::,,, ::`.:,   ... .. .:,     .:. ..`... ..`   ..   .:,    .. ::  .::,     .:,`   
   ,::    :::::::  ::, :::::::  `:::::::.,:: :::  ::: .::::::  ::::: ::::::  .::::::  
   ,::    :::::::: ::, :::::::: ::::::::.,:: :::  ::: :::,:::, ::::: ::::::, :::::::: 
   ,::    :::  ::: ::, :::  :::`::.  :::.,::  ::,`::`:::   ::: :::  `::,`   :::   ::: 
   ,::    ::.  ::: ::, ::`  :::.::    ::.,::  :::::: ::::::::: ::`   :::::: ::::::::: 
   ,::    ::.  ::: ::, ::`  :::.::    ::.,::  .::::: ::::::::: ::`    ::::::::::::::: 
   ,::    ::.  ::: ::, ::`  ::: ::: `:::.,::   ::::  :::`  ,,, ::`  .::  :::.::.  ,,, 
   ,::    ::.  ::: ::, ::`  ::: ::::::::.,::   ::::   :::::::` ::`   ::::::: :::::::. 
   ,::    ::.  ::: ::, ::`  :::  :::::::`,::    ::.    :::::`  ::`   ::::::   :::::.  
                                ::,  ,::                               ``             
                                ::::::::                                              
                                 ::::::                                               
                                  `,,`


https://www.thingiverse.com/thing:900137
NACA airfoil sweep - OpenSCAD library by Parkinbot is licensed under the Creative Commons - Attribution - Non-Commercial license.
http://creativecommons.org/licenses/by-nc/3.0/

# Summary

*June, 30 - updated Naca_sweep.scad and Naca4.scad*  

The STL designs shown along with this thing are not really meant for printing, rather to visually demonstrate the power of a special programming technique based on new features of OpenSCAD 2015 that will allow you to do really wicked stuff. Also I verify a promise given in a previous post  [NACA Airfoils - 4 digit fully parametric OpenSCAD library](http://www.thingiverse.com/thing:898554), where I introduced some very flexible airfoil calculation functionality.   

To give you an overview where this programming technique applies: As long as a wing, fin, blade or fuselage design does not exceed the (scalable) range of a single NACA airfoil type almost all requirements will be accomplished by juggling around with the mighty OpenSCAD operators *linear_extrude()* and *rotate_extrude()*.  

Whenever a specific (e.g. non-linear) trajectory and/or a transition between different airfoil types, say between a NACA1480 and a NACA1510 is demanded, one is stumped with this tools. In cases, where convexity is granted for all shapes, the *hull()* operator maybe helpful. I have demonstrated this technique in my [Springs, helicoils, elliptic rings](http://www.thingiverse.com/thing:648813) post. Concave stuff by contrast is always more resistive.   

With this post I show the implementation of a sweep operator that connects a set of 2D "slices" placed on a trajectory in 3D space into a single polyhedron. Each slice must be derived from a non-self-intersecting polygon describing a 2D shape, like an airfoil (or any other shape) and have the same number of points as all others. Transformed into a 3D point set, Euclidean transformations are applied to correctly place it on the trajectory in 3D space *sweep()* builds an object of.  

My two examples present two techniques to generate trajectory hull objects with transitions:   
1. Slice objects built of two (or more) 2D shapes and composed by union(). This approach is easier, but CGAL (F6) rendering can take a lot of time.  
2. Polyhedron objects built from a vector of 2D shapes. This approach needs a function to generate the vector set and has the advantage of CGAL rendering being very fast.  

The code for central *module sweep(dat, convexity){ }* is just a few lines. You call it with a fully prepared vector of 3D points set vectors.  

To be be able to freely place a 2D shape within 3D space, I added a bunch of functions operating over points sets and providing translation, rotation and scaling functionality.  

Use functions  
- v3D  to expand a 2D point set vector [[X1, Y1], ... , [Xn, Yn]] into the 3D point set vector [[X1, Y1, 0], ... , [Xn, Yn, 0]]  
- T_(x=0, y=0, z=0, v) to translate a point set vector v in all three dimensions.  
- R_(x=0, y=0, z=0, v) to rotate a point set vector v in all three dimensions.  
- S_(x=1, y=1, z=1, v) to scale a point set vector v in all three dimensions.  
- Tx_(x=0, v), Ty_(y=0, v), Tz_(z=0, v) as shortcuts to translate a point set vector v in one dimension.  
- Rx_(x=0, v), Ry_(y=0, v), Rz_(z=0, v) as shortcuts to rotate a point set vector v in one dimension.  
- Sx_(x=1, v), Sy_(y=1, v), Sz_(z=1, v) as shortcuts to scale a point set vector v in one dimension.  

A last hint: Use F12 to check whether triangle orientation in the polyhedron is correct and has no self-intersections. If you see any purple triangles after F5, there is a problem and the result will be rejected by CGAL or at least cause trouble when applying any Boolean operations. 
If everything is purple, you can either
- reverse your tracjectory by changing the sign of the path variable. 
- or reverse the vertex order in all your polygons

Have fun!