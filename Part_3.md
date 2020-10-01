# Part 3 - Files and Permissions
Linux follows a philoshphy - 'Everything is a file' - which it inherits from UNIX. So really anything - even your webcam is a file as far as Linux  is considered.  
To be more precise, everything is a 'stream of bytes' in Linux.  
  
## Check out your 🏠
This job can be served by the `ls` command. Use the`-l` option to see long listing of files. The first column of this listing is what we're interested in. Let's do that for our home directory.    
Whenever you login to your shell or you open the terminal, you are by default in your home directory which is generally `/home/username/`.
```bash
ls -l 
# I could also do ls -l /home/pulsar17/

#Truncated Output
...
-rw-------  1 pulsar17 pulsar17       240 Sep 29 01:37  2020-09-28-20-07-50.029-VBoxSVC-7386.log
drwxr-xr-x  7 pulsar17 pulsar17      4096 Jan 13  2020  afrost-website
drwxr-xr-x 12 pulsar17 pulsar17      4096 Nov 18  2019  Akira
drwxr-xr-x  3 pulsar17 pulsar17      4096 Jan 12  2020  Android
...
```
Focus on the `1st` column. It has space for 10 'things'. The 1st character tells you about the type of the file. The 9 characters after it are the 9-bit permission model that Linux follows **for every file**.

## The various types of files are:
- **A Normal file** - These 'files' would have a `-` in the 1st character of listing. These can be images, audio files, videos, executables, etc.
- **Directories** - These 'files' would have a `d` in the 1st character of listing. (To see the information about a directory and not its contents, add the `-d`  option to ls - ```ls -ld thedirectory```).
- **Block files** - These 'files' would have a `b` in the 1st character of listing. These are hardware files and these are generally how you interface with your SSDs and HDDs. 
- **Links** - These 'files' would have an `l` in the 1st character of listing. Links point to other files in the filesystem.
- **Character files** - These 'files' would have a `c` in the 1st character of the listing. These are your terminals. You would find these files along with block files in `/dev` directory.
- **Sockets** - These 'files' would have an `s` in the 1st character of the listing. These are used for communication between various applications. Honestly, I've never used these files. Maybe I have but indirectly. (They're there for a reason? 🤷‍♂️)
- **Pipes** - These 'files' would have `p` in the 1st character of the listing. These are related to the `|` pipe operator in Linux but they're accessible as a file. These files are 'named pipes'.

Phewww 😌. So many file types but, but, they're all accessible by a single `read()` syscall.
Having '**everything is a file**' greatly simplifies the world for us in the Linux land.

## Not Allowed, Sir 🕴
The 9 bit permission model has its roots in UNIX. Though not perfect, it is ubiquitous. Every file in Linux has an `owner` and a `group`. Everyone who is not the owner and not in the group is `others`/`everyone else in the world`.   

The `9` bits are a combination of group of `3` bits:
| User (Owner) | Group | Other |
|---|---|---|
| `r` `w` `x`| `r` `w` `x`| `r` `w` `x`|

`r` - read  
`w` - write  
`x` - execute  

Lets's add divisions to a listing of a file `me.png`

```
ls -l me.png

#Output
- | rw- | rw- | r-- | ...
```
The permission bits give the following information:
- It's a normal file.
- Nobody can execute this file. (Why would you? It's a `.png` file)
- The owner and the group can read and write to the file. (can also delete it)
- Others can only read the file. Not allowed to write to the file 😢. Unfair isn't it? That is life 😌.

## You can change it all (if you own it)
Only the owner and the `root` user are allowed to change the permissions of a file. Use the `chmod ` command ( I pronounce it as [chuh][mode])  
Let's :  
```
#give everyone every permission to `me.png`
chmod a+rwx me.png

#then take read permission from others 
chmod o-r me.png

#then take read permission from group
chmod g-r me.png

#then take write permission from owner
chmod u-w me.png

#Finally list the permssions
ls -l me.png

#Output
-r-x-wx-wx 1 pulsar17 pulsar17 8357662 Aug 23 18:42 me.png

```

`chgrp` command changes the group of a file.
Try `man chgrp` to see how it's done.

## Extended Permissions
(I should totally refrain from talking about them.)
Anyways, these are in addition to traditional 9 bit permissions.
These are:
- `setuid bit` - Allows other users to execute files as the `owner`.
- `setgid bit` - Files and directories created in a directory with  `setgid bit` set will inherit the group rather than group of the creating user.
- `sticky bit` - For directories so that users don't delete each other's files. Try `ls /tmp`. You'll see a `t` at the end of the permission instead of `x`.

## Even more extended permissions
These provide more granular control and will include `ACLs` and `SELinux`. 

## Exercise
Do `man chmod` to see another way of specifying permissions (**Hint**: it will be like 0777 or 666). Also see how extended permissions can be set. (I couldn't use them doesn't mean you won't be able to 😌)

# Next Part of the Series
Next session would be all about pipes in Linux. - one of the most powerful thing you have at your command.
