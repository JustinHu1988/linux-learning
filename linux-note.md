
## some simple commands

- date
- cal
- df
- free
- exit

switch to virtual terminal(in graphical desktop): Ctrl+Alt+F1 - Ctrl+Alt+F6
switch (in virtual terminal): Alt+F1 - Alt+F7

##file system

- pwd - Print name of current working directory
- cd - Change directory
- ls - List directory contents
 
 In general, if you do not specify a pathname to something, the working directory will be assumed.

Some cd shortcuts:

- cd : Changes the working directory to your home directory.
- cd - : Changes the working directory to the previous working directory.
- cd ~user_name : Changes the working directory to the home directory of user_name. For example, cd ~bob will change the directory to the home directory of user "bob".

>Important Facts About Filenames
- Filenames that begin with a period character are hidden.
- Filenames and commands in Linux are case sensitive.
- Linux has no concept of a "file extension".
- Limit the punctuation characters in the names of files you create to period, dash, and underscore. Do not embed spaces in filenames. If you want to represent spaces between words in a filename, use underscore characters.


## Linux System

- ls - List directory contents
- file - Determine file type
- less - View file contents

As we explore the system it will be useful to know what files contain. To do this we will use the file command to determine a file's type. Filenames in Linux are not required to reflect a file's content. While a filename like "picture.jpg" would normally be expected to contain a JPEG compressed image, it is not required to in Linux. We can invoke the file command this way:

    file filename
    
When invoked, the file command will print a brief description of the file's contents.

There are many kinds of files. In fact, one of the common ideas in Unix-like operating systems such as Linux is that "everything is a file".

While many of the files on your system are familiar, for example MP3 and JPEG, there are many kinds that are a little less obvious and a few that are quite strange.

**less**

The less command is program to view text files. Throughout our Linux system, there are many files that contain human-readable text. The less program provides a convenient way to examine them.

>What Is "Text"
There are many ways to represent information on a computer. All methods involve defining a relationship between the information and some numbers that will be used to represent it.
Some of these representation systems are very complex (such as compressed video files), while others are rather simple. One of the earliest and simplest is called ASCII text.
Text is a simple one-to-one mapping of characters to numbers. It is very compact. It is important to understand that text only contains a simple mapping of characters to numbers.
Plain ASCII text files contain only the characters themselves and a few rudimentary control codes like tabs, carriage returns and line feeds.
Throughout a Linux system, many files are stored in text format and there are many Linux tools that work with text files.

Why would we want to examine text files? Because many of the files that contain system settings(called configuration files) are stored in this format, and being able to read them gives us insight about how the system works. In addition, many of the actual programs that the system uses (called scripts) are stored iin this format.

The less command is used like this:

    less filename
    
Two kinds of links:

- symbolic link
- hard link


##操作文件和目录

- cp - Copy files and directories
- mv - Move/rename files and directories
- mkdir - Create directories
- rm - Remove files and directories
- ln - Create hard and symbolic

While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command line programs.
For example, how could we copy all the HTML files from one directory to another, but only copy files that do not exist in the destination directory or are newer than versions in the destination directory? Pretty hard with a file manager. Pretty easy with the command line:

    cp -u *.html destination

**通配符(wildcard)**
Since the shell uses filenames so much, it provides special characters to help you rapidly specify groups of filenames. These special characters are called wildcards. Using wildcards (which is also known as globbing) allow you to select filenames based on patterns of characters. The table below lists the wildcards and what they select:

- \*  Matches any characters
- ?  Matches any single characters
- [characters]  Matches any character that is a member of the set characters
- [!characters]  Matches any character that is not a member of the set characters
- [[:class:]]  Matches any character that is a member of the specified class

**Commonly Used Character Classes**

- [:alnum:]  Matches any alphanumeric character
- [:alpha:]  Matches any alphabetic character
- [:digit:]  Matches any numeral
- [:lower:]  Matches any lowercase letter
- [:upper:]  Matches any uppercase letter

Using wildcards makes it possible to construct very sophisticated selection criteria for filenames.
Here are some examples of patterns and what they match:

- \*  All files
- g*  All files beginning with "g"
- b*.txt  Any file beginning with "b" followed by any characters and ending with ".txt"
- Data???  Any file beginning with "Data" followed by exactly three characters
- [abc]*  Any file beginning with either an "a", a "b", or a "c"
- BACKUP.[0-9][0-9][0-9]  Any file beginning with "BACKUP." followed by exactly three numerals
- [[:upper:]]*  Any file beginning with a uppercase letter
- [![:digit:]]*  Any file not beginning with a numeral
- *[[:lower:]123]  Any file ending with a lowercase letter or the numerals "1", "2", or "3"

Wildcards can be used with any command that accepts filenames as arguments.

>Character Ranges
If you are comming from another Unix-like environment or have been reading some other books on this subject, you may have encountered the [A-Z] or the [a-z] character range notations. These are traditional Unix notations and worked in older versions of Linux as well. But you have to be very careful with them because they will not produce the expected results unless properly configured. For now, you should avoid using them and use character classes instead.

>Wildcards Work In The GUI Too
Wildcards are especially valuable not only because they are used so frequently on the command line, but are also supported by some graphical file managers.

### mkdir - 创建目录

    mkdir directory...
    
A note on notation: When three periods follow an argument in the description of a command(as above), it means that the argument can be repeated, thus:

    mkdir dir1 dir2 dir3
    
would create three directories named "dir1", "dir2", "dir3".

### cp - 复制文件和目录
The cp command copies files or directories. It can be used two different ways:

    cp item1 item2
    
to copy the single file or directory "item1" to file or directory "item2", and:

    cp item... directory

to copy multiple items (either files or directories) into a directory.

#### cp Options

- -a, --archive
- -i, --interactive
- -r, --recursive
- -u, --update
- -v, --verbose

#### cp Examples

    cp file1 file2
Copy file1 to file2. If file2 exists, it is overwritten with the contents of file1. If file2 does not exist, it is created.

    cp -i file1 file2
Same as above, except that if file2 exists, the user is prompted before it is overwritten.

    cp file1 file2 dir1
Copy file1 and file2 into directory dir1. dir1 must already exist.

    cp dir1/* dir2
Using a wildcard, all the files in dir1 are copied into dir2. dir2 must already exist.

    cp -r dir1 dir2
Copy the contents of directory dir1 to directory dir2. If directory dir2 does not exist, it is created and after the copy, will contain the same contents as directory dir1. If directory dir2 does exist, then directory dir1 (and its contents) will be copied into dir2.

### mv - 移动和重命名文件
The mv command performs both file moving and file renaming, depending on how it is used. In either case, the original filename no longer exists after the operation. 
mv is used in much the same way as cp:

    mv item1 item2
    
to move or rename file or directory "item1" to "item2" or:

    mv item... directory

to move one or more items from one directory to another.


mv shares many of the name options as cp:

- -i --interactive
- -u --update
- -v --verbose

#### mv Examples

    mv file1 file2
Move file1 to file2. If file2 exists, it is overwritten with the contents of files. If file2 does not exist, it is created. In either case, file1 ceases to exist.

    mv -i file1 file2
Same as above, except that if file2 exists, the user is prompted before it is overwritten.

    mv file1 file2 dir1
Move file1 and file2 into directory dir1. dir1 nust already exist.

    mv dir1 dir2
if directory dir2 does not exist, create directory dir2 and move the contents of directory dir1 into dir2 and delete directory dir1. if directory dir2 does exist, move directory dir1 (and its contents) into directory dir2.


### rm - 删除文件和目录

    rm item...

where "item" is one or more files or directories.

- -i, --interactive
- -r, --recursive
- -f, --force
- -v, --verbose

#### rm Examples

    rm file1
Delete file1 silently

    rm -i file1
Same as above, except that the user is prompted for confirmation before the deletion is performed.

    rm -r file1 dir1
Delete file1 and dir1 and its contents.

    rm -rf file1 dir1
Same as above, except that if either file1 or dir1 do not exist, rm will continue silently.
    
    
>Be Careful With rm!
Unix-like operating systems such as Linux do not have an un delete command. Once you delete something with rm, it's gone. Linux assumes you're smart and you know what you're doing.
Be particularly careful with wildcards. Consider this classic example. Let's say you want to delete just the HTML files in a directory. To do this, you type:

    rm *.html

which is correct, but if you accidentally place a space between the "*" and the ".html" like so:

    rm * .html

the rm command will delete all the files in the directory and then complain that there is no file called ".html".

**Here is a useful tip.** Whenever you use wildcards with rm (besides carefully checking your typing!), test the wildcard first with ls. This will let you see the files that will be deleted. Then press the up arrow key to recall the command and replace the ls with rm.


### ln - 创建链接

The ln command is used to create hard or symbolic links. It is used in one of two ways:

    ln file link
to create a hard link, and :

    ln -s item link
to create a symbolic link where "item" is either a file or a directory.

#### Hard link
Hard links are the original Unix way of creating links, compared to symbolic links, which are more modern. By default, every file has a single hard link that gives the file its name. When we create a hard link, we create an additional directory entry for a file. Hard links have two improtant limitations:

1. A hard link cannot reference a file outside its own file system. This means a link may not reference a file that is not on the same disk partition as the link itself.
2. A hard link may not reference a directory.

A hard link is indistinguishable from the file itself. Unlike a symbolic link, when you list a directory containing a hard link you will see no special indication of the link. When a hard link is deleted, the link is removed but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted. It is important to be aware of hard links because you might encounter them from time to time, but modern practice prefers symbolic links, which we will cover next.

#### Symbolic link
Symbolic links were created to overcome the limitations of hard links. Symbolic links work by creating a special type of file that contains a text pointer to the referenced file or directory. In this regard, they operate in much the same way as a Windows shortcut though of course, they perdate the Windows feature by many years;-)

A file pointed to by a symbolic link, and the symbolic link itself are largely indistinguishable from one another. For example, if you write something to the symbolic link, the referenced file is also written to. However, when you delete a symbolic link, only the link is deleted, not the file itself. If the file is deleted before the symbolic link, the link will continue to exist, but will point to nothing. In this case, the link is said to be broken. In many implementations, the ls command will display broken links in a distinguishing color, such as red, to reveal their presence.


**How to know two hard links point to the same file**
When thinking about hard links, it is helpful to imagine that files are made up of two parts: the data part containing the file's contents and the name parts that all refer to the same data part. The system assigns a chain of disk blocks to what is called an inode, which is then associated with the name part. Each hard link therefore refers to a specific inode containing the file's contents.

The ls command has a way to reveal this information. It is invoked with the "-i" option:
    
    ls -li

If two hard links share the same inode number, they are the same file.

Symbolic links were created to overcome the two disadvantages of hard links: hard links cannot span physical devices and hard links cannot reference directories, only files. Symbolic links are a special type of file that contains a text pointer to the target file or directory.

Creating symbolic links is similar to creating hard links:

    ln -s file-path link-name

When creating symbolic links, you can either use absolute pathnames or relative pathnames, as we did in out earlier example. Using relative pathnames is more desirable because it allows a directory containing symbolic links to be renamed and/or moved without breaking the links.

In addition to regular files, symbolic links can also reference directories.

One thing to remember about symbolic links is that most file operations are carried out on the link's target, not the link itself. rm is an exception. When you delete a link, it is the link that is deleted, not the target.


##Working With Commands

- type - Indicate how a command name is interpreted
- which - Display which executable program will be executed
- man - Display a command's manual page
- apropos - Display a list of appropriate commands
- info - Display a command's info entry
- whatis - Display a very brief description of a command
- alias - Creat an alias for a command

### What are "commands"?
A command can be one of four different things:

1. An executable program like all those files we saw in /usr/bin. Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in scripting languages such as the shell, perl, python, ruby, etc.
2. A command built into the shell itself. bash supports a number of commands internally called shell builtins. The cd command, for example, is a shell builtin.
3. A shell function. These are miniature shell scripts incorporated into the environment. We will cover configuring the environment and writing shell functions in later chapters, but for now, just be aware that they exist.
4. An alias. Commands that we can define ourselves, built from other commands.

### Identifying Commands
It is often useful to know exactly which of the four kinds of commands is being used and Linux provides a couple of ways to find out.

#### type
The type command is a shell builtin that display the kind of command the shell will execute, given a particular command name. It works like this:

    type command-name

####  which
Sometimes there is more than one version of an executable program installed on a system. While this is not very common on desktop systems, it's not unusual on large servers. To determine the exact location of a given executable, the which command is used:

    which ls
    -> /bin/ls

which only works for executable programs, not builtins nor aliases(aliases maybe ok?) that are substitutes for actual executable programs. When we try to use which on a shell builtin, for example, cd, we either get no response or an error message.

#### help
bash has a built-in help facility available for each of the shell builtins. To use it, type "help" followed by the name of the shell builtin. For example:

    help cd

#### --help
Many executable programs support a "--help" option that displays a description of the command's supported syntax and options. For example:

    mkdir --help

Some programs don't support the "--help" option, but try it anyway. Often it results in an error message that will reveal the same usage information.

#### man
Most executable programs intended for command line use provide a formal piece of documentation called a manual or man page. A special paging program called man is used to view them. It is used like this:

    man program-name
    
Man pages vary somewhat in format but generally contain a title, a synopsis of the command's syntax, a description of the command's purpose, and a listing and description of each of the command's options. Man pages, however, do not usually include examples, and are intended as a reference, not a tutorial.

On most Linux systems, man uses less to display the manual page, so all of the familiar less commands work while displaying the page.

The "manual" that man displays is broken into sections and not only covers user commands but also system administration commands, programing interfaces, file formats and more.

**Man Page Organization**

1. User commands
2. Programming interfaces kernel system calls
3. Programming interfaces to the C library
4. Special files such as device nodes and drivers
5. File formats
6. Games and amusements such as screen savers
7. Miscellaneous
8. System administration commands

Sometimes we need to look in a specific section of the manual to find what we are looking for. This is particularly true if we are looking for a file format that is also the name of a command.
Without specifying a section number, we will always get the first instance of a match, probably in section 1. To specify a section number, we use man like this:

    man section_number search_term

#### apropos 
It is also possible to search the list of man pages for possible matches based on a search term. It's very crude but sometimes helpful.
Here is an example of a search for man pages using search term "floppy":

    apropos floppy

The first field in each line of output is the name of the man page, the second field shows the section.
Note that the man command with the "-k" option performs the exact same function as apropos.

#### whatis
The whatis program displays the name and a one line description of a man page matching a specified keyword:

>The Most Brutal Man Page Of Them All
As we have seen, the manual pages supplied with Linux and other Unix-like systems are intended as reference documentation and not as tutorials. Many man pages are hard to read, but I think that the grand prize for difficulty has got to go to the man page for bash. It is very accurate and concise, as well as being extremely complete. So check it out if you dare and look forward to the day when you can read it and it all makes sense.

#### info
The GNU Project provides an alternative to man pages for their programs, called "info".
Info pages are hyperlinked much like web pages.

    info program_name

The info program reads info files, which are tree structured into individual nodes, each containing a single topic. Info files contain hyperlinks that can move you from node to node. A hyperlink can be identified by its leading asterisk, and is activated by placing the cursor upon it and pressing the enter key.

To invoke info, type "info" followed optionally by the name of a program.Below is a table of commands used to control the reader while displaying an info page:

- ? - Display command help
- PgUp or Backspace
- PgDn or Space
- n - Display the next node
- p - Display the previous node
- u - Display the parent node of the currently displayed node, usually a menu.
- Enter - Follow the hyperlink at the cursor location
- q - Quit

Most of the command line programs we have discussed so far are part of the GNU Project's "coreutils" package, so typing:

    info coreutils

will display a menu page with hyperlinks to each program contained in the coreutils package.

#### README and other documantation
Many software packages installed on your system have documentation files residingin the /usr/share/doc directory. Most of these are stored in plain text format and can be viewed with less. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a ".gz" extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless that will display the contents of gzip-compressed text files.


#### USE alias
>Trick: It's possible to put more than on command on a line by separating each command with a semicolon character.

    command1; command2; command3...
    
For example:

    cd /usr; ls; cd -
   
First we change directory to /usr then list the directory and finally return to the original directory(by using "cd -").

Now let's turn this sequence into a new command using alias. The first thing we have to do is dream up a name for our new command. Let's try "test". Before we do that, it would be a good idea to find out if the name "test" is already being used. To find out, we can use the type command:

    type test
    -> test is a shell builtin
    
The name "test" is already taken. Let's try "foo":

    type foo
    -> bash: type: foo: not found
    
"foo" is not taken. So let's create our alias:

    alias foo='cd /usr; ls; cd -'
    
Notice the structure of this command:

    alias name='string'

After the command "alias" we give alias a name followed immediately (no whitespace allowed) by an equals sign, followed immediately by a quoted string containing the meaning to be assigned to the name. After we define our alias, it can be used anywhere the shell would expect a command.

We can also use the type command again to see our alias:
    
    type foo
    -> foo is aliased to 'cd /usr; ls; cd -'
   
To remove an alias, the `unalias` command is used, like so:

    unalias foo
    
While we purposefully avoided naming our alias with an existing command name, it is not uncommon to do so. This is often done to apply a commonly desired option to each invocation of a common command. For instance, we saw earlier how the ls command is often aliased to add color support:

    type ls
    -> ls is aliased to 'ls --color=tty'
    
To see all the aliases defined in the environment, use the alias command without arguments.

There is one problem with defining aliases on the command line. They vanish when your shell session ends. In a later chapter, we will see how to add our own aliases to the files that establish the environment each time we log on.



## I/O redirection

The "I/O" stands for input/output and with this facility you can redirect the input and output of commands to and from files, as well as connect multiple commands together into powerful command pipelines.

To show off this facility, we will introduce the following commands:

- cat - Concatenate files
- sort - sort lines of text
- uniq - Report or omit repeated lines
- grep - Print lines matching a pattern
- wc - Print newline, word, and byte counts for each file
- head - Output the first part of a file
- tail - Output the last part of a file
- tee - Read from standard input and write to standard output and files

###Standard input, Standard output, Standard error

Many of the programs that we have used so far produce output of some kind. This output often consists of two types. First, we have the program's results; that is, the data the program is designed to produce, and second, we have status and error messages that tell us how the program is getting along. If we look at a command like ls, we can see that it displays its results and its error messages on the screen.

Keeping with the Unix theme of "everything is a file", programs such as ls actually send their results to a special file called standard output (often expressed as stdout) and their status messages to another file called standard error (stderr). By default, both standard output and standard error are linked to the screen and not saved into a disk file. In addition, many programs take input from a facility called standard input(stdin) which is, by default, attached to the keyboard.

I/O redirection allows us to change where output goes and where input comes from. Normally, output goes to the screen and input comes from the keyboard, but with I/O redirection, we can change that.

### Redefine standard output

I/O redirection allows us to redefine where standard output goes. To redirect standard output to another file besides the screen, we use the ">" redirection operator followed by the name of the file.
It's often useful to store the output of a command in a file. For example, we could tell the shell to send the output of the ls command to the file ls-output.txt instead of the screen:

    ls -l /usr/bin > ls-output.txt

Here, we created a long listing of the /usr/bin directory and sent the results to the file ls-output.txt. Let's examine the redirected output of the command:

    ls -l ls-output.txt
    
If we look at the file with less, we will see that the file ls-output.txt does indeed contain the results from our ls command:

    less ls-output.txt

Now, let's repeat out redirection test, but this time with a twist. We'll change the name of the directory to one that does not exist:

    ls -l /bin/usr > ls-output.txt
    -> ls: cannot access /bin/usr: No such file or directory
    
We received an error message. This makes sense since we specified the non-existent directory /bin/usr, but why was the error message displayed on the screen rather than being redirected to the file ls-output.txt? 
The answer is that the ls program does not send its error messages to standard output. Instead, like most well-writen Unix programs, it sends its error messages to standard error, the error message was still sent to the screen. 

We'll see how to redirect standard error in just a minute, but first, let's look at what happened to our output file:

    ls -l ls-output.txt

The file now has zero length! This is because, when we redirect output with the ">" redirection operator, the destination file is always rewritten from the beginning. Since our ls command generated no results and only an error message, the redirection operation started to rewrite the file and then stopped because of the error, resulting in its truncation. In fact, if we ever need to actually truncate a file(or create a new, empty file) we can use a trick like this:
 
    > ls-output.txt

Simply using the redirection operator with no command preceding it will truncate an existing file or create a new, empty file.

So, how can we append redirected output to a file instead of overwriting the file from the beginning?
For that, we use the ">>" redirection operator, like so:

    ls -l /usr/bin >> ls-output.txt
    ls -l /usr/bin >> ls-output.txt
    

### Redirecting standard error
Redirecting standard error lacks the ease of a dedicated redirection operator.
 To redirect standard error we must refer to its file descriptor. 
 A program can produce output on any of several numbered file streams. While we have referred to the first three of these dile steams as standard input, output and error, the shell references them internally as file descriptors zero, one, and two, respectively. The shell provides a notation for redirecting files using the file descriptor number. Since standard error is the same as file descriptor number two, we can redirect standard error with this notation.
 
    ls -l /bin/usr 2> ls-error.txt
    
The file descriptor "2" is placed immediately before the redirection operator to perform the redirection of standard error to the file ls-error.txt.


### Redirecting Standard output and standard error to the same file
There are cases in which we may wish to capture all of the output of a command to a single file. To do this, we must redirect both standard output and standard error at the same time.

    ls -l /bin/usr > ls-output.txt 2>&1
    
 Using this method, we perform two redirections. First we redirect standard output to the file ls-output.txt and then we redirect file descriptor two (standard error) to file descriptor on (standard output) using the notation 2>&1.
   
 Notice that the order of the redirections  is significant. The redirection of standard error must always occur after redirecting standard output or it doesn't work. 
 
 Recent versions of bash provide a second, more streamlined method for performing this combined redirection:
 
    ls -l /bin/usr &> ls-output.txt
    
In this example, we use the simple notation &> to redirect both standard output and standard error to the file ls-output.txt.



Sometimes "silence is golden", and we don't want output from a command, we just want to throw it away. This applies particularly to error and status messages. The system provides a way to do this by redirecting output to a special file called "/dev/null". This file is a system device called a bit bucket which accepts input and does nothing with it. To suppress error messages from a command, we do this:

    ls -l /bin/usr 2> /dev/null
    
>/dev/null in Unix Culture
The bit bucket in an ancient Unix concept and due to its universality, has appeared in many parts of Unix culture. When someone says he/she is sending your comments to /dev/null, now you know what it means.


### Redirecting standard input
Up to now, we haven't encountered any commands that make use of standard input(acturally we have, but we'll reveal that surprise a little bit later), so we need to introduce one.

### cat
The cat command reads one or more files and copies them to standard output like so:
    
    cat [file]

In most cases, you can think of cat as being analogous to the TYPE command in DOS. You can use it to display files without paging, for example:

    cat ls-output.txt

will display the contents of the file ls-output.txt. cat is often used to display short text files. Since cat can accept can accept more than one file as an argument, it can also be used to join files together. Say we have downloaded a large file that has been split into multiple parts (multimedia files are often split this way on USENET), and we want to join them back together. If the files were named:
movie.mpeg.001 movie.mpeg.002 ... movie.mpeg.009

we could join them back together with this command:

    cat movie.mpeg.0* > movie.mpeg

Since wildcards always expand in sorted order, the arguments will be arranged in the correct order.

This is all well and good, but what does this have to do with standard input? Nothing yet, but let's try something else. What happens if we type "cat" with no arguments:

    cat
    
Nothing happens, it just sits there like it's hung. It may seem that way, but it's really doing exactly what it's supposed to.

**If cat is not given any arguments, it reads from standard input and since standard input is by default, attached to the keyboard**, it's waiting for us to type something! Try this:

    cat
    The quick brown fox jumped over the lazy dog.
    
Next, type a Ctrl-d (i.e., hold down the Ctrl key and press "d") to tell cat that it has reached end of file(EOF) on standard input:

    cat
    The quick brown fox jumped over the lazy dog.
    The quick brown fox jumped over the lazy dog.
    
In the absence of filename arguments, cat copies standard input to standard output, so we see our line of text repeated. We can use this behavior to create short text files.

Let's say that we wanted to create a file called "lazy_dog.txt" containing the text in our example.

    cat > lazy_dog.txt
    The quick brown fox jumped over the lazy dog.
    
Type the command followed by the text we want in to place in the file. Remember to type Ctrl-d at the end. 
**Using the command line, we have implemented the world's dumbest word processor!**
To see our results, we can use cat to copy the file to stdout again.


Now that we know how cat accepts standard input, in addition to filename arguments, let's try redirecting standard input:
 
    cat < lazy_dog.txt
    The quick brown fox jumped over the lazy dog.

Using the "<" redirection operator, we change the source of standard input from the keyboard to the file lazy_dog.txt. We see that the result is the same as passing a single filename argument. This is not particularly useful compared to passing a filename argument, but is serves to demonstrate using a file as a source of standard input. Other commands make better use of standard input.

Before we move on, check out the man page for cat, as it has several interesting options.

### Pipeline
The ability of commands to read data from standard input and send to standard output is utilized by a shell feature called pipelines. Using the pipe operator "|" (vertical bar), **the standard output of one command can be piped into the standard input of another**:

    command1 | command2

For example, `less` can accepts standard input, we can use `less` to display the output of any command that sends its results to standard output:

    ls -l /usr/bin | less

This will use the output of `ls -l /usr/bin` as the input of `less`, then less will display the result.
Using this technique, we can conveniently examine the output of any command that produces standard output.

### filters
Pipelines are often used to perform complex operations on data. It is possible to put several commands together into a pipeline.
Frequently, the commands used this way are referred to as filters.
Filters take input, change it somehow and then output it. The first one we will try is sort. Imagine we wanted to make a combined list of all of the executable programs in /bin and /usr/bin, put them in sorted order and view it:

    ls /bin /usr/bin | sort | less

Since we specified two directories(/bin and /usr/bin), the output of ls would have consisted of two sorted lists, one for each directory. By including sort in our pipeline, we changed the data to produce a single, sorted list.

### uniq
The `uniq` command is often used in conjunction with sort. uniq accepts a sorted list of data from either standard input or a single filename argument (see the uniq man page for details) and, by default, removes any duplicates from the list.
So, to make sure our list has no duplicates (that is, any programs of the same name that appear in both the /bin and /usr/bin directories) we will add uniq to our pipeline:

    ls /bin /usr/bin | sort | uniq | less

If we want to see the list of duplicates instead, we add the "-d" option to uniq like so:

    ls /bin /usr/bin | sort | uniq -d | less

### wc - word count
The `wc` command is used to display the number of lines, words and bytes contained in files. For example:

    wc ls-output.txt
    -> 7902 64566 503634 ls-output.txt
 
In this case it prints out three numbers: lines, words, and bytes contained in ls-output.txt. Like our previous commands, if executed  without command line arguments, wc accepts standard input. The "-l" option limits its output to only report lines. Adding it to a pipeline is a handy way to count things. 
To see the number of programs we have in our sorted list, we can do this:
    
    ls /bin /usr/bin | sort | uniq | wc -l

### grep
`grep` is a powerful program used to find text patterns within files.
It's used like this:

    grep pattern [file...]

When grep encounters a "pattern" in the file, it prints out the lines containing it. The patterns that grep can match can be very complex, but for now, we will concentrate on simple text matches.

Let's say we want to find all the files in our list of programs that had the word "zip" embedded in the name. Such a search might give us an idea of some of the programs on our system that had something to do with file compression. 

    ls /bin /usr/bin | sort | uniq | grep zip

There are a couple of handy options for grep: "-i" which causes grep to ignore case when performing the search (normally searches are case sensitive) and "-v" which tells grep to only print lines that do not match the pattern.

### head/tail
Sometimes you may only want the first few lines or the last few lines of the output from a command. 
The `head` command prints the first ten lines of a file, and the `tail` command prints the last ten lines. You can adjust the number of lines with the "-n" option:

    head -n 5 ls-output.txt
    -> print out the first 5 lines of the ls-output.txt
    
    tail -n 3 ls-output.txt
    -> print the last 3 lines of the ls-output.txt

These can be used in pipelines as well:

    ls /usr/bin | tail -n 5
    -> print the first 5 lines of the ls command's output

`tail` has an option which allows you to view files in real-time. This is useful for watching the progress of log files as they are being written.

In the following example, we will look at the messages file in /var/log. Superuser privileges are required to do this on some Linux distributions, since the /var/log messages file may contain security information:

    tail -f /var/lgo/messages

Using the "-f" option, tail continues to monitor the file and when new lines are appended, they immediately appear on the display, until you type Ctrl-c.


### tee - 从stdin读取数据，同时输出到stdout和文件

The tee program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files. This is useful for capturing a pipeline's contents at an intermediate stage of processing.
 For example:
   
    ls /usr/bin | tee ls.txt | grep zip
    -> list the content at /usr/bin , output them to both ls.txt and standard output, use this as input for grep, and find sentence containing the keyword "zip".
    


As we gain Linux experience, we will see that the redirection feature of the command line is extremely useful for solving specialized problems.
There are many commands that make use of standard input and output, and almost all command line programs use standard error to display their informative messages.



## See world form shell 

- echo - Display a line of text


### Expansion
Each time you type a command line and press the enter key, bash performs several processes upon the text before it carries out your command.

We have seen a couple of cases of how a simple character sequence, for example "*", can have a lot of meaning to the shell. The process that makes this happen is called expansion.
With expansion, you type something and it is expanded into something else before the shell acts upon it. 

To demonstrate what we mean by this, let's take a look at the echo command. echo is a shell builtin that performs a very simple task. It prints out its text arguments on standard output:

    echo this is a test
    -> this is a test
 
That's pretty straightforward. Any argument passed to echo gets displayed.
Let's try another example:

    echo *
    -> Desktop Documents ls-output.txt Music Pictures Public Templates Videos


The shell expands the "*" into something else before the echo command is executed.
When the enter key is pressed, the shell automatically expands any qualifying characters on the command line before the command is carried out, so the echo command never saw the "*", only its expanded result. Knowing this,  we can see that echo behaved as expected.

### Pathname expansion

The mechanism by which wildcards work is called pathname expansion.

>Pathname Expansion of Hidden Files
As we know, filenames that begin with a period character are hidden. Pathname expansion also respects this behavior. 
An expansion such as:

    echo *

does not reveal hidden files.
what will happen if we add a period at start:

    echo .*

This will include hidden files, but also include directory "." and "..".
To correctly perform pathname expansion in this situation, we have to employ a more specific pattern. This will work correctly:

    echo .[!.]*

### tilde character
As you may recall from our introduction to the cd command, the tilde character("~") has a special meaning. When used at the beginning  of a word, it expands into the name of the home directory of the named user, or if no user is named, the home directory of the current user:

    echo ~
    -> /home/me
    
If user "foo" has an account, then:

    echo ~foo
    -> /home/foo



### arithmetic expansion 
The shell allows arithmetic to be performed by expansion.
This allow us to use the shell prompt as a calculator:

    echo $((2 + 2))
    -> 4

**Arithmetic expansion uses the form**:

    $((expression))

Where expression is an arithmetic expression consisting of values and arithmetic operators.

Arithmetic expansion only supports integers (whole numbers, no decimals), but can perform quite a number of different operations. Here are a few of the supported operators:

    + - * / % **(Exponentiation)

Spaces are not significant in arithmetic expressions and expressions may be nested. For example, to multiply five squared by three:

    echo $(($((5**2))*3))
    -> 75
    
Single parentheses may be used to group multiple subexpressions. With this technique, we can rewrite the example above and get the same result using a simgle expansion instead of two:

    echo $(((5**2)*3))
    -> 75
    
Here is an example using the division and remainder operators. Notice the effect of integer division:

    echo $((5/2))
    -> 2
    
here **can't** get the correct answer.


### brace expansion
Perhaps the strangest expansion is called brace expansion. With it, you can create **multiple text strings** from a pattern containing braces.
For example:

    echo Front-{A,B,C}-Back
    -> Front-A-Back Front-B-Back Front-C-Back
    
Patterns to be brace expanded may contain a leading portion called a preamble and a trailing portion called a postscript.
The brace expression itself may contain either a comma-separated list of strings, or a range of integers or single characters. The pattern may not contain embedded whitespace.

    echo Number_{1..5}
    -> Number_1 Number_2 Number_3 Number_4 Number_5

A range of letters in reverse order:

    echo {Z..A}
    -> Z Y X W V U T S R Q P O N M L K J I H G F E D C B A

Brace expansions may be nested:

    echo a{A{1,2},B{3,4}}b
    -> aA1b aA2b aB3b aB4b

What is this good for?
The most common application is to make lists of files or directories to be created.

For example, if we were photographers and had a large collection of images that we wanted to organize into years and months, we can do it this way:

    mkdir Pics
    cd Pics
    mkdir {2007..2009}-0{1..9} {2007..2009}-{10..12}
    ls
    
### parameter expansion
We're only going to touch briefly on parameter expansion in this chapter, but we'll be covering it extensively later. 

It's a feature that is more useful in shell script than directly on the command line. Many of its capabilities have to do with the system's ability to store small chunks of data and to give each chunk a name.
Many such chunks, more properly called variables, are available for your examination.
For example, the variable named "USER" contains your user name. To invoke parameter expansion and reveal the contents of USER you would do this:

    echo $USER
    ->yourusername
    
To see a list of available variables, try this :

    printenv | less

You may have noticed that with other types of expansion, if you mistype a pattern, the expansion will not take place and the echo command will simply display the mistyped pattern.


### Command substitution
Command substitution allows us to use the output of a command as an expansion:

    echo $(commandname)
    
for example:

    ls -l $(which cp)
    
Here we passed the result of `which cp` as an argument to the ls command, thereby getting the listing of  the cp program without having to know its full pathname.

We are not llimited to just simple commands, entire pipelines can be used:

    file $(ls /usr.bin.* | grep zip)
    
In this example, the results of the pipeline became the argument list of the file command.

There is an alternate syntax for command substitution in older shell programs which is also supported in bash. It uses back-quotes instead of the dollar sign and parentheses:

    ls -l `which cp`
   
    
### Quoting
Now we know how many ways the shell can perform expansions, it's time to learn how we can control it.

For example:

    echo this is a        test
    -> this is a test
    
word-splitting by the shell removed extra whitespace from the echo command's list of arguments.

    echo The total is $100.00
    -> The total is 00.00

parameter expansion substituted an empty string for the value of "$1" because it was an undefined variable.
The shell provides a mechanism called quoting to selectively suppress unwanted expansions.


#### double quote

If you place text inside double quotes, all the special characters used by the shell lose their special meaning and are treated as ordinary characters.
The exceptions are $,\(backslash),and `(back-quote).(参数展开、算数展开和命令替换依然能执行)

Using double quotes, we can cope with filenames containing embedded spaces.

By using double quotes, we stop the word-splitting and get the desired result; further, we can even repair the damage:

    ls -l "two words.txt"
    mv "two words.txt" two_words.txt
    

   
Remember, parameter expansion, arithmetic expansion, and command substitution still take place within double quotes:

    echo "$USER $((2+2)) $(cal)"


We should take a moment to look at the effect of double quotes on command substitution. First let's look a little deeper at how word splitting  works. 

By default, word-splitting looks for the presence of spaces, tabs, and newlines(linefeed characters) and treats them as delimiters between words. This means that unquoted spaces, tabs and newlines are not considered to be part of the text. They only serve as separators. Since they separate the words into different arguments, our example command line contains a command followed by four distinct arguments. If we add double quotes:

    echo "this is a   test"
    -> this is a   test

word-splitting is suppressed and embedded spaces are not treated as delimiters, rather they become part of the argument. Once the double quotes are added, our command line contains a command followed by a single argument.


The fact that newlines are considered delimiters by the word-splitting mechanism causes an interesting, albeit subtle, effect on command substitution.
Consider the following:

    echo $(cal)
    February 2008 Su Mo Tu We Th Fr Sa 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
    echo "$(cal)"
    February 2008
    ....

When you press the enter key, the text of input will expansion.
In the first instance, the unquoted command substitution resulted in a command line containing thirty-eight arguments.
In the second, a command line with one argument that includes the embedded spaces and newlines.


#### Single quotes
If we need to suppress all expansions, we use single quotes.


### escape character
Sometimes we only want to quote a single character, we can precede a chracter with a backslash, which in this context is called the escape character.
Often this is done inside double quotes to selectively prevent an expansion:

    echo "The balance for user $USER is: \$5.00"
    -> The balance for user me is: $5.00
    
It's also common to use escaping to eliminate the special meaning of a character in a filename. 
Note that within single quotes, the backslash loses its special meaning and is treated as an ordinary character.

>Backslash Escape Sequences
In addition to its role as the escape character, the backslash is also used as part of a notation to represent certain special characters called **control codes**.
The first thirty-two character in the ASCII coding scheme are used to transmit commands to teletype-like devices.
- \a Bell("Alert"-causes the computer to beep)
- \b Backspace
- \n Newline.
- \r Carriage return
- \t Tab
The idea behind this representation using the backslash originated in the C programming language and has been adopted by many others, including the shell.


### interpretation of escape 

Adding the "-e" option to echo will enable interpretation of escape sequences. You may also place them inside $''.

As we move forward with using the shell, we will find that expansions and quoting will be used with increasing frequency, so it makes sense to get a good understanding of the way they works.
Without a proper understanding of expansion, the shell will always be a source of mystery and confusion, and much of it potential power wasted.




## Keyboard

In this chapter, we will look at bash features that make keyboard use faster and more efficient.

- clear - Clear the screen
- history - Display the contents of the history list

### Cursor Movement Commands

- Ctrl-a : Move cursor to the beginning of the line.
- Ctrl-e : Move cursor to the end of the line.
- Ctrl-f : Move cursor forward one character; same as the right arrow key.
- Ctrl-b : Move cursor backward one character; same as the left arrow key.
- Alt-f : Move cursor forward one word.
- Alt-b : Move cursor backward one word.
- Ctrl-l : Clear the screen and move the cursor to the top left corner. The clear command does the same thing.

### Text Editing Commands

- Ctrl-d : Delete the character at the cursor location
- Ctrl-t : Transpose the character at the cursor location with the one preceding it.
- Alt-t : Transpose the word at the cursor location with the one preceding it.
- Alt-l : Convert the characters from the cursor location to the end of the word to lowercase.
- Alt-u : Convert the characters from the cursor location to the end of the word to uppercase.

### Cut And Paste Commands
>The Readline documentation uses the terms killing and yanking to refer to what we would commonly call cutting and pasting.

- Ctrl-k : Kill text from the cursor location to the end of line.
- Ctrl-u : Kill text from the cursor location to the beginning of the line.
- Alt-d : Kill text from the cursor location to the end of current word.
- Alt-Backspace : Kill text from the cursor location to the beginning of the word. If the cursor is at the beginning of a word, kill the previous word.
- Ctrl-y Yank text from the kill-ring and insert it at the current location.


>The Meta Key 

### completion
Completion occurs when you press the tab key while typing a command. 

completion will also work on variable (if the beginning of the word is a "$"), user names(if the word begins with "~"), commands(if the word is the first word on the line) and host names(if the beginning of the word is "@"). Host name completion only works for host names listed in /etc/hosts.

There are



### linux文件扩展名
linux文件的扩展名只展示文件可能的用途。  
文件是否可以执行，在于其“x”属性（但不代表一定执行成功）。  
> 网上下载的可执行文件，有可能在linux系统中无法执行，这可能是因为文件属性被改变。

### linux文件长度限制
- 单一文件或目录最长文件名：255字符
- 完整路径名称：4096字符

###linux文件名的限制
避免使用特殊字符，例如：*?<>;&![]|\'"`(){}  
因为这些符号在命令行界面下有特殊含义。例如文件名以小数点开头代表隐藏文件。  
同时，由于命令执行当中，常会用到-option之类的参数，因此最好也避免将文件名开头以-或+来命名。

##linux目录配置
###linux目录配置标准：FHS

| | 可分享的(shareable)| 不可分享的(unshareable)|
|:---:|:---:|:---:|
| - 不变的（static） | /usr(软件放置) | /etc（配置文件） |
| | /opt（第三方软件） | /boot（开机与内核文件） |
| - 可变的（variable） | /var/mail（用户邮件信箱） | /var/run（程序相关） |
| | /var/spool/news（新闻组） | /var/lock（程序相关） |

FHS针对目录树架构，仅定义出**三层目录**下应该放什么数据：

- / （root，根目录）：与开机系统有关；
- /usr （UNIX software resource）：与软件安装/执行有关；
- /var （variable）：与系统运作过程有关。

####根目录
根目录下，应该有以下子目录：

- /bin：单用户维护模式下还能操作的命令。主要有：cat，chmod，chown，date，mv，mkdir，cp，bash等常用命令。
- /boot：开机使用的文件。包括Linux内核文件、开机菜单、开机所需配置文件等。
- /dev：设备与设备接口都以文件形式存在于此。访问这个目录下的某个文件，就等于访问某个设备。
- /etc：系统主要配置文件。例如账号密码、各种服务的起始文件等。可以让一般用户查阅，但只有root可以修改。建议不要放置可执行文件在这个目录。
- /home：系统默认用户主文件夹。
- /lib：开机时会用到的函数库。
- /media：可删除的设备。包括软盘、光盘、DVD等。
- /mnt：暂时挂载额外设备时使用。
- /opt：第三方软件的放置目录。
- /root：系统管理员的主文件夹。
- /sbin：开机、修复、还原系统所需要的命令。
- /srv：网络服务启动后，所需要取用的数据目录。
- /tmp：一般用户或者正在执行的程序暂时放置文件的地方。需要定期清理。

因为根目录与开机有关，开机过程中仅有根目录会被挂载，因此根目录下与开机过程有关的目录不能放到与根目录不同的分区。
不能与根目录分开的目录：

- /etc：配置文件
- /bin：重要执行文件
- /dev：所需要的设备文件
- /lib：执行文件所需的函数库与内核所需的模块
- /sbin：重要的系统执行文件
这五个目录不可与根目录分开。

#### /usr

放置“UNIX Software Resource”（UNIX操作系统软件资源）的目录。
FHS建议所有软件开发者应该将他们的数据合理的分别放置到这个目录下的子目录。
所有系统默认的软件都会放置到/usr下，建议子目录：

- /usr/X11R6/：X Window系统重要数据的目录
- /usr/bin/：绝大部分用户可使用的命令放在这里。它与/bin不同（是否与开机过程有关）。
- /usr/include/：C/C++等程序语言的头文件和包含文件放置处
- /usr/lib/：各应用软件的函数库、目标文件（object file），以及不被一般用户惯用的执行文件或脚本。某些软件会提供一些特殊的命令来进行服务器的设置，这些命令也不会经常被系统管理员操作，那就会被摆放到这个目录下。注意，如果使用X86_64的linux系统，可能会有/usr/lib64/目录产生。
- /usr/local/：系统管理员在本机自行安装自己下载的软件，建议安装在此目录，便于管理。
- /usr/sbin/：非必需系统命令。例如某些网络服务器软件的服务命令。
- /usr/share/：放置共享文件。这个目录下的数据几乎不分硬件架构均可读取（基本都是文本文件）。此目录下常见子目录：/usr/share/man（在线帮助文件），/usr/share/doc（软件文件说明），/usr/share/zoneinfo（时区文件）
- /usr/src/：一般源码放置于此。内核源码则建议放在/usr/src/linux/目录下。


#### /var
/var 目录主要针对常态性变动的文件，包括缓存（cache）、登录文件（logfile）以及某些软件运行所产生的文件，包括程序文件（lock file，run file），或者例如MySQL数据库的文件等。常见子目录：

- /var/cache/：应用程序运行时产生的缓存文件
- /var/lib/：程序执行时，需要使用到的数据文件放置的目录。各自软件应该有各自的目录。例如MySQL的数据库放置到/var/lib/mysql/。
- /var/lock/：某些设备或者文件资源一次只能被一个应用程序使用，如果同时有两个程序使用该设备则会出错，因此需要将该设备锁定，确保该设备只会给单一软件使用。
- /var/log/：登录文件的目录。
- /var/mail/：个人电子邮件信箱的目录。
- /var/run/：某些程序或者服务启动后，会将它们的PID放置在这个目录下。
- /var/spool/：放置一些队列数据（排队等待其他程序使用的数据），通常使用后会被删除。


#### 一些重要的目录：

- /lost+found：使用标准的ext2/ext3文件系统格式才会产生的目录，当文件系统发生错误时，将一些丢失的片段放置到这个目录下。
- /proc：这个目录是个虚拟文件系统，数据都在内存中，例如系统内核、进程、外部设备的状态及网络状态等。
- /sys：也是个虚拟文件系统，主要也是记录与内核有关的信息，包括目前已加载的内核模块与内核检测到的硬件设备信息等。



### 目录树（directory tree）


### 查看系统信息：
lsb_release: print distribution-specific information





# 7 linux文件与目录管理
## 目录与路径
切换目录的相关命令和符号：
###命令
- cd：切换目录。（Change Directory）。只输入“cd”的话，与输入“cd ~”一样回到当前用户主文件夹
- pwd：显示当前目录。
- mkdir:新建一个新的目录。默认情况下需要逐层创建，若加上参数-p，则可以直接创建多层目录。通过参数-m可以设置目录权限。
- rmdir：删除一个空的目录。若要删除多层空目录，可加参数-p。

###特殊目录符号

- .：此层目录
- ..：上一层目录
- \-：前一个工作目录
- ~：“当前用户身份”所在的主文件夹
- ~account：代表account这个用户的主文件夹

>根目录下也有"."和".."两个目录，不过完全一样。即根目录的上一层目录等同于根目录本身。

### 执行文件路径的变量：$PATH

环境变脸PATH，会包含一系列目录，当你执行一个命令时，系统会依照PATH设置的路径去逐步查找相应文件名的可执行文件。如果有多个同名文件，先查询到的同名命令先被执行。

>执行echo $PATH，会显示出当前的PATH路径。

两种方式可以执行可执行文件的命令：

- 执行文件在PATH路径里，直接输入文件名即可执行。
- 输入文件的绝对路径或相对路径来执行。

>如果可执行文件不在PATH路径里，即使在当前目录里，也无法通过输入文件名来执行。
>此时，可以通过绝对路径或相对路径来执行；也可以选择将该文件所在目录加入到PATH里。
将指定目录添加到PATH:

    PATH="$PATH":/root


- 不同身份用户默认的PATH不同，默认能够随意执行的命令也不同。
- PATH是可以修改的，一般用户可以通过修改PATH来执行某些位于/sbin或/usr/sbin下的命令来查询。
- 使用绝对路径或相对路径直接指定某个命令的文件名来执行，会比查询PATH要更正确。
- 命令应该要放置到正确的目录下，执行才会比较方便。
- 本目录（.）最好不要放到PATH中。


## 文件与目录管理
shared drive
####查看：ls
常用参数：-adlF

####复制：cp
常用参数：-air

由于cp有种种的文件属性和权限特性，所以，在复制时需要了解到：

- 是否需要完整保留来源文件的信息？
- 源文件是否为软链接文件？
- 源文件是否为特殊的文件？
- 源文件是否为目录？

####删除：rm
常用参数：
-i：删除前询问
-f：忽略不存在的文件，不出现警告信息
-r：递归删除，用在目录的删除，属于危险操作！！！

####移动：mv
常用

