
- ### Terminal/CLI
	- A shell is a tool for interacting with a computer
		- **CLI** - Command Line Interface
	- Multiple different shell programs, but many common aspects
	- ###### Shell interface is a language for running programs and manipulating their input/output
		- Less user friendly than GUI
		- More expressive

- ### Basics
	- On GUI systems, you can access a shell with a terminal emulator
		- Ex. Terminal, Xterm
	- Shell will print a prompt and wait for a command
		- Prompt is customizable, but often written as $ or > in documentation
	- Command is interpreted by the shell, and will typically launch one or more programs
	- Certain characters are special, need to be put in quotes or escape

- ### Commands
	- A command is broken up into space separated words
	- The first word indicates a program to be run
	- ###### Additional words are arguments to that program
		- Not literally arguments being passed into program
		- Ex. `> mv old_file new_file`
			- mv renames (or moves)
		- Ex. `> rm old_file`
			- Deletes old_file
			- NO RECOVERY
			- Add `-r` to delete a directory recursively

- ### Optional arguments
	- Many programs have optional arguments that change their behavior
		- Each program defines its own options; the shell does not interpret them
	- By convention, options start with - or --
		- Some programs allow options with single-character names to be combined
	- ###### Ex. `ls` optional arguments
		- `ls` lists files
		- `ls -l` lists files with additional info (`l` = long)
		- `ls -l -t -r` or `ls -ltr` lists files with additional info (`l` = long), sorted by time (`t`), with newest at the end (`r` = reverse)
		- `ls -a` lists all files, including hidden ones (starting with `.`)

- ### File names
	- Files are referred to using path names
	- A path is a sequence of zero or more directory names followed by a file or directory name, separated by slashes (`/`)
		- Ex. `/path/to/my/file` - all names except the last must be directory names
	- A path that starts with `/` is absolute; other paths are interpreted relative to some starting point
	- A path ending with `/` always indicates a directory
	- File extensions are not necessary

- ### Relative paths
	- Absolute paths are long and can be inconvenient to use
	- Relative paths describe a file in terms of some starting place "the working directory"
		- A file or directory name by itself refers to a file in the cwd
	- A path describes a sequence of steps, starting in the cwd
		- Longer paths such as foo/bar refers to a file bar inside a directory foo that is in the cwd
	- `..` in a path indicates the parent of a the cwd
	- `../..` refers to the parent of the parent of the cwd
	- `.` indicates the cwd

- ### Referring to files in a shell
	- The shell adds some extra syntax for conveniently using files
	- `~` always indicates the user's home directory
		- Shell expands ~ before it is passed to a program
	- `?` and `*` are wildcards that can be replaced by a single character or any number of characters respectively
		- A name such as `foo*txt` matches any file in a directory that begins with foo and ends with txt

- ### Using wildcards
	- List all C source code in directory: `ls *.c`
	- List all C source code in sub-directories: `ls */*.c`
	- List all C files in parent directory's sub-directories: `ls ../*/*.c`
	- Copy all C source and header files to some directory: `cp *.c *.h backup`
	- Using wildcards only makes sense for programs that take a variable number of arguments
	- Note: `*` never lists files starting with `.` unless the `.` is explicit

- ### Processes
	- Process is a program currently running
		- Each process has unique process id
	- `ps` lists the processes you have started in your current session
	- `top` provides an updated list of current running processes
		- `htop` is nicer version of this
	- `kill PROCESS_ID` kills processes