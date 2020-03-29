# unix-linux-basics
A repo to document some basics in Unix/Linux scripting 

## Listing all directories in current working drive by name

Say I have to directories in my current drive named Folder1 and Folder2, I can list all the directories with the name ```Folder``` with ```ls``` and directory flag ```-d```

```shell
ls -d Folder

>>> Folder1/ Folder2/ 
```

---

## Listing all directories in current working drive

In this example I have directories named Folder1, Folder2, Stuff, and Things. I can list only the directories in my current directory by using ```ls``` and flag ```-d``` like before, but now use the wildcard ```*``` with ```/``` (directory indicator). 

```shell
ls -d */

>>> Folder1/ Folder2/ Stuff/ Things/
```

---

## Printing to console

Simple printing to the console with ```echo```

In the terminal:
```shell
$ echo Hello World!

>>> Hello World!
```

```shell
$ echo Hello    World!

>>> Hello World! # No extra spaces!
```

```shell
$ echo "Hello   World"'!' # Extra spaces (note the need for '!')

>>>Hello   World!
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
STR="this is a string"
echo "$STR" | cut -d' ' -f4

>>> string
```

The above code snippet just printed the substring to the console, but let's assign it to a variable:

```shell
STR="this is a string"
var="$(cut -d' ' -f 4 <<< $STR)"
echo "$var"

>>> string
```

In this code snippet, ```var``` will be the variable name and the trailing ```<<<``` before ```$STR``` does the actual assigning of substring to ```var```.

---

## Simple renaming of single file

Using ```mv``` to rename a single file. ```mv``` then ```original file name``` then ```new file name```

```shell
$ mv file.txt file_rename.txt
```

---

## 