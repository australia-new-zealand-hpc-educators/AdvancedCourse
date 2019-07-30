# Bash Shell Scripting


##  Shells and Login Files
* The default shell environment is the Bash shell (Bourne-again shell). The shell is a program that acts as command interpreter between the user and the kernel.
* When Bash is invoked as an interactive login shell it first reads and executes commands from the file `/etc/profile`. It looks for `~/.bash_profile`, `~/.bash_login`, and `~/.profile`, in that order, and reads and executes commands from the first one that exists and is readable.
-- *Slide End* --


##  Shells and Login Files cont...
* Users can modify their `.bash_profile` to ensure that they have the environmental features that they want when they login.
* When a command is entered it is stored in `.bash_history`
* When a login shell exits, Bash reads and executes commands from the file `~/.bash_logout`, if it exists. 
-- *Slide End* --


##  Example extended .bash_profile
* A sample extended `.bash_profile` is available from the directory `/usr/local/common/HPCshells`
* Includes alias, history size modifications etc.
-- *Slide End* --


##  Various Shells
* Examples of various shells include the *nix-universal Bourne shell (sh) Bourne-Again shell (bash), Z shell (zsh), Korn shell (ksh), extended C shell (tcsh) and the friendly interactive shell (fish). There is even an amusing attempt to develop a shell into a text-based adventure game (Adventure shell, available at `http://nadvsh.sourceforge.net/`).
* To view what shells are available; `ls -l /bin/*sh*`
-- *Slide End* --


##  Various Shells cont...
* Each have different features and often slightly different syntax, which is mostly beyond the scope of this course. However among bash and tsch the following are two major differences.

| Value       |    bash          |    tcsh             |
|-------------|------------------|--------------------|
|Variable     |  `var=val`       |  `set var=val`        |
|Environment  |  `export var=val`  |  `setenv var val`     | 
-- *Slide End* --


##  Bash Shell Shortcuts
| Value       | Explanation                                                                     |
|-------------|:--------------------------------------------------------------------------------|
| ~           | Shortcut to user's home directory.                                              | 
| .           | The current directory.                                                          | 
| ..          | One level up in the file system hierarchy.                                      | 
| TAB         | Autocompletion suggestions.                                                     | 
| !!          | Repeat last typed command; can be combined with other commands.                 | 
| !ec	      | Repeat last typed command that started with 'ec'                                |
| &&          | Combine commands if the first succeeds (e.g., make && make install)                     | 
| &#124;&#124; | Alternative command if the first fails (e.g., make makefile1 &#124;&#124; make Makefile)  | 
-- *Slide End* --


##  Bash Shell Shortcuts cont...
| Value       | Explanation                                                                     |
|-------------|:--------------------------------------------------------------------------------|
| ctrl+w      | Remove word behind cursor.                                                      | 
| ctrl+u      | Delete everything from cursor to beginning of the line                          | 
| alt+f       | Go forward to the end of the previous word                                      | 
| alt+b       | Move cursor back to the beginning of the previous word                          | 
| ctrl+d      | Quick logout.                                                                   | 
| ctrl+r      | Recursive search through your history to locate previous commands.              | 
| ctrl+z      | Stop the current process.                                                       |
-- *Slide End* --


##  Use of Shell Scripting
* Shell scripts combine Linux commands with logical operations. It is an underrated utility, but it is not the answer for everything.
* They are not always great at resource intensive tasks (e.g., extensive file operations) where speed is important. They are certainly not recommended for heavy-duty mathematical operations (e.g., floating point) - use programming language instead. They are not recommended in situations where data structures, multi-dimensional arrays (it's not a database!) and port/socket I/O is important. 
-- *Slide End* --


##  Scripts with Variables
*  The most basic form of scripting simply follows commands in sequence, such as this rather undeveloped backup script, which runs tar and gzip on the home directory. A version of this is available at: `/usr/local/common/HPCshells/backup1.sh`
* Not much of a script! Consider what parts can be made into variables. `/usr/local/common/HPCshells/backup2.sh`
* A variable is prefaced by a dollar sign ($) to refer to its value. 
-- *Slide End* --


##  Special Characters
* There are also a number of special characters in bash scripting. 
* Quoting disables these characters for the content within the quotes. Both single and double quotes can be used, and single quotes can be used to incorporate double quotes. 
* "Backtick" quotation marks can be used for command substitution within the script, but they are not POSIX standard. 
* Examples: 
`echo 'The "Sedimentary" and the "Igenuous" argue about metamorphism'`   
`echo "There are $(ls | wc -l) files in $(pwd)"`
-- *Slide End* --


##  Scripts with Loops
* In addition to variable assignments, bash scripting allows for loops (for/do, while/do, util/do). 
* The for loop executes stated commands for each value in the list.
* The while loop allows for repetitive execution of a list of commands, as long as the command controlling the while loop executes successfully.
* The until loop executes until the test condition executes successfully.
-- *Slide End* --


##  Scripts with Loops cont...
* Examples of these scripts are in  `/usr/local/common/HPCshells/loops.txt`
* These can be converted to permanent scripts e.g., `/usr/local/common/HPCshells/lowercaserename.sh` and `/usr/local/common/HPCshells/sshtrigger.sh`
-- *Slide End* --


<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanAdvanced/master/Images/whilenotedge.jpg" />
-- *Slide End* --


##  Scripts with Conditionals
* A set of conditions can be expressed through an if/then/fi structure. A single test with an alternative set of commands is expressed if/then/else/fi. Finally, a switch-like structure can be constructed through a series of elif statements in a if/then/elif/elif/.../else/fi structure. i.e.,
1. if..then..fi statement (Simple) 
2. if..then..else..fi statement (Optional) 
3. if..elif..else..fi statement (Ladder) 
4. if..then..else..if..then..fi..fi..(Nested) 
* An example is available at: `/usr/local/common/HPCshells/filetest.sh`
-- *Slide End* --


##  Scripts with Conditionals cont...
* There are several conditional expressions that could be used to test with the files. The following are few common examples; 

| Value                           |Explanation                                                   |
|---------------------------------|-------------------------------------------------------------|
| [ -e filepath ]                 | Returns true if file exists.                                 |
| [$var lt value ] [ gt ] [ eq ]  | Returns true if less than, greater than or equal             |
| [ -f filepath ]                 | Returns true if filepath is actually a file.                 |
| [ -x filepath ]                 | Returns true if file exists and executable.                  |
-- *Slide End* --


##  Scripts with Conditionals cont...
| Value                           |Explanation                                                   |
|---------------------------------|-------------------------------------------------------------|
| [ -S filepath ]                 | Returns true if file exists and its a socket file.           |
| [ expr1 -a expr2 ]              | Returns true if both the expression is true.                 |
| [ expr1 -o expr2 ]              | Returns true if either of the expression1 or 2 is true.      | 
-- *Slide End* --


##  Scripts with Conditionals cont...
* Conditionals can also be interrupted and resumed using the 'break' and 'continue' statements. The break command terminates the loop (breaks out of it), while continue causes a jump to the next iteration (repetition) of the loop, skipping all the remaining commands in that particular loop cycle. Examples at: `/usr/local/common/HPCshells/break.sh` and `/usr/local/common/HPCshells/continue.sh`
* A variant on the conditional to escape the problems associated with deeply nested if-then-else statements is the `case` statement. The first match executes the listed commands. Examples at: `/usr/local/common/HPCshells/case.sh`
-- *Slide End* --


##  Script Selects and Functions
* The select command with conditionals can be used to create simple menus for users which prompts them for their input. There is an example at: `/usr/local/common/HPCshells/select.sh`
* Functions subroutines or subscripts within a shell script, which can have local variables, accept, and return parameters. Functions may not be empty. See the example at: `/usr/local/common/HPCshells/hellofunction.sh`
-- *Slide End* --


##  Scripting Conventions
* There are several scripting conventions which make the code more effective, more robust, more portable, and more readable. Therefore use them!
* The following example at: `/usr/local/common/HPCshells/findemails.sh` and the datafile `/usr/local/common/HPCshells/hidden.txt` will illustrate some of these conventions.
-- *Slide End* --


##  Scripting Conventions cont...
* Liberally comment your code so that other readers know what it does. Use explicit variable names. Use output to tell the user what is happening. Use variables when appropriate rather than hard-coded paths. Provide exit statements to clear variables and provide an error code.
* A common conditional, and sadly often forgotten, is whether or not a script has the requiste files for input and output specified!
* Invite user input with the 'read' command; protect against escape characters with the 'raw' option.
-- *Slide End* --


##  Metacharacters
* Metacharacters have meaning beyond their literal meaning. Powerful, but use with caution (e.g., wildcards). Metacharacter meaning depends very much on the context, which can cause problems. For example;
* the semi-colon can be a command separator in a script or a double as a terminator in a case statement. 
* the colon represents a null command in a script, or as a field separator (e.g., in `/etc/passwd`).
* the dot (.) is used to source a filename, to represent the current working directory as a path, to represent a character in regular expression, or in multiple form as a sequence.
-- *Slide End* --


##  Metacharacters cont ..
* Single quotes however will interpret anything literally between the quotes as a string with no interpretation to a meta-character (aka 'strong quoting'). Double quotes will substitute a limited set which are usually the symbols which are wanted in their interpreted mode. e.g., variables, backticks, and sometimes backslash escapes. (aka "weak quoting"). n example is given at `/usr/local/common/HPCshells/quotes.sh`
-- *Slide End* --


##  Metacharacters cont ..
* In some cases backtics are seen for command substitution. This is not a POSIX standard, it does exist for historical reasons. Nesting commands with backticks also requires escape characters; the deeper the nesting the more escape characters required. e.g., echo "Hello, $(whoami)".
-- *Slide End* --


##  Script Commands
* A script can also be initiated in the background with an ampersand. 
* The commands `fg` (foreground) and `bg` (background) are complementary manipulations of processes.  Jobs can be suspended with Cntrl-Z to return to the terminal. 
* A background job can be killed with `kill %job-number`. A listing of jobs can be achieved with the `jobs` command.
-- *Slide End* --


##  Script  Commands cont...
* For example;
`eval 'for i in {1..100}; do sleep 2; echo "Igneous" >> rocks.txt ; done' &`    
`eval 'for i in {1..100}; do sleep 2; echo "Sedimentary" >> rocks.txt ; done'`    
`eval 'for i in {1..100}; do sleep 2; echo "Metamorphic" >> rocks.txt ; done' &`    
* It is important not to run large scripts on the login node. Set up a job on a compute node with `sinteractive`.
-- *Slide End* --

