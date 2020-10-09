## Pipes In Linux
Look at the output of this command 
```bash
cat timetraveldiaries.txt | grep doctor
```
If you closely notice there are two commands `cat` and `grep` connected by a `|` - famous as the pipe character.  
Now let's try to figure out what's going on here. Look at the parts separately (You could try running 1. and 3. separately)
1. `cat timetraveldiaries.txt` - This will print 🖨️ out the file on your terminal. Pretty trivial, right?😌. What you should know that `cat` actually prints to `stdout` - the standard output.  
The `stdout` of `cat` happens to be attached to the terminal we're working on. In another case, it could have been 'something else'.
1. `|` - Well, it's the pipe character. Hold on for a bit to know what it does 😌.
2. `grep doctor` - If you run this command separately, you'll see nothing happens. Why's that? `grep` If not given a file reads from `stdin` - the standard input and searches for the search term - in our case `doctor`.  
We did not give a file. So, `grep` searches `doctor` in `stdin`. Type `I am doing fine but I am not the Dr.` Press Enter. Nothing Happens.
Now type `I am doing fine and I am the doctor`. Now it higlights `doctor`. To exit press `Ctrl + D`.

Now that we know that how individual pieces work (except the `|` character), we are ready to understand how the whole thing works.
It will be useful to visualize pipe as this:
```bash
cat timetraveldiaries.txt >===< grep doctor
```
`|` connects the `stdout` of `cat` to `stdin` of `grep`
The `cat` command dumps the content of file on it's `stdout` which is also the `stdin` of `grep` now. 
`grep` reads from it's `stdin` like it normally does and searches `doctor` for us.

This whole thing has the effect of searching `doctor` in the file `timetraveldiaries.txt`

This attachment of `stdin` of one command to `stdout` of another is taken care of by the kernel and we as a user don't need to concern ourselves.

## More examples
I couldn't think of examples. So I used `|` to search for `|` character in my history 😇.

```bash
history | grep '|'
```
Remember `ls`? To know the most recent file in current directory you could do
```bash
ls -ltr | tail -1
```
To help with the thought process when using pipes, I'll walk you through an example:

### Suppose I wanted to know the 5 most recent commands that I typed on the terminal that used `|` character.
1. What I need first is my history 😌. ` history` command takes care of that.
2. Then I need to somehow filter commands that had `|` character in them. If I am able to do that, I can get any number of commands that had `|` let alone 5.
3. `history` is good and I know I can search or filter using `grep` but how do I connect them? Any guesses?😁 
4. `|` is a connector - a tool for composition of separate tools. I use it like I did in an above example:
```bash
history | grep '|'
```
This gives me each command(or group of commands really since pipe was used) that had `|` in them.  

5. Now I somehow need to get only the **last** 5 lines from this.
`tail` command does exactly that.
I have the commands with `|` and I know `tail -5` will get me the last 5 lines but how do I connect them? Again, pipes!
6. Finally, I would type 
```bash
history | grep '|' | tail -5
```
Yes, you can pipe any number of times. Think of left side of a pipe as a single unit. Every time you pipe, you should be closer to what you want.

## A suggestion/warning
When working with pipes, if the commands that are used with them go along well, you'll get the desired results.
By going along I mean they work on atleast some similar kind of data - line based data, column based data. This totally depends on the command. A line based could go well with column based. Again, depends on the commands.  
I was sure that the last 5 lines of `history | grep '|'` would give me 'recent' commands because I knew how `history` prints the history.

## Taking it further
At the cost of  sounding too complicated, and it can be done, what you could do is **run** the last command that contained `|` character. Since I need only the most recent command, I use `tail -1` instead of `tail -5`.
```bash
history | grep '|' | tail -1
```
At this stage we know we have the most recent command that contains `|` but it's only a history entry which looks something like:
```bash
1988  ls -ltr | tail -1
```
How do I execute it? Well if you want to execute a command you can pipe it to `bash` command. You could say something like this:
```bash
 history | grep '|' | tail -1 | bash
```
But notice that the output also contains  `1988` . Bash will complain as `1988` is not a command. We need filtering! And this time `grep`  won't do as we need to 'extract' something and not search it.  
`sed` comes to rescue here.
```bash
 history | grep '|' | tail -1 | sed 's/^[ ]*[0-9]*[ ]*//g' | bash
``` 
Don't get intimidated by this long command. Also once you know `sed` then after a little bit of searching, you can figure out how to get everything except the 1st field (I did it by searching 😌).  
You then simply pass *everything except the 1st field* to `bash`.
> **Note:** You need that extra leading space if you pipe this command to bash. It's because the command is itself written to history before completing. So without a leading space this command will end up executing itself. **Commands with a leading space are not written to history.**

This was one way of doing it. You may find your own using different commands. 😇

# Excercise
Learn about `awk` and `cut`. You can achieve similar filtering through them like the `sed` command. Check [this StackOverflow answer](https://stackoverflow.com/questions/7110119/bash-history-without-line-numbers) to see how other people have achieved filtering.