# Lab Report 2 - Debugging 
This lab report will detail the process of debugging the file MarkDownParse.java. The main goal of this program is to read and print only links in the markdown file.
## Fix 1: Testing the imagelink file
### (a) Symptom
[Here](https://github.com/samw0627/markdown-parse-revisited/blob/974bfe799475872fc8f3fbe259e67e7f659741b4/imagelink.md) is the link to the failure inducing input that prompted us to make the change.

When we tried to read from a program that has an image and a link, this was the original output.

`[randomimage.png, https://something.com, https://something.com, some-page.html, some-page.html]` 

whereas the expected output should be

`[https://something.com, some-page.html]`

The program printed out image file name as well as the links of the webpages.

### (b)What's The Problem?
The main bug is that the program failed to recognise that the brackets surrounding the image file is not a link. Therefore, when the program detects Square Brackets and Open Brackets on the same line, in this case `![image](someimage.png` , it printed out the image file name as well as the links of the webpage.

###(c)Fix





