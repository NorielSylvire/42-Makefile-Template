# Develop Templates

Templates in the develop branch are used when you have already finished, validated and passed a project and you want to continue developing the project as opposed to templates in the main branch, which are used when you still haven't finished the project.

Templates in the main branch have quite a few less features, because you won't need them when turning a project in. This way you avoid running into problems caused by the extra stuff in the makefile.

## Features
There are a number of features available in this branch that the main branch just lacks so as to not provoke the wrath of moulinette or cause unexpected issues.

Features in develop that main doesn't have:
* Test rules: useful for developing your own unit tests and running them.
* Debug rule: it generates the debug files. Useful for debugging with lldb or any other tool.
* Local install rules: it installs the library into a user defined directory. Usage explained below.

## Variations
There are two variations of the template.
LibMakefile is used compiling libraries, while ProgMakefile is used for compiling programs.

Make sure to rename them to just Makefile before using!

## Usage
Copy the appropriate template into your project's directory.

Then rename the NAME macro acording to your project's subject.
If using the library template, also rename LIBNAME to be the same as the NAME but without the lib at the  beginning and without the .a at the end.

These makefiles are configured to use a very specific project structure.

### 

The src path is the path where all the source code files will be located.
Inside it there are other paths defined, such as:
* Include path: used for .h or any other header files. Put your bonus and test headers here too!
* Main source path: use this directory for the mandatory project's .c files.
* Bonus path: used for bonus .c files, if you have them.
* Test path: develop your test .c files, if any, here.
* Libft path: obviously this is the path to libft. Remove this if your project doesn't use  libft.

### 

The target path is where everything you compile will go.
If you want to clean everything in the project, just delete everything  in the target path or delete the target directory entirely!

Inside it there's two more paths:
* Binary path: this is the path where all executables and archives will go.
* Object path: all compiled objects go here.

### 

The local install (LI) paths are used for installing a copy of your library to a user-defined path.
This is useful for when you have already finished a project, like libft or printf, so that whenever you wanna use that library you don't need to copy the entire libft/printf project into your current project.

Instead, configure your GCC to use your custom include and lib paths and just use  `#iclude <libft.h>` instead of, for example, `#include "../../includes/libft/libft.h"`. Also, this way you don't really need to tell the compiler where to look for the library archive.

These are the default values for the local install paths:
* Include path: ~/include
* Library path: ~/lib

Why these specific paths? Because you can't really do a proper install of your library in 42's ACTUAL lib directory because it's protected and you can't write there.
If you could do this you woulnd't need to configure the compiler to use these custom lib and include paths.

But I guess this is the next best thing after doing a proper install.

### 

You can of course configure every single one of these paths to your liking.
For instance consider leaving the target path as just `.` and the binary path as just `$(TGT_PATH)/`, just like it is in the main branch.

This way your program/library will be compiled in the main project directory, like intended by the subject, and your objects will be compiled in `./obj` which is also a nice path.

## Usage

TO-DO: explain every rule and macro, and how to use them.
