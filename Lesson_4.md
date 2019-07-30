
##  Shell Scripting Example with PBS and Slurm
* Because SLURM calls a shell when launched any shell commands can can also be used in a Slurm script. 
* As an example, an MD Drug Docking experiment, MD3 -  Aspirin to A2 phospholipase, includes a range of Linux commands and shell script structures. This includes variable assignment, redirections, and loops. This job can be copied to a local directory and lauched like any other Slurm job. The jobscript and data files are at: `/usr/local/common/HPCshells/NAMD/drugdock.Slurm`
-- *Slide End* --


##  Automatic Script Generation
* A heredoc (also known as a here-string or here-document) is a file or input literal, a section of source code that is treated as a separate file with specified delimiters. In various Unix shells the '<<' with a delimiter name will treat subsequent code until the identifier as reached as a separate file. With the addition of a minus sign, leading tabs are ignored which aid formatting. 
-- *Slide End* --


##  Automatic Script Generation cont...
* For example, the command `tr a-z A-Z << END_TEXT` will conduct a translate on all data until a END_TEXT is reached in the doc for or `tr a-z A-Z <<< 'igneous sedimentary metamorphic'` in the string form. Variables can also be parsed. e.g.., `rocks='igneous sedimentary metamorphic'`, `tr a-z A-Z <<< $rocks`. 
* Heredocs can also be used however to create Slurm scripts. A loop can be used to create multiple jobs for submission. See `/usr/local/common/HPCshells/heres/herescript.sh`. See also `/usr/local/common/Gaussian`
-- *Slide End* --

