# unix-linux-basics
A repo to document some basics in Unix/Linux scripting 

## ls 

Example: isting all directories in current working drive by name

Say I have to directories in my current drive named Folder1 and Folder2, I can list all the directories with the name ```Folder``` with ```ls``` and directory flag ```-d```

```shell
$ ls -d Folder

Folder1/ Folder2/ 
```

Example: listing all directories in current working drive

In this example I have directories named Folder1, Folder2, Stuff, and Things. I can list only the directories in my current directory by using ```ls``` and flag ```-d``` like before, but now use the wildcard ```*``` with ```/``` (directory indicator). 

```shell
$ ls -d */

Folder1/ Folder2/ Stuff/ Things/
```

---

Example: find all file names using wildcard recursively in directories from current directory

```shell
$ find . -name "*.ipynb"

./MSU_Dynamics/MSU Dynamics Lab_Student_Introduction.ipynb
./MSU_Dynamics/MSU_Dynamics_Lab_Data.ipynb
./python_class_example.ipynb
```

## echo

Simple printing to the console with ```echo```

In the terminal:
```shell
$ echo Hello World!

Hello World!
```

```shell
$ echo Hello    World!

Hello World! # No extra spaces!
```

```shell
$ echo "Hello   World"'!' # Extra spaces (note the need for '!')

Hello   World!
```

---

## % Symbol with variables

When the percent sign (%) is used in the pattern ${variable%substring}, it will return content of the variable with the shortest occurrence of substring deleted from the back of the variable.

This quick example will strip the extension off a sample ```csv``` file:
```shell
$ f = file1.csv 
$ echo "${f%.csv}"

file1
```
---

## Subset of strings based off a deliminater

Use ```cut``` command to cut a string based off a specific deliminater

For example let's make a string ```this is a string```. We can run ```cut``` with the fdeliminater lag ```-d``` for which to cut the string based off. This will chop the string into the number of substrings between the deliminater. In this example, there will be 3 spaces and thus 4 substrings:
<ol>
<li>this</li>
<li>is</li>
<li>a</li>
<li>string</li>
</ol>

The use the ```-f``` flag will grab the number issued to the substring. So ```-f4``` will grab the fourth substring ```string```

```shell
$ STR="this is a string"
$ echo "$STR" | cut -d' ' -f4

string
```

The above code snippet just printed the substring to the console, but let's assign it to a variable:

```shell
$ STR="this is a string"
$ var="$(cut -d' ' -f 4 <<< $STR)"
$ echo "$var"

string
```

In this code snippet, ```var``` will be the variable name and the trailing ```<<<``` before ```$STR``` does the actual assigning of substring to ```var```.

---

## Simple renaming of single file

Using ```mv``` to rename a single file. ```mv``` then ```original file name``` then ```new file name```

```shell
$ mv file.txt file_rename.txt
```

---

## Operators

There are several operators in the shell:

<ul>
    <li>Arithmetic Operators</li>
    <li>Relational Operators</li>
    <li>Boolean Operators</li>
    <li>String Operators</li>
    <li>File Test Operators</li>
</ul>

---

## Loops

<u>
    <li>The while loop</li>
    <li>The for loop</li>
    <li>The until loop</li>
    <li>The select loop</li>
</ul>

#### while-loop

Example: print out numbers 0-9

```shell
$ var=0 # initiate var to 0

$ while [ $var -lt 10 ] # terms to loop over
> do
>   echo $var # print value of var
>   var=`expr $var + 1` # update var by adding 1 
> done

0
1
2
3
4
5
6
7
8
9

```

#### for-loop

Example: print names of all ```.sh``` files in directory named Shell that start with rename

```shell
FILES=Shell/rename*.sh
$ for f in $FILES
$ do
>   echo $f
> done

Shell/rename_multi.sh
Shell/rename_multi_better.sh
Shell/rename_multi_cut.sh
```

#### until-loop

Example: 

#### select-loop



---

## Metacharacters

Cetain characters in the Shell have special meaning and will result in the script to terminate with out being addressed. Adding a backslash ```\``` before the special character will pass it.

Example: the string "Hello; World"

* ```;``` is a special character that expects the following information to be a separate script command:

```shell
$ echo Hello; World

-bash: World: command not found
```

The script ends after the ```;``` and then it tries to interpret the command ```World``` to no avail (unless it is set somewhere else).

Corrected:

```shell
$ echo Hello\; World

Hello; World
```

Example: ```$``` character

```shell
$ echo "He gave me $2500!"

He gave me $500!
```

---

## Grep

A very useful tool in shell scripting is ```grep```. 

The grep filter searches a file for a particular pattern of characters, and displays all lines that contain that pattern. The pattern that is searched in the file is referred to as the regular expression (grep stands for globally search for regular expression and print out).


---

## Sed

Another handy tool is ```sed```. 

The sed command allows for searching text within files, finding and replacing text, and insertion or deletion of text in files as well. 

Example: say there exists a file ```file.txt``` with one line consisting of:

```
Hellow Wolrd1
```

Obviously there are some typos here, but sed can quickly show changes:

```shell
$ sed 's/Hellow Wolrd1/Hello World!/' file.txt

Hello World!
```

* Note, this command only <strong><em>prints</em></strong> out to the screen what the changes would do, but it doesn't actually <strong><em>change</em></strong> the file.

There are two simple ways of saving the changes:

<ol>
<li>Change the contents and save to the original file</li>

To change the file in place, the flag ```-i``` needs to be run 

* Note, for macos ```sed``` there needs to be an additional ```''``` after the ```-i```:

```shell
$ sed -i '' 's/Hellow Wolrd1/Hello World!/' file.txt
```

<li>Change the contents and save to different file</li>

Save changes to new file (file2.txt) and keep unchanged contents of the original file (file.txt)

```shell
$ sed 's/Hellow Wolrd1/Hello World!/' file.txt > file2.txt
```

</ol>

More about ```sed``` here: https://github.com/MethaneRain/unix-linux-basics/blob/master/sed.md

---

## Cat

The ```cat``` (concatenate) command reads data from the file and gives the content as output. This allows the user to create, view, and concatenate files.

Example: grab details of a simple shell script for getting info on netCDF files using ```ncdunmp``` that takes a cmd line argument for path to files

```shell
$ cat ncdump_mulitple_files.sh

#!/bin/sh

# Quick script to grab headers using ncdump for all netCDF files in specified
# path given as a cmd argument

#path=/path/to/files/*.nc
path=${1}*.nc

# allow script to run if no netCDF files are present
# nothing will display if no files are present
shopt -s nullglob

# for-loop over .nc files in path
for f in $path
do
  ncdump -h $f
done

```

Example: getting details of multiple files

```shell
$ cat hellowrold.sh var.sh

#!/bin/sh
# This is a comment!
echo "Hello      World"       # This is a comment, too!
echo "Hello World"
echo "Hello * World"
echo Hello * World
echo Hello      World
echo "Hello" World
echo Hello "     " World
echo "Hello "*" World"
echo `hello` world
echo 'hello' world
#!/bin/sh
my_var="My first variable script"
echo $my_var
```

Example: printing out details like before, but now with line numbers using the flag ```-n```

```shel
$ cat -n helloworld.sh

 1	#!/bin/sh
 2	# This is a comment!
 3	echo "Hello      World"       # This is a comment, too!
 4	echo "Hello World"
 5	echo "Hello * World"
 6	echo Hello * World
 7	echo Hello      World
 8	echo "Hello" World
 9	echo Hello "     " World
 10	echo "Hello "*" World"
 11	echo `hello` world
 12	echo 'hello' world

```

For more basic info check out: https://github.com/MethaneRain/unix-linux-basics/blob/master/cat.md

---

## Functions

```shell
isLeap()
{
	year=$1
	if [ $(( $year % 4 )) -eq 0 ]; then
		if [ $(( $year % 100 )) -eq 0 ]; then
			if [ $(( $year % 400 )) -eq 0 ]; then
				return 1
			else
				return 0
			fi
		else
			return 0
		fi
	fi
}

# Leap year
# No: 1800, 1900, 2100, 2200, 2300, 2500 
# Yes: 2000, 2400

for year in $@
do
	isLeap $year
	retval=$?
	if [ $retval -eq 0 ]; then
		echo "$year : No"
	else
		echo "$year : Yes"
	fi
done
```

---

## Pipe Command

In shell scripting there exists a handy tool called the pipe command ```|``` that allows the output of one command to be the input of another.

Example: use ```cat``` and ```head``` to read a file and print out the first 3 lines

```shell
$ cat helloworld.sh | head -3 

#!/bin/sh
# This is a comment!
echo "Hello      World"       # This is a comment, too!
```

Normally ```cat helloworld.sh``` would print the whole file and ```head -3 helloworld.sh``` would print out the first three lines. This is an overly simple example but still shows the value of the ```|``` command.

Example: 