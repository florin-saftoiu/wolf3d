Hacking the WOLF3D source code
==========================================
This is me trying to understand and mess around with the Wolfenstein 3D source code.

Requirements
------------
* Install DOSBox
* Install Borland C++ 3.0 in DOSBox, under ```C:\BORLANDC```
* Clone this repo and mount its root as ```C:``` in DOSBox
* Copy the original Wolfenstein 3D data files in ```C:\WOLF3D\WOLFSRC```
* Set ```PATH``` environment variable to include ```C:\BORLANDC\BIN```

Stuff I've done to ```WOLFSRC\WOLF3D.PRJ```
-------------------------------------------
* Set output directory to project directory, because the BC++ 3 IDE cannot force a working directory other than the project directory when running the executable
* Set output directory for ```C0.ASM``` as project directory
* Remove ```SIGNON.OBJ``` and ```GAMEPAL.OBJ``` dependencies and add them back from the ```OBJ``` folder
* Set ```INCLUDE``` directory to ```C:\BORLANDC\INCLUDE``` and ```LIB``` directory to ```C:\BORLANDC\LIB```
* Set **Options -> Debugger -> Display Swapping** to **Always**, otherwise it messes the game output when debugging
* Set **Options -> Debugger -> Heap size** to **320K**, otherwise the game complains about not having enough memory
