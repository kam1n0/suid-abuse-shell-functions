# suid-abuse-shell-functions
*Credit to Tib3rius* | https://tryhackme.com/room/linuxprivesc

* In Bash versions <4.2-048 it is possible to define shell functions with names that resemble file paths, then export those functions to that they are used instead of any actual executable at that file path.

* Find all the SUID/SGID executables on the machine

[![Image of suid](https://github.com/kam1n0/suid-abuse-shell-functions/blob/master/tmp_upload/suid.png)](#)

1) Execute 'suid-env2' and note that it seems to be trying to start the apache2 webserver:

[![Image of suid-env2](https://github.com/kam1n0/suid-abuse-shell-functions/blob/master/tmp_upload/suid-env2.png)](#)

2) Run strings on the file to look for strings of printable characters:

[![Image of strings](https://github.com/kam1n0/suid-abuse-shell-functions/blob/master/tmp_upload/strings.png)](#)

* The last line "/usr/sbin/service apache2 start" suggests that the service executable is being called to start the webserver.
* The full path of the executable (/usr/sbin/service) is being used.

3) Verify the version of Bash installed on the machine is less than 4.2-048:

[![Image of version](https://github.com/kam1n0/suid-abuse-shell-functions/blob/master/tmp_upload/version.png)](#)

4) Create a Bash function with the name "/usr/sbin/service" that executes a new Bash shell (using -p so permissions are preserved) and export the function:

[![Image of function](https://github.com/kam1n0/suid-abuse-shell-functions/blob/master/tmp_upload/function.png)](#)

5) Run the suid-env2 executable to gain a root shell:

[![Image of root](https://github.com/kam1n0/suid-abuse-shell-functions/blob/master/tmp_upload/root.png)](#)
