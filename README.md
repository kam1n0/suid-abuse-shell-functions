# suid-abuse-shell-functions
*Credit to Tib3rius* | https://tryhackme.com/room/linuxprivesc

* In Bash versions <4.2-048 it is possible to define shell functions with names that resemble file paths, then export those functions to that they are used instead of any actual executable at that file path.

* Find all the SUID/SGID executables on the machine

link suid

1) Execute 'suid-env2' and note that it seems to be trying to start the apache2 webserver:

link suid-env2

2) Run strings on the file to look for strings of printable characters:

link strings

* The last line "/usr/sbin/service apache2 start" suggests that the service executable is being called to start the webserver.
* The full path of the executable (/usr/sbin/service) is being used.

3) Verify the version of Bash installed on the machine is less than 4.2-048:

link version

4) Create a Bash function with the name "/usr/sbin/service" that executes a new Bash shell (using -p so permissions are preserved) and export the function:

link function

5) Run the suid-env2 executable to gain a root shell:

link root
