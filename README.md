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

#
These makefiles are configured to use a very specific project structure.
For example the src path is the path where all the source code files will be located.
See [Macros](https://github.com/NorielSylvire/42-Makefile-Template/tree/develop?tab=readme-ov-file#macros) for more info.

Make sure to change all the paths to your liking before using, and make sure your actual project structure and your path macros match!
For instance consider leaving the target path as just `.` and the binary path as just `$(TGT_PATH)/`, just like it is in the main branch.
This way your program/library will be compiled in `./`, your main project directory, like intended by the subject, and your objects will be compiled in `./obj` which is also a nice path.

## Rules and Macros <img src="https://img.shields.io/badge/Made%20With-Love-orange.svg" alt="Made With Love"/>
These templates all use a very specific set of rules and macros, some of which are custom and need explanation.
Make sure to read the [Usage](https://github.com/NorielSylvire/42-Makefile-Template/tree/develop?tab=readme-ov-file#usage) section, remove any comments and configure your Makefile before using it!

### Macros
Macros are separated into five different categories:

#
**Tools**

These macros are used to define which tools to use, and their flags. For example you can change the compiler to your preferred one.
Here's what each one does:
* NAME: this must be the same as the name in your subject. Example: libft.a
* LIBNAME: for compiling and using libraries, it must be the same as the NAME but without the lib at the beginning and without the .a at the end. Example: ft
* TNAME: this is the name of the test executable that will run your own custom tests. Example: test
* CC: choose your C Compiler. Examples: gcc, cc, clang
* CFLAGS: your default flags for the compiler. Put here every flag you'll want to use all the time. Example: -Wall -Wextra -Werror because these are mandatory by the subject.
* COBJFLAGS: these will be all the CFLAGS plus some extra that you decide you want for your objects. Example: $(CFLAGS) -c -fstanitize=address
* DBGFLAGS: these flags will be used only when debugging
* ARFLAGS: the flags used when making library archives. Example: -crs
* RMFLAGS: the default flags used when running rm. Example: -rfp

#
**Paths**

These macros are used to configure your project structure.
You can follow this structure or configure the Makefile to follow your own structure.

This is what each path means:

#
The src path is the path where all the source code files will be located.
All your `.c` and `.h` files must be located here.

Src paths:
* Include path: used for .h or any other header files. Put your bonus and test headers here too!
* Main source path: use this directory for the mandatory project's .c files.
* Bonus path: used for bonus .c files, if you have them.
* Test path: develop your test .c files, if any, here.
* Libft path: obviously this is the path to libft. Remove this if your project doesn't use  libft.

#
The target path is where everything you compile will go.
If you want to clean everything in the project, just delete everything in the target path or delete the target directory entirely!

Inside it there's two more paths:
* Binary path: this is the path where all executables and archives will go.
* Object path: all compiled objects go here.

#
The local install (LI) paths are used for installing a copy of your library to a user-defined path.
This is useful for when you have already finished a project, like libft or printf, so that whenever you wanna use that library you don't need to copy the entire libft/printf project into your current project.

Instead, configure your GCC to use your custom include and lib paths and just use  `#include <libft.h>` instead of, for example, `#include "../../includes/libft/libft.h"`, and instead of `#include "libft.h"` and then compiling with `gcc obj1.o obj2.o -Lyour/lib/dir -lyourlibname`.

These are the default values for the local install paths:
* Include path: ~/include
* Library path: ~/lib
* Binary path: ~/bin
When compiling a library, it'll use the lib path so that you can use your library as if it was a standard library.
When compiling a program, it copies the binary to your user's home/bin directory, so that you can run it as a command. Add that directory to your path variable inside your .zshrc file or any other shell config file.

Why these specific paths? Because you can't really do a proper install of your library in 42's ACTUAL lib directory because it's protected from writing there.
If you could do this you woulnd't need to configure the compiler to use these custom lib and include paths.
But I guess this is the next best thing after doing a proper install.

#
**Source and object files**

This is where you name each and every source file in your project.
Here's what each macro does:
* HDRS: list your header files here. Useful when doing a local install to put the latest version of your in your custom include path.
* MSRC: your main project source files. These are all the `.c` files in your **mandatory** version of the project.
* OBJ: the main source objects to be compiled
* BSRC: your bonus source files. These will be all the `..._bonus.c` files from the **bonus** version of the project.
* BOBJ: the bonus objects to be compiled.
* TSRC: you may want to make your project using TDD, in which case you will want to define the test `.c` files separately and compile them separately. These files could contain unit tests of your project, for instance.
* TOBJ: the test objects to be compiled.

#
**Config**

Configure your custom macros here.
The templates already come with a few custom macros:
* UNW: these are all the unwanted/garbage files that you'll want to delete often. Example: .DS_Store ./*/.DS_Store (this will remove every single one of those pesky .DS_Store files you often get when using 42's Macs. To use this run `make xclean` because it's Xtra clean!
* SECONDS_VISIBLE: the amount of time, in seconds, to wait before clearing the console in the ctry and cbtry rules. Use those when you just wanna see if your project compiles and passes the norm.
* BONUS: this one's optional. Use it and set it to 0 if you'll not be having separate `.._bonus.c` files and instead you'll use this variable to tell the program it's in bonus mode.

#
**Colors**

The templates come with multiple terminal colors to **bring** your **M**ak**e**file **to life**.
Usage examples: `@echo "$(RED)Everyhing after that will be red.$(GREEN)And now everything will be green.$(DEF_COLOR)And now back to the terminal's default color.\n"`

### Rules
Many of the template's rules are custom and require some explaining:
* all: runs $(NAME).
* $(NAME): compiles your program/library.
* debug: sets the DBGFLAGS to -g so that the compiler generates the files needed to use lldb/gdb properly.
* bonus: this could go one of two ways. You could **either** set the BONUS macro to 1 and then just run $(NAME) with an added -D$(BONUS) when you don't want separate bonus and mandatory files, **or** you can actually compile the separate BSRC files here. Choose one or the other.
* test: compiles and executes your unit tests, if any. Just remove this if you won't make your own tests.
* $(OBJ_PATH)/%.o: compiles the % object, where % is the name of a source file minus the `.c` at the end. If needed, makes a new directory for the object to be in.
* linstall: performs a local install of your program/library, to use it as a standard library or as a command.
* mkdir: makes all the necessary temporary directories.
* clean: cleans object files.
* fclean: cleans both object files and the actual program/library.
* xclean: cleans objects, the program/library, AND the unwanted files defined in the UNW macro.
* re: recompiles. Performs fclean then all.
* bre: recompiles for bonus. Performs fclean then bonus rule.
* try: recompiles, then cleans up, then runs norminette. Useful when you just wanna know if your program compiles and passes the norm.
* btry: recompiles the bonus, then cleans up, then runs norminette.
* ctry: runs try, then clear after SECONDS_VISIBLE seconds.
* cbtry: runs btry, then clear after SECONDS_VISIBLE seconds.

#
And that's it!
Thanks for giving my templates a try, and I hope they're useful to you.
Make sure to notify me if you run into any problems.
