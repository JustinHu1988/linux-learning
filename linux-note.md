
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

