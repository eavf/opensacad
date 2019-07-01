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


http://www.thingiverse.com/thing:648813
OpenSCAD library - Springs, helicoils, elliptic rings by Parkinbot is licensed under the Creative Commons - Attribution - Non-Commercial license.
http://creativecommons.org/licenses/by-nc/3.0/

# Summary

LATE BREAKING: in my newer post [springs and springmaker - OpenSCAD library](https://www.thingiverse.com/thing:3252637) I present a library with fast executing code that directly constructs coils and springs via polyhedron.

OpenSCAD has some extraordinary *xxx_extrude()* functionality, which will do a lot astonishing things with just some fingertips. The bad news is: to do quite a lot of things - especially coils - properly, a more sophisticated approach might be required. *linear_extrude()* will projectively deform your cross sectional shape when coiling helices by use of the *twist* parameter. You will either have to compensate for that (which is not any more possible in more coiled designs) or take the stony way presented in my lib.   

Whenever your task is to extrude a shape along a non-circular trajectory like an ellipse, a spring, an elliptical spring, a heart or any other curve in 3D space, the *hull()* operator is your friend.   
The drawback is: It renders slowly and F6 easily may take hours, as I found out producing my sampler for this thing.   

To give you an idea how the mathematics behind it is knitted, as well as some ready-to-use coiled stuff I packed a little library containing four parametrized modules  

*elliptic_ring(r1 = 10, r2 = 5, r = 2, slices = 100, h = 0, w = 360)*  
*helicoil(Windings = 5, R = 20, r = 1, slices = 50, clockwise = true, square = true)*  
*spring(Windings = 5, R = 20, r=2, h = 20, slices = 50)*  
*elliptic_spring(Windings = 5, R1 = 20, R2 = 0, r=1, h = 20, slices = 50)*  

The code does look neat at the first glace but also somehow strange, since it heavily uses my *ShortCuts.scad* library, which I have presented in one of my previous projects: http://www.thingiverse.com/thing:644830 Sorry for that, but it speeds up my programming so much that I don't want to do without any more. Give it a chance and you'll also fall in love with it.   

To sum it up, your chart will contain two libs, one referencing the other. Usage examples are shown in the screenshots.  


# Instructions

To make the lib available for your code copy *Springs.scad* and *ShortCut.scad* into your OpenSCAD libaries folder or current project folder and reference them it by  

*include <Springs.scad>*  

*ShortCut.scad* may also used as standalone lib. reference it with   

*include <ShortCuts.scad>*  

Also note that I put *help()* functionality into each of my libs. For further instructions concerning *ShortCut.scad* please refere to http://www.thingiverse.com/thing:644830