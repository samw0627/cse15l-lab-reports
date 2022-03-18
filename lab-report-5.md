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
This output corresponds to file 194.md, the content is shown below.
```
[Foo*bar\]]:my_(url) 'title (with parens)'

[Foo*bar\]]
```
In this case, Joe's implementation is correct and my implementation is wrong.


## Comparison two: Line 1065 (577.md)
The Comparison of the output os shown below,
```
1065c1062
< [] //My Implementation
---
> [train.jpg] //Joe's Implementation
```
This output corresponds to file 577.md.
```
![foo](train.jpg)
```
In this case, my implementation is correct and Joe's implementation is wrong.

## Change in Implementation
For Error 1, the bug comes from the fact that open paren doesn't come right after the square brackets. Based on my implementation, it does not reach the `toReturn.add` statement if the open paren doesn't come right after the square brackets, hence the program failed to detect the code. This is the code block that need to be changed in order to fix this.
```
if(nextCloseBracket +1 == openParen && openParen + 1 != closeParen){
toReturn.add(markdown.sybstring(openParen + 1, closeParen));
```
For Error 2, the bug comes from the fact that Joe's program did not check for `!` at the front of the line, and printed anything when the program detects the square bracket. The code can be fixed by adding a statement to check if `!` exists at the beginning of the line, the program should output empty brackets. These are the code that needs to be changed 
```
  if(nextOpenBracket == -1 || nextCloseBracket == -1 || closeParen == -1 || openParen == -1) {
      return toReturn;
   }
 ```
