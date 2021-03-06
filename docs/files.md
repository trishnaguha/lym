## File permissions

```eval_rst
.. index:: File permission
```

Linux followed the long Unix history, and has the same kind of permission and ownership of files and directories. In this chapter, we will learn in details about the same.

Let us look back the output of *ls -l* command.

```
$ ls -l
total 24
drwxrwxr-x. 2 fedora fedora 4096 Jun 24 08:00 dir1
-rw-rw-r--. 1 fedora fedora  174 Jun 23 13:26 files.tar.bz2
-rw-rw-r--. 1 fedora fedora  164 Jun 23 13:20 files.tar.gz
-rw-rw-r--. 1 fedora fedora   19 Jun 23 14:14 hello.txt
lrwxrwxrwx. 1 fedora fedora   13 Jun 23 12:32 name -> /etc/hostname
```

The first column contains the permission details of each file and directory. The permissions are displayed using groups of three values,
*r* for read access, *w* for write access, and *x* for execute access.
These 3 values are mentioned for owner,group, and other user accounts. The first - can be *d* for directories or *l* for links.

There is another way to calculate the same file permissions, using numbers.

```
|----------|-----|
| Read     | 4   |
|----------|-----|
| Write    | 2   |
|----------|-----|
| Execute  | 1   |
|----------|-----|
```

Means, if you want to give read and write access only to the owner and group, you can mention it like this "660", where the first digit is for
the owner, second digit is for the group, and the third digit is for the other users. We can use this format along with the *chmod* command to change permissions of any file or directory.

```eval_rst
.. index:: chmod
```
### chmod command

*chmod* is the command which changes the file mode bits. A few examples
are given below.

```
$ echo "hello" > myfile.txt
$ cat myfile.txt 
hello
$ ls -l myfile.txt
-rw-rw-r--. 1 fedora fedora 6 Jun 25 03:42 myfile.txt
$ chmod 000 myfile.txt 
$ ls -l myfile.txt
----------. 1 fedora fedora 6 Jun 25 03:42 myfile.txt
$ cat myfile.txt 
cat: myfile.txt: Permission denied
$ chmod 600 myfile.txt 
$ ls -l myfile.txt
-rw-------. 1 fedora fedora 6 Jun 25 03:42 myfile.txt
$ cat myfile.txt 
hello
```

In the first line, we created a new file called *myfile.txt* using the *echo* command (we redirected the output of echo into the file). Using the *chmod 000 myfile.txt* command, we removed the read/write permissions of the file, as you can see in the next line, even the owner of the file can not read it. Making the mode *600* brings back
read/write capability of the owner on that particular file.

The executable permission is required for the directory access, and also for any file you want to execute.

```eval_rst
.. index:: PATH
```
### PATH variable

The *PATH* variable is a special variable, when we type a command in the bash shell, it searches for the command in the directories menioned
in the PATH variable. We can know the current *PATH* value using the *echo* command.

```
$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/fedora/.local/bin:/home/fedora/bin
```

The different directories are separated by *:*. You can see that in the */home/fedora/bin* directory is mentioned in the path, means if we have that directory, and an executable file is there, we can use it as a normal command in our shell. We will see example of this in the later part of this book.

```eval_rst
.. index:: which
```
### which command

By using the *which* command, we can find out the exact path of the executable being used a command in our shell.

```
$ which chmod
/usr/bin/chmod
$ which tree
/usr/bin/which: no tree in (/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/fedora/.local/bin:/home/fedora/bin)
```

The second examples shows the output in case the *which* command can not find the executable mentioned.

### she-bang or sha-bang in executable files

she-bang or sha-bang is the first line the in scripts, which starts with *#!* and then the path of the interpreter which is to be used for the rest of the file. We will create a simple bash hello world script using the same, and then execute it.

![](/img/she-bang.png)

```
$ vim hello.sh
$ chmod +x hello.sh 
$ ./hello.sh 
Hello World!
```