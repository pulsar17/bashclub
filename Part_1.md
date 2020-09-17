# Part 1 - What can you do with BASH/Linux?

Here I talk about **5 Useless things** that you could do in BASH. Why? coz it's fun! Although at the end I show you a very useful thing that illustrates the power of the command line.  
At this stage you probably won't be able to understand how that 'thing' works but by the end of this series you will be able to do such complex 'things' by yourself. You'll be creating more of such complex 'things'. So, hold on as we start our journey together.

### The 5 things would be:
1. Let the cow talk. Maybe it'll say hi.
~~~bash
cowsay "hi"
~~~
2. A 'beautiful' ASCII art of an image.
~~~bash
asciiview <the-image>
~~~
3. Star Wars! 
~~~bash
telnet towel.blinkenlights.nl
~~~ 
4. Nothing more lol than this. Rainbowifies the text 
~~~bash
lolcat
~~~
5. Makes you think - are we living in the Matrix?
~~~bash
cmatrix
~~~

### One kinda useful 
~~~bash
echo "Wow! espeak is a good tool and it has got a robotic voice too" | espeak
~~~ 
Pipe anything to espeak and it will speak for you. Cool! Isn't it?

### The Useful One
This command is a glimpse of what you can actually do using the command line:

~~~
sudo dd if=/dev/sda bs=1M conv=sync,noerror status=progress | gzip -c | ssh username@remote_machine 'cat > backup.tar.gz'
~~~
It creates a remote backup of a local hard drive partition, but it compresses it along the way. The sheer power of command line can be seen here. Individual simple commands which are good at their job composed to do a complex job.

## Next Part Of the Series
Next part would be about various basic commands like ``ls, cat, mkdir`` and some shortcuts related to them that might come in handy.




