# URL,Servers,and Debugging

1) **Download JDK**
* [visit this link](https://www.oracle.com/java/technologies/downloads/) and download the latest version that corresponds to your OS.

2) **GitHub Desktop**
* [Download Here](https://desktop.github.com/)
* Login with your GitHub account.
* Once you login, click on the tutorial for creating a repository and follow the instrucitons.
* Once you've done the tutorial its time to clone your repository. Click the clone repository button and choose the repository you wish to clone.
* Great, Youve cloned your repository from the internet onto your Desktop application!

3) **Wavelet**<br/><br/>
Before creating our webserver, there is starter code to download
* [Here is the repository](https://github.com/ucsd-cse15l-f22/wavelet) fork this repository, then clone it to GitHub Desktop and open it in visual studio.
* Feel free to read the code in Server.java but it is not needed. Do make sure to read the code in NumberServer and try to make sense of it.

4) **Web Server**
* first you must compile NumberServer along with Server ` javac NumberServer.java Server.java`
* Once you compile it, you can start your server with this command: `java NumberServer <port>` (fill in port without the arrows).
* You can now visit the web server with the URL provided in terminal and use different paths that are seen in the starter code
  
5) **Creating a StringServer**
 * First of all here is the code I used to created a web server that supports adding Strings and printing the result of all added string:
  
  
```java 
import java.io.IOException;
import java.net.URI; 
import java.util.*;


class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;
    String message="";

    ArrayList<String> wordList= new ArrayList<String>();
   
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(" Justins Number is: %d", num);
       
        } 
        else if(url.getPath().contains("/add-message"))
        {
            String[] parameters = url.getQuery().split("=");
          
                if (parameters[0].equals("s")) {
                    message+="\n";
                 for(int i=1;i<parameters.length;i++)
                 message+=" "+parameters[i];
                }
                return message;
        } 
            else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/")) {
                return message;
            }
            return "404 Not Found!";
        }
    }
}


public class StringServer
{
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
   ```

  <br/>                                     
                                                      
                                                      
 * And here are two examples of how to edit the URL to highlight how the code funcitons:
         
   <br/>                                                     
                                                      
                                                      
                                                      
                                                      
 ![](https://github.com/gammii23/cse15l-lab-reports/blob/main/Screen%20Shot%202023-04-21%20at%202.31.26%20PM.png)          
 ![](https://github.com/gammii23/cse15l-lab-reports/blob/main/Screen%20Shot%202023-04-21%20at%202.32.46%20PM.png)                                                     
                                                      
Okay so let's talk about this code:
1) The method that control these URL requests is ```public String handleRequest(URI url)```.
  First of all my handler class has a class variable called "message". This gets concatenated each time a URL is requested. Each time a URL is requested, it is passed through the handleRequest method in the parameter `(URI url)`. The method looks at the path and if the path contains "add-message" it then checks if there is a query(?). An array called parameters stores all argument in the URL and all the arguments are before/after the equals signs in the URL. The code checks if the first index of the array is "s". and if it is, it adds each element of the array after that to the class variable "message". So as you can see, message is constantly getting updated and printed.This code all relies on the URL though, mainly the path to update the message variable. The values of this code include "add-message", "s", new Handler(), etc. The things that change when a URL is requested in parameters array and messages get updated.
  
  
# Part 2
1) Array method "ReverseInPlace"
* The method "ReverseInPlace" has fundamental errors that create unwanted symptoms. Here is the J-unit tests I wrote to test this method and the other methods in the ArrayExamples class:
<br/>


```java 
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
    int [] input2= {7,5,4};
    int [] expected= {4,5,7};
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(expected,input2);
	}


  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
    int [] input2= {1,2,3};
    int [] expected= {3,2,1};
    assertArrayEquals(expected,ArrayExamples.reversed(input2));
  }

  @Test 
  public void testAverage()
  {
    double[]nums={1.0,1.0,2.0,3.0,4.0,5.0};
    double result= (16.0/6.0);
    assertEquals(result,ArrayExamples.averageWithoutLowest(nums),0.0001);
  }
}

   ```
   
<br/>
* The failure-inducing input when testing ReverseInPlace would be 
 
 
 
 ```java
 int [] input2= {7,5,4}; 
 ```

<br/>
The expected result is {4,5,7} but the actual code loops through the array too many times.

<br/>

* An input that doesn't result in a failure is seen in this code:
<br/>


```java
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
  }
  ```
  
 <br/>
 
 * The input 
 
 ```java
 int[] input1 = { 3 };
 ```
 Does not create an error due to the fact that there is nothing to switch around. As you can see the original code has a bug that makes it so it does not work for *most* cases

