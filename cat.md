```cat```



```
Options Description
-b (GNU: --number-nonblank), number non-blank output lines
-e implies -v but also display end-of-line characters as $ (GNU only: -E the same, but without implying -v)
-n (GNU: --number), number all output lines
-s (GNU: --squeeze-blank), squeeze multiple adjacent blank lines
-t implies -v, but also display tabs as ^I (GNU: -T the same, but without implying -v)
-u use unbuffered I/O for stdout. POSIX does not specify the behavior without this option.
-v (GNU: --show-nonprinting), displays nonprinting characters, except for tabs and the end of line character
```

<table class="wikitable">
<tbody><tr>
<th><kbd>Command</kbd></th>
<th>Explanation
</th></tr>
<tr>
<td><kbd>cat file1.txt </kbd></td>
<td>Display contents of file
</td></tr>
<tr>
<td><kbd>cat file1.txt file2.txt</kbd></td>
<td>Concatenate two text files and display the result in the terminal
</td></tr>
<tr>
<td><kbd>cat file1.txt file2.txt &gt; newcombinedfile.txt</kbd></td>
<td>Concatenate two text files and write them to a new file
</td></tr>
<tr>
<td><kbd>cat &gt;newfile.txt</kbd></td>
<td>Create a file called newfile.txt. Type the desired input and press CTRL+D to finish. The text will be in file newfile.txt.
</td></tr>
<tr>
<td><kbd>cat -n file1.txt file2.txt &gt; newnumberedfile.txt</kbd></td>
<td>Some implementations of cat, with option -n, can also number lines
</td></tr>
<tr>
<td><kbd>cat file1.txt &gt; file2.txt</kbd></td>
<td>Copy the contents of file1.txt into file2.txt
</td></tr>
<tr>
<td><kbd>cat file1.txt &gt;&gt; file2.txt</kbd></td>
<td>Append the contents of file1.txt to file2.txt
</td></tr>
<tr>
<td><kbd>cat file1.txt file2.txt file3.txt | sort &gt; test4</kbd></td>
<td>Concatenate the files, sort the complete set of lines, and write the output to a newly created file
</td></tr>
<tr>
<td><kbd>cat file1.txt file2.txt | less</kbd></td>
<td>Run the program "less" with the concatenation of file1 and file2 as its input
</td></tr>
</tbody></table>