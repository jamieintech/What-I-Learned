# Inputs from console

- run from the command prompt
- the user interacts with the application by reading data output on the command line
- the user interacts by entering data into the command line
- considered relatively low in user experience



## Input Stream Reader

- takes command line or standard input and returns it as String data

- the String returned by the Input Stream Reader can be parsed to other data types

    ```java
    import java.io.BufferedReader;
    import java.io.IOException;
    import java.io.InputStreamReader;
    
    public class ConsoleApp{
    //since the input from the command line can introduce errors, an error handler is needed
    //throws: method may have an exception
        public static void main(String[] args) throws IOException {
            //Instantiate the BufferedReader and create an object
            BufferedReader readIt = new BufferedReader(new InputStreamReader(System.in));
    
            //Take command line input and store it in a string
            String myname = readIt.readLine();
    
            //The command line input comes in as a string
            //parsing is needed to convert it into a different data type
            String num = readIt.readLine();
            int mynum = Integer.parseInt(num);
        }
    }
    ```

- in Java, when the application is deployed, it's exported to a `jar` file

    - `jar` file = Java archive
    - .jar files are bundled with the required imported classes => they run of their own
    - once exported, the .jar file can be run from the command line



## Scanner

- part of Java util class

- way much simpler than the input stream reader/buffered reader

  ```java
  import java.util.Scanner;
  
  public class ConsoleApp{
      public static void main(String[] args){
          Scanner myScan = new Scanner(System.in);
          System.out.println("Enter username:");
          
          String userName = myScan.nextLine();
          System.out.println("Greetings "+userName);
          
          myScan.close()
      }
  }
  ```

  

