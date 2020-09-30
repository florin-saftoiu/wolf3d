Hacking the WOLF3D source code
==========================================
This is me trying to understand and mess around with the Wolfenstein 3D source code.

Requirements
------------
* Install DOSBox
* Install Borland C++ 3.0 in DOSBox, under `C:\BORLANDC`
* Clone this repo and mount its root as `C:` in DOSBox
* Copy the original Wolfenstein 3D data files in `C:\WOLF3D\WOLFSRC`
* Set `PATH` environment variable to include `C:\BORLANDC\BIN`

Stuff I've done to `WOLFSRC\WOLF3D.PRJ`
-------------------------------------------
* Set output directory to project directory, because the BC++ 3 IDE cannot force a working directory other than the project directory when running the executable
* Set output directory for `C0.ASM` as project directory
* Remove `SIGNON.OBJ` and `GAMEPAL.OBJ` dependencies and add them back from the `OBJ` folder
* Set `INCLUDE` directory to `C:\BORLANDC\INCLUDE` and `LIB` directory to `C:\BORLANDC\LIB`
* Set **Options -> Debugger -> Display Swapping** to **Always**, otherwise it messes the game output when debugging
* Set **Options -> Debugger -> Heap size** to **320K**, otherwise the game complains about not having enough memory

Using VSCode for **editing** the source code
----------------------------------------
* Put DOSBox on your `PATH`
* Create the following tasks in your `tasks.json` that looks like this :
```
{
    "label": "build wolf3d",
    "type": "shell",
    "command": "dosbox",
    "args": [
        "-noconsole",
        "-c",
        "'MOUNT C ${workspaceFolder}\\..\\..'",
        "-c",
        "'SET PATH=C:\\BORLANDC\\BIN;%%PATH%%'",
        "-c",
        "'C:\\'",
        "-c",
        "'CD WOLF3D\\WOLFSRC'",
        "-c",
        "'C:\\BORLANDC\\BIN\\BC.EXE /b WOLF3D.PRJ'",
        "-c",
        "'IF ERRORLEVEL 0 IF NOT ERRORLEVEL 1 EXIT'"
    ]
},
{
    "label": "run wolf3d",
    "type": "shell",
    "command": "dosbox",
    "args": [
        "WOLF3D.EXE",
        "-noconsole",
        "-exit"
    ]
},
{
    "label": "build, then run wolf3d",
    "type": "shell",
    "command": "dosbox",
    "args": [
        "-noconsole",
        "-c",
        "'MOUNT C ${workspaceFolder}\\..\\..'",
        "-c",
        "'SET PATH=C:\\BORLANDC\\BIN;%%PATH%%'",
        "-c",
        "'C:\\'",
        "-c",
        "'CD WOLF3D\\WOLFSRC'",
        "-c",
        "'C:\\BORLANDC\\BIN\\BC.EXE /b WOLF3D.PRJ'",
        "-c",
        "'IF ERRORLEVEL 0 IF NOT ERRORLEVEL 1 WOLF3D.EXE'",
        "-c",
        "'IF ERRORLEVEL 0 IF NOT ERRORLEVEL 1 EXIT'"
    ],
    "group": {
        "kind": "build",
        "isDefault": true
    }
}
```
* To run the game use `dosbox WOLF3D.EXE -exit`