# Advanced Linux Environment Commands


##   Archiving and Compressing Files
* Copy the file from `/usr/local/common/HPCshells/class.tar.gz` to the home directory.
* The double-barelled suffix, .tar.gz indicates that it is an archive ("tape archive"!) and compressed (with the gzip application). Such a file (often appearing as *.tgz) is often referred to as a "tarball".
* The type of a file can often be determined by the file command: `file class.tar.gz`
-- *Slide End* --


##  Archiving and Compressing Files cont...
* To review the contents of a tarball (check for tarbombs!): `tar tf class.tar.gz`
* To recover from a tarbomb: `tar tf tarbomb.tar | xargs rm -rf`
* To extract (and compare value of compression): `tar xvf class.tar.gz`
* To create a tarball: `tar cvfz name.tar.gz directory/`
-- *Slide End* --


<img src="https://imgs.xkcd.com/comics/tar.png" height="125%" width="125%" />
-- *Slide End* --


##  Archiving and Compressing Files cont ...
* Another common compression algorithm that Linux users are likely to encounter with regularity is bzip2.
* Efficient in size, slower in decompression speed.
* To create a bzip2 tarball: `tar cvfj class.tar.bz2 class/`
* To check the contents: `tar tjf class.tar.gz` 
* To extract and uncompress the tarball : `tar xvf class.tar.bz2`
-- *Slide End* --


##  Archiving and Compressing Files cont ...
* But wait, there's more! A third common compression is LZMA2 which is used in xz files.
* Like bzip2 efficient in size, slower in decompression speed.
* To create a xz tarball: `tar cvfJ class.tar.xz class/`
* To check the contents: `tar tf class.tar.xz` 
* To extract and uncompress the tarball : `tar xvf class.tar.xz`
-- *Slide End* --


##  Redirections and Tee
* A principle of UNIX-like systems is that the output of one program can be used as the input for another.
* The introductory lesson included basic commands for redirection, concatenation, and piping.
* Process streams as well as data streams can be redirected: `diff <(ssh user@spartan.hpc.unimelb.edu.au ls -R (/home/lev/data/) <(ls -R /home/lev/workdata/)`
* The default behaviour is to accept inputs from the terminal (standard input) and display the results, either output or errors, to the terminal (standard output). 
-- *Slide End* --


##  Redirections and Tee cont..
* Redirections can be further modified by placing a file descriptor (fd) next immediately before the redirector. These fd numbers are 0 (standard input), 1 (standard output), 2 (standard error). e.g., `ls -d /home/username/seismic 2> error.txt`
* Standard error can also to be redirected to the same destination that standard output is directed to using 2>&1; it merges stderr (2) into stdout (1).
-- *Slide End* --


##  Redirections and Tee cont..
* The tee command copies standard input to standard output and also to any files included in the tee. When combined with pipes it takes input from a single direction and outputs it two directions. e.g.,  `who -u | tee whofile.txt | grep username`
-- *Slide End* --


##  Redirections and Tee Summary
| Redirection Syntax                | Explanation                                                    |
|:----------------------------------|:--------------------------------------------------------------:|
|`command > file`                   | Redirect standard output to a file                             |
|`command >> file`                  | Redirect standard output to end of file                        |
|`command 2> file`                  | Redirect standard error to a file                              |
|`command -options < file`          | Redirect a file as standard input to a command                 |
-- *Slide End* --


##  Redirections and Tee Summary cont..
| Redirection Syntax                | Explanation                                                    |
|:----------------------------------|:--------------------------------------------------------------:|
|`command > file 2>&1`              | Redirect standard output and standard error to file            |
|`command >> file 2>&1`             | Redirect standard and standard error to end of file            |
| <code>command &#124; command2</code>  | Pipe standard output to a second command                   |
-- *Slide End* --


##  Redirections and Tee Summary cont..
| Redirection Syntax                | Explanation                                                    |
|:----------------------------------|:--------------------------------------------------------------:|
|<code>command 2>&1 &#124; command2</code>  | Pipe standard output and standard error to a second command    |
|<code>command1 &#124; tee file &#124; command2</code> | Apply command1 and command2 to file        |
-- *Slide End* --


##  File Attributes, Types, Ownership
* The `ls -l` command illustrates file ownership (user, group), file type, permissions, and date when last modified.
* The first character is type; a "-" for a regular file, a "d" for a directory, and "l" for a symbolic link. Less common file types include "b" for block devices (e.g., hard drives, ram etc), "c" for character devices which stream data one character at a time (e.g., mice, keyboards, virtual terminals).
* In UNIX-like operating systems devices are a type of file as well, and are structured under the `/dev` directory. 
-- *Slide End* --


##  File Attributes, Types, Ownership
*  Permissions are expressed in a block of three for "user, group, others" and for permission type (read r, write w, execute x). Executable also implies 'searching', thus "x" is usually found for directories as well.
* An "s" in the execute field indicated setuid. Causes any user or process to have access to system resources as though they are the owner of the file. If the bit is set for the group, the set group ID bit is set and the user running the program is given access based on access permission for the group the file belongs to.
-- *Slide End* --


##  File Attributes, Types, Ownership cont
* There is "t", "save text attribute", or more commonly known as "sticky bit" in the execute field allows a user to delete or modify only those files in the directory that they own or have write permission for. A typical example is the /tmp directory, which is world-writeable.
* The change permissions of a file use the `chmod` command. To chmod a file you have to own it. The command is : chmod [option] [symbolic | octal] file. For options, the most common is `-R` which changes files and directories recursively.
-- *Slide End* --


##  File Attributes, Types, Ownership cont
* For symbolic notation, first establish the user reference, either "u" (user, the owner of the file), "g" (group, members of the file's group), "o" (others, neither the owner or group members), or "a" (all). If a user reference is not specified the operator and mode applies to all.
* Then determine the operation; either "+" (add the mode), "-" remove the mode, or "=" (equals, mode only equals that expression). Finally, specify the mode permissions as described above, "r" (read), "w" (write), "x" (execute), "s" (setuid, setgid), "t" (sticky). 
-- *Slide End* --


##  File Attributes, Types, Ownership cont
* In octal notation a three or four digit base-8 value is presented derived from the sum of the component bits, so the equivalent of "r" in symbolic notation adds 4 in octal notation (binary 100), "w" in symbolic notation adds 2 in octal notation (binary 010) and "x" adds 1 in octal notation (binary 001). No permissions adds 0 (binary 000). For special modes the first octal digit is either set to 4 (setuid), 2 (setgid), or 1 (sticky). 
* The sum of the three (or four components) thus makes up an alternative exact notation for the chmod command (e.g., 0640. 750 etc).
-- *Slide End* --


<img src="https://raw.githubusercontent.com/UoM-ResPlat-DevOps/SpartanAdvanced/master/Images/jamesbond007.jpg" />
-- *Slide End* --


##  File Attributes, Types, Ownership cont
* If you have root permission, you can make use of the `chown` (change owner) command. Usually group is optional on the grounds that users are usually provided ownership. A common use is to provide ownership to web-writeable directories e.g., (`chown -R www-data:www-data /var/www/files`). 
-- *Slide End* --


##  File Attributes, Types, Ownership cont
* A `umask` ("user mask") which we encountered in the .bashrc limiting the permission modes for files and directories created by a process. When a program or script creates a file or directory, it specifies  permissions. Typical umask values are 022 (removing the write permission for the group and others) and 002 (removing the write permission for others).
-- *Slide End* --


##  Links and File Content
* The ln command creates a link, associating one file with another. There are two basic types; a hard link (the default) and a symbolic link. 
* The core difference is that a hard link is a specific location of physical data, whereas a symbolic link is an abstract location of another file. Hard links cannot link directories and nor can they cross system boundaries; symbolic links can do both of these. 
* The general syntax for links is: `ln [option] source destination` .This most common option is `-s`, to create a symbolic link. The source is the original file. The destination is the link.
-- *Slide End* --


##  Links and File Content cont...
* With a hard link: File1 -> Data1 and File2 -> Data1 . With a symbolic link: File2 -> File1 -> Data1
* A file consists of a filename and an inode reference. The reference maps to the actual inode. The inode contains the permissions, and data address. More than one filename can have the same inode reference
* Links are particularly useful if you want to share a file with another user, such as working on a collaborative paper (ensure that read/write access is granted). 
-- *Slide End* --


##  File Manipulation Commands
* The command head and tail print the first and last ten lines of a file by default. The standard syntax is `[head..tail] [option] [file]`. The most typical option is `-n` for the number of lines. 
* Rename will rename the specified files by replacing the first occurrence of expression in their name by replacement. e.g., `rename .txt .bak *.txt`
-- *Slide End* --


##  File Manipulation Commands cont...
* Split can be used to split large files into smaller components. The general syntax is `split [OPTION]... [INPUT [PREFIX]]`. Common options include byte (-b #) or linecount (-l #, default of 1000) for the new files. The input is the filename and the prefix is the output, PREFIXaa, PREFIXab etc.
-- *Slide End* --


##  File Manipulation Commands cont...
* The `cut` command copies a secion from each line of a file, based on the arguments parsed to it, whereas `paste` merges lines of files together. 
* Can operate on characters, delimiters (tab by default), or fields. 
`cut -d',' -f3 quakes.csv > latitude.txt` `cut -d',' -f4 quakes.csv > longitude.txt` `paste -d " " latitude.txt longitude.txt > quakelist.txt`
-- *Slide End* --


##  File Manipulation Commands cont...
* A variation on the `paste` command is the `join` command. Like paste, `join` will take two files and combine the fields. Unlike `paste` however `join` will only do if there is a common field. The common field however is only included once in the standard output.
* Very handy for combining tables with a common field!
-- *Slide End* --


##  File Manipulation Commands cont...
* The `sort` command will organise a text file into an order specified by options. The general syntax is `sort [option] [input file] -o [filename]`.
* Some of the options include -b (ignore beginning spaces), -d (use dictionary order, ignore punctuation), -m (merge two input files into one sorted output, and -r (sort in reverse order). 
* An interesting option for sort is for natural language ordering (e.g., 1, 10, 2, 20); for this case use `sort -g` filename (generic) or `-V` (version number).
* The `sort` command also has a very useful option for sorting by columns. Delimiters can be established with the -t option (e.g., `-t,` for comma separated values) and fields with the the `-k` option (e.g., sort by the second field in numeric order in a comma separated file would be sort -t, -nk2 fiename.csv)
-- *Slide End* --


##  File Manipulation Commands cont...
* To filter repeated lines in a text file use uniq. The standard syntax is `uniq [options] [input file] [output file]`. A simple example is `uniq repeats.txt unique.txt`. It is sometimes used with `sort` e.g., `sort repeats.txt | uniq > sortuniq.txt`. The combination of sort and uniq can be used to remove from the content file in the removals files(e.g., `sort content.txt removals.txt | uniq -u`).
-- *Slide End* --


##  System Information Commands
* The du "disk usage' command has the standard syntax of `du [options] [file]`. Without arguments `du` will print all files, entering directories recursively, with output in kilobytes. Most commonly experessed as `du -sh` (disk usage, summary form, human readable)
*  The following is a handy use of xargs is to parse a directory list and output the results to a file. The command script below runs a disk usage in summary, sorts in order of size and exports to the file diskuse.txt. The "\n" is to ignore spaces in filenames.
`du -sk * | sort -nr | cut -f2 | xargs -d "\n" du -sh  > diskuse.txt`
-- *Slide End* --

 
##  System Information Commands cont...
* The command 'df' will generate a report of file system disk space usage.
* The command `free -h` provides total, used, and free memory on a system.
* A typical command to access system information is `uname`, with the simple syntax `uname [options]`. The most common command is uname -a (all) which provides, in order, kernel name, network node name, kernel release and version, machine hardware name, processor and hardware platform (if known), and operating system. 
-- *Slide End* --


##  System Information Commands cont...
* Another useful source for system information is the /proc directory. The directory doesn't actually contain 'real' files but runtime system information. Examples: `less /proc/cpuinfo`, `less /proc/filesystems`, `less /proc/uptime`, `less /proc/meminfo`, `less /proc/mounts`, `less /proc/partitions`
* The command lscpu will provide information about the processor architecture as well gathered from /proc/cpuinfo including the number of CPUs, threads, cores, and sockets. 
-- *Slide End* --

