# Lab Report 3 - Copy whole directories with  `scp -r`
## Step 1: Copying markdownparse2 into ieng6 account
Using the command `$ scp -r . cs15lwi22afk@ieng6.ucsd.edu:~/markdownparse2` I was able to copy the whole markdownparse2 directory to ieng6
![image](scnr1.png)
![image](scnr2.png)<br>
## Step 2: Compiling and running the tests after logging into ieng6
Next I log into ieng6 and tried to compile MarkdownparseTest using the commands<br>
`javac -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar MarkdownParseTest.java`<br>
 `java -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar org.junit.runner.JUnitCore MarkdownParseTest`<br>
![image](scnr3.png)
![image](scnr4.png)<br>


