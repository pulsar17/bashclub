# The Basic Commands ( 101 )
Because Hello World! is necessary. 😌
```bash
echo "Hello World!"
```
To change into ```world``` directory
```bash
cd ./world
```
> Note: There are two types of path you may specify - relative and absolute. The path given here as an argument to cd is a relative path. 
> Absolute paths start with a '```/```', the root of the Linux filesystem. An example would be ```/home/pulsar17/world```.  
> '```.```' is an alias to the current directory.

List it all (in the current directory)
```bash
ls .
```
List and give me more info about the contents of current directory (```-l```) but give me most recent files at the bottom (```-tr```)
```bash
ls -ltr .
```
Rename ```DoctorWho2009.file``` to ```DoctorWho2020.file```
```bash
mv DoctorWho2009.file DoctorWho2020.file
```
> Note: For it to work you need to be in the directory that contains DoctorWho2009.file. Also there is no ```rename``` command as such. Apart from renaming files ```mv``` is also used to move files as its name suggests.

Copy ```veryimportantfile.file``` to ```evenmoreimportantfile.file``` (Why do that? You might think that 'very' important things are also 'even more' important things. Prioritise 😌 (Imagine Stonks Man meme))
```bash
cp veryimportantfile.file evenmoreimportantfile.file
```

Create files and directories
- Touching is fine? 🤷‍♂️
```bash
touch thisisanewfile.txt
```
- The Directory Creator
```bash
mkdir thisisanewdir anotherdir yetanotherdir "A Single Dir"
```
To include spaces in an argument enclose the argument in double quotes ```" "```.
> Note: Spaces in names of files and directories are not recommended. Use '```_```' or '```-```' instead.

Remove files and directories
```bash
rm file_to_remove
```
**Caution!** ```rm``` won't ask you whether you want to delete a file or not. Be extra careful with directories.
To remove a directory, type:
```bash
rm -rf dir_to_remove
```
Know your Local IP Address
```bash
ip a #You need to look for the IP Address as it outputs much more info
```
Know your Public IP Address
```bash
curl ifconfig.me ; echo
```
Help will be given to those who ~~deserve~~ need it.
```bash
man ls
```
```man``` presents a manual for the command given as argument. It is quite useful and a life-saver when not connected to internet.

## Exercise
Type
```bash
man man
``` 
Get acquainted with reading a man page.   
Look for the various sections numbered 1,2,3, ...  
Then look at the top left corner of the man page of any command.  
Example - ```man(1)```

## Next Part Of the Series
Next part would be about files, users, permissions and introduction to pipes (```|```) in Linux.




