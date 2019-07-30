# Basics of Regular Expressions


##  Regular Expressions and Metacharacters
* The main text searching, substitution, and reporting tools are grep, sed (stream editor), and awk (programming language) respectively.
* Regular expressions have meta-characters, some of which are described below.

| Metacharacter | Explanation         | Example                                          |
|:--------------|:-------------------|:-----------------------------------------------|
| ^             | Beginning of line anchor   | `grep '^row' /usr/share/dict/words`       |
| $             | End of line anchor         | `grep 'row$' /usr/share/dict/words`       |
-- *Slide End* --


##  Regular Expressions and Metacharacters cont..
| Metacharacter | Explanation        | Example   |
|---------------|--------------------|-----------|
| .             | Any single character       | `grep '^...row...$' /usr/share/dict/words` |
| *             | Match zero plus preceding characters | `grep '^...row.*' /usr/share/dict/words`   |
| [ ]           | Matches one in the set        | `grep '^[Pp]' /usr/share/dict/words`    |
-- *Slide End* --


##  Regular Expressions and Metacharacters cont..
| Metacharacter | Explanation        | Example   |
|---------------|--------------------|-----------|
| [x-y]		| Matches on in the range                | `grep '^[s-u].row..$' /usr/share/dict/words`   |
| [^ ]          | Matches one character not in the set   |  `grep '^[^a].row..$' /usr/share/dict/words`   |
| &#124;     | Logical OR   |  `grep '^[^a &#124; P].row..$' /usr/share/dict/words`   |
-- *Slide End* --


##  Regular Expressions and Metacharacters cont..
| Metacharacter | Explanation        | Example   |
|---------------|--------------------|-----------|
| [^x-y]        | Matches any character not in the range | `grep '^[^a-z].row..$' /usr/share/dict/words` |
| \             | Escape a metacharacter |  `grep '^A\.$' /usr/share/dict/words`
-- *Slide End* --


##  Regular Expressions and Metacharacters cont...
* The 'matches one in the set' metacharacter has a number of options that one may find useful.

| Metacharacter| Explanation                                             |
|--------------|---------------------------------------------------------|
| [:digit:]    | Only the digits 0 to 9                                  |
| [:alnum:]    | Any alphanumeric character 0 to 9 OR A to Z or a to z.  | 
| [:alpha:]    | Any alpha character A to Z or a to z.                   |
| [:blank:]    | Space and TAB characters only.                          |
-- *Slide End* --


##  Regular Expressions and Metacharacters cont...
* Metacharacters can be combined in an interesting manner with grep options. Examples; (i) using grep to count the number of empty lines in a file; `grep -c '^$' filename` (ii) a search for words with no vowels; `grep -v "[aeiou]" /usr/share/dict/words`
-- *Slide End* --


<img src="https://imgs.xkcd.com/comics/regular_expressions.png" />
-- *Slide End* --


##   Text Manipulation with sed
* Sed makes text transformation on an input stream (e.g., file) and has the general form of `sed [OPTION] [SCRIPT] [INPUT]`. Some common options are `e` (multiple scripts per command), `-f` (add script file) and `-i` (in-place editing).
* The general form of a script is `Command/RegExp/Replacement/Flags`. The most common command is `s` for `substitute`, and the most common flags are `g` (global) or a number for replacement thoughout each line and `I` to ignore case. 
* Sed has alternative three alternative delimiters in its scripts; '/', ':', or '|'
-- *Slide End* --


##  Text Manipulation with sed cont...
| Command                | Explanation                                                              |
|------------------------|:-------------------------------------------------------------------------|
| `sed 's/^/     /'`       | Insert five whitespaces at the beginning of every line.                  | 
| `sed '/baz/s/foo/bar/g'` |  Substitute all instances of 'foo' with 'bar' on lines that start with 'baz' |
| `sed '/baz/!s/foo/bar/g'`| Substitute "foo" with "bar" except for lines which contain "baz" |
| `sed /^$/d`    | Delete all blank lines.                                                    |
| `sed s/ *$//` | Delete all spaces at the end of every line.             |
-- *Slide End* --


##  : Text Manipulation with sed cont...
| Command               | Explanation                             |
|-----------------------|----------------------------------------|
| `sed -i 's/$/\r/g'`     | *nix to MS-Windows, adds CR.            | 
| `sed -i 's/\r$//g'`     | MS-Windows to *nix, removes CR          |

* A popular list of one-line sed commands can be found at the following URL 
http://sed.sourceforge.net/sed1line.txt
-- *Slide End* --


<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanAdvanced/master/Images/awk1.jpg" />
-- *Slide End* --


##  : Report Presentation with awk
* Awk is a data driven programming language, its name derived from the surname initial of the designers (Alfred Aho, Peter Weinberger, and Brian Kernighan). Awk is particularly good at understanding and manipulating text structured by fields - such as tables of rows and columns. 
* The essential organization of an AWK program follows the form: pattern { action }. This is sometimes structured with BEGIN and END which specify actions to be taken before any lines are read, and after the last line is read. With it's structured data features, awk can print columns by number ($0 equals everything).
-- *Slide End* --


##  Report Presentation with awk
* By default awk uses a space as the internal field separator. To use a comma invoke with `-F` e.g. `awk -F"," '{print $3}' quakes.csv`
* Adding new separators to the standard output print of multiple fields is recommended - otherwise AWK will print without any separators. For example; `awk -F"," '{print $1 " : " $3}' quakes.csv`
* Other commands can be piped through awk: `awk -F"," '{print $1 " : " $3 | "sort"}' quakes.csv | less`
-- *Slide End* --


##  Report Presentation with awk cont...
* 'NR' specified the row number. More examples:
`awk -F"," 'END {print NR}' quakes.csv`    
`awk -F"," 'NR>1{print $3 "," $2 "," $1}' quakes.csv`   
`awk -F"," '(NR <2) || (NR!=6) && (NR<9)' quakes.csv > selection.txt`   
-- *Slide End* --


##  Report Presentation with awk cont...
* Other useful awk one-liners make use of the arithmetic functions of this programming language:
* Print the total number of fields in $file.    
`awk '{totalf = totalf + NF }; END {print totalf}' $file`
* Print the sum of the fields (columns) of every line (row); NF is number of field.    
`awk '{sum=0; for (i=1; i<=NF; i++) sum=sum+$i; print sum}' $file`	
* A popular list of one-line awk commands can be found at the following URL   
`http://www.pement.org/awk/awk1line.txt`
-- *Slide End* --


##  Shells and Login Files
* The default shell environment is the Bash shell (Bourne-again shell). The shell is a program that acts as command interpreter between the user and the kernel.
* When Bash is invoked as an interactive login shell it first reads and executes commands from the file `/etc/profile`. It looks for `~/.bash_profile`, `~/.bash_login`, and `~/.profile`, in that order, and reads and executes commands from the first one that exists and is readable.
-- *Slide End* --


##  Shells and Login Files cont...
* Users can modify their `.bash_profile` to ensure that they have the environmental features that they want when they login.
* When a command is entered it is stored in `.bash_history`
* When a login shell exits, Bash reads and executes commands from the file `~/.bash_logout`, if it exists. 
-- *Slide End* --

