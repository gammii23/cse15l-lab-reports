# URL and Servers

1) **Download JDK**
* [visit this link](https://www.oracle.com/java/technologies/downloads/) and download the latest version that corresponds to your OS.

2) **GitHub Desktop**
* [Download Here](https://desktop.github.com/)
* Login with your GitHub account.
* Once you login, click on the tutorial for creating a repository and follow the instrucitons.
* Once you've done the tutorial its time to clone your repository. Click the clone repository button and choose the repository you wish to clone.
* Great, Youve cloned your repository from the internet onto your Desktop application!

3) **Wavelet**
Before creating our webserver, there is starter code to download
* [Here is the repository](https://github.com/ucsd-cse15l-f22/wavelet) fork this repository, then clone it to GitHub Desktop and open it in visual studio.
* Feel free to read the code in Server.java but it is not needed. Do make sure to read the code in NumberServer and try to make sense of it.

4) **Web Server**
* first you must compile NumberServer along with Server(ex: javac NumberServer.java Server.java).
* Once you compile it, you can start your server with this command: java NumberServer <port> (fill in port without the arrows).
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

                                                      
                                                      
 * And here is two examples of how to edit the URL to highlight how the code funcitons:
                                                      
                                                      
 ![](https://github.com/gammii23/cse15l-lab-reports/blob/main/Screen%20Shot%202023-04-21%20at%202.31.26%20PM.png)          
 ![](https://github.com/gammii23/cse15l-lab-reports/blob/main/Screen%20Shot%202023-04-21%20at%202.32.46%20PM.png)                                                     
                                                      
                                                      
  
 
  

