# Lab Report 3: Testing MarkdownParse
This lab report will detail the process of testing my implementation of MarkdownParse and another implementation of MarkdownParse that I have reviewed on 3 novel implementation.
Here is the [link](https://github.com/samw0627/markdown-parse-revisited) to my repository and here is the [link](https://github.com/w2llS/markdown-parse) to the repository I have reviewed.
## Snippet 1 - with backticks
### JUnit Test for My Implementation
    @Test
    public void getLinksnew1() throws IOException{
        Path fileName = Path.of("new1.md");
        String contents = Files.readString(fileName);
        assertEquals(List.of("`google.com","google.com", "ucsd.edu"), MarkdownParse.getLinks(contents));
        
### JUnit Test for the Reviewed Implementation
    @Test
    public void getLinksnew1() throws IOException{
        String fileContents = Files.readString(Path.of("new1.md"));
        ArrayList<String> testOutput = MarkdownParse.getLinks(fileContents.split("\n"));
        assertEquals("Check first element in array", "`google.com", testOutput.get(0));
        assertEquals("Check first element in array", "google.com", testOutput.get(1));
        assertEquals("Check first element in array", "ucsd.edu", testOutput.get(2));
        }
        

### JUnit Output for My Implementation
    1) getLinksnew1(MarkdownParseTest)
        java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com, ucsd.edu]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.getLinksnew1(MarkdownParseTest.java:42)
        
### JUnit Output for Reviewed Implementation

    1) getLinksnew1(MarkdownParseTest)
        org.junit.ComparisonFailure: Check first element in array expected:<[`google].com> but was:<[url].com>
        at org.junit.Assert.assertEquals(Assert.java:117)
        at MarkdownParseTest.getLinksnew1(MarkdownParseTest.java:55)
        
 For my code, I think a small changes can be made. I can add a criteria of checking the number of backticks in the square brackets. Output the link if there are even number of backticks, don't print the link if there are odd numbers.

## Snippet 2 - nest parentheses, brackets, and escaped brackets
### JUnit Test for My Implementation
    @Test
    public void getLinksnew2() throws IOException{
        Path fileName = Path.of("new2.md");
        String contents = Files.readString(fileName);
        assertEquals(List.of("a.com", "a.com(())","example.com"), MarkdownParse.getLinks(contents));
    }
    
    
### JUnit Test for the Reviewed Implementation
      @Test
      public void getLinksnew2() throws IOException{
        String fileContents = Files.readString(Path.of("new2.md"));
        ArrayList<String> testOutput = MarkdownParse.getLinks(fileContents.split("\n"));
        assertEquals("Check first element in array", "`a.com", testOutput.get(0));
        assertEquals("Check first element in array", "a.com(())", testOutput.get(1));
        assertEquals("Check first element in array", "example.com", testOutput.get(2));
      }
      
### JUnit Output for My Implementation
      2) getLinksnew2(MarkdownParseTest)
        java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[a.com, a.com((, example.com]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.getLinksnew2(MarkdownParseTest.java:49)
  
### JUnit Output for Reviewed Implementation
    2) getLinksnew2(MarkdownParseTest)
        org.junit.ComparisonFailure: Check first element in array expected:<[`a].com> but was:<[a.com)](b].com>
        at org.junit.Assert.assertEquals(Assert.java:117)
        at MarkdownParseTest.getLinksnew2(MarkdownParseTest.java:66)
 I think making it so that this case would work requires major change to the code. This is because there are a lot of combination of nested parentheses and the best way to check whether open paren equals to close paren is to use a stack.
 
 ## Snippet 3 - Newlines in brackets and parentheses
 ### JUnit Test for My Implementation
    @Test
    public void getLinksnew3() throws IOException{
        Path fileName = Path.of("new3.md");
        String contents = Files.readString(fileName);
        assertEquals(List.of("https://ucsd-cse15l-w22.github.io/"), MarkdownParse.getLinks(contents));
    }
 ### JUnit Test for the Reviewed Implementation
     @Test
     public void getLinksnew3() throws IOException{
        String fileContents = Files.readString(Path.of("new3.md"));
        ArrayList<String> testOutput = MarkdownParse.getLinks(fileContents.split("\n"));
        assertEquals("Check first element in array", "https://ucsd-cse15l-w22.github.io/", testOutput.get(0));
        }
 ### JUnit Output for My Implementation
     3) getLinksnew3(MarkdownParseTest)
     java.lang.AssertionError: expected:<[https://ucsd-cse15l-w22.github.io/]> but was:<[]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.getLinksnew3(MarkdownParseTest.java:56)
        
 ### JUnit Output for Reviewed Implementation
     3) getLinksnew3(MarkdownParseTest)
        java.lang.IndexOutOfBoundsException: Index 0 out of bounds for length 0
        at java.base/jdk.internal.util.Preconditions.outOfBounds(Preconditions.java:64)
        at java.base/jdk.internal.util.Preconditions.outOfBoundsCheckIndex(Preconditions.java:70)
        at java.base/jdk.internal.util.Preconditions.checkIndex(Preconditions.java:248)
        at java.base/java.util.Objects.checkIndex(Objects.java:373)
        at java.base/java.util.ArrayList.get(ArrayList.java:426)
        at MarkdownParseTest.getLinksnew3(MarkdownParseTest.java:77)
I think I can add minor changes to the code. I can use the trim function that removes all front and tailing space before performing the parsing operation.




     
