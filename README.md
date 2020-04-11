# unix-linux-basics
A repo to document some basics in Unix/Linux scripting 

## Listing all directories in current working drive by name

Say I have to directories in my current drive named Folder1 and Folder2, I can list all the directories with the name ```Folder``` with ```ls``` and directory flag ```-d```

```shell
$ ls -d Folder

Folder1/ Folder2/ 
```

---

## Listing all directories in current working drive

In this example I have directories named Folder1, Folder2, Stuff, and Things. I can list only the directories in my current directory by using ```ls``` and flag ```-d``` like before, but now use the wildcard ```*``` with ```/``` (directory indicator). 

```shell
$ ls -d */

Folder1/ Folder2/ Stuff/ Things/
```

---

## Printing to console

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

1) Change the contents and save to the original file

To change the file in place, the flag ```-i``` needs to be run 

* Note, for macos ```sed``` there needs to be an additional ```''``` after the ```-i```:

```shell
sed -i '' 's/Hellow Wolrd1/Hello World!/' file.txt
```

2) Change the contents and save to different file

Save changes to new file (file2.txt) and keep unchanged contents of the original file (file.txt)

```shell
sed 's/Hellow Wolrd1/Hello World!/' file.txt > file2.txt
```