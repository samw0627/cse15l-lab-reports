# Lab Report 5: More Testing On Markdown Parse
This week I tested my MarkdownParse implementation on over 600 files. I then compared the output of my implementation with joe's implementation.
## Doing the Comparison
In order to find the differences in output in different test, I amended the bash script with a for loop such that it would run all the files in the `test-files` repository. This is the bash script code.
```
for file in test-files/*.md;
do
   echo $file
   javaMarkdownParse $file
done
```
Then I run this command 
`time bash script.sh > lab5.txt` which prints out all the result in the text file.
Afterwards I run this command `diff markdownparse2/lab5.txt markdown-parse/results.txt` to compare the out put between my implementation and Joe's implementation.

## Comparison one: Line 212 (194.md)
The Comparison of the output is shown below.
```
212c212
< [] //My Implementation
---
> [url] //Joe's Implementation
```
This out put corresponds to file 194.md, the content is shown below.
```



## Comparison two: Line 1065 (file 577.md)
