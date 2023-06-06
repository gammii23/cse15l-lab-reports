### Debugging and Reflection
<br/>
1. EdStem Discussion
<br/>
<br/>

**Title: Unknown String index out of bounds error.**
<br/>

**Category: Debugging**


![](dog.png)

<br/>
a. I am using a Macbook air running Mac OS. I am using the visual studio code terminal.
<br/>
<br/>
b. So what was expected to happen is the loop keeps running until the user enters valid inputs. It will keep prompting the user and asking the user the same question until the inputs are valid.
<br/>
<br/>
c. I wanted to test out what it looks like when I enter invalid inputs. The program I created is a dog barking simulator. You pick either b,g,h for bark, growl, or howl, and then you choose between 1,2,3 for volume. I made sure that my bash script prints out the exit code and it is 1. Any help is appreciated. Thank you!
<br/>
<br/>
**Justin Gamm: Hi, Im unsure what you other two code files are but from what I can see, I can suggest one thing without explicitly telling you what to do. Remember scanning for next Int only looks for an integer but you are also clicking the enter key when you input an int. Try dealing the result of clicking enter. You cannot ignore it. Hope that helps.**
