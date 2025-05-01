# upload1
1.general description?
in this project we used the (java language)by using(Intellj) to make a code that do
specific commands by the user's orders,in short,the code act's the 
Terminal,so we build two classes in the java(the Minishell class :that acts the main
class ,we run it by calling the functions that we made in the second
class and we also used the scanner to recieve the users requirements.
(the ShellCommandHandler class:that contains the methods and the todo lists to
implement the operations for each command)
as well (The shell will support basic file system operations like navigating
directories, listing contents, and creating files and directories.)
-------------------------------------------------------------------------------------------------------------------------------------------------
2.About compiling and running the code ?
i used (Intellj) to do the code by using (java language),first i thought about the
commands and what does each one of them do in general(in the Terminal) so i started to
build the functions for the required commands(pwd-ls-cd-touch-mkdir-and the help and
exit funstions in addition) in the ShellCommandHandler class,so when we run the
Minishell class and it scans the users input it will use these functions\methods ,so
after scanning the users input,for example(ls folder1)the minishell class with split
this input for 2 words,and will call the required function by the first word(here the
listing function for ls command)and will do this operation(the listing)on the next
word that specefied the required directory(here folder1).
in the ShellCommandHandler class,i also used two libraries( java.io.File;
 java.io.IOException;)in ShellCommandHandler class,and the
 library(java.util.Scanner;)in the minishell class and i used ready operations from
 the ready class(File)
 Attention,the the code is infinte code and it does not stop until the user input(exit)
 so the exit function will be called
----------------------------------------------------------------------------------------------------------------------------------------------
 3.Example?
compiler: Welcome to MiniShell! Type 'help' for a list of commands.

user: help

compiler: there are an available Commands that you can use:
1.cd [directory_name]    - Change current directory
2.cd..[with adding ..]    - Use '..' to move to parent directory
3.mkdir [directory_name] - Create a new directory"
4.touch [file_name]      - Create a new file
5.ls                     - List files and directories in the current directory
6.pwd                    - Print current working directory path
7.help                   - Show this help message
8.exit                   - Exit the program

user: mkdir 
compiler: Usage: mkdir [directory_name]

user:mkdir folder1
compiler:Directory created: folder1

user:mkdir folder1
compiler:Directory already exists.
---------------------------------------------------------------------------------------------------------------------------------------------
4.explanation for the functions
(the shellcomandhandler class)
public class ShellCommandHandler {            //the class 
    private File currentDirectory;             //an private atribute in the class

    public ShellCommandHandler() {             //constructer to Initialize currentDirectory to the user's current working directory
            String userDir = System.getProperty("user.dir");           //initialize string varriable and get the string value from the user
            File currentDirectory = new File(userDir);    //initializing a varriable and it's kind:file,by sending the user's string value to save it as currentDirectory
            return currentDirectory;
    }

   >>>>>>>>> public void printWorkingDirectory() {          //function to Print the absolute path of the current directory
        System.out.println("this is the absolute path of your current directory:"+currentDirectory.getAbsolutePath());
    }

    >>>>> public void listDirectory() {    //a function that Lists all files and directories in the current directory
        File[] listing = currentDirectory.listFiles();     //initializing an array,it's inputs are objects of the type-file-
        if (listing != null && listing.length > 0) {        //check if the array is not empty and it has a length(it means that it contains values)
            System.out.println("Files and directories in: " + currentDirectory.getAbsolutePath());    //to print each file or directory with it's absolute path as an output for the user
            for (File file : filesList) {             //to list the files by using for loop until finishing all the files in the currentDirectory
                if (file.isDirectory()) {          //to check if the next listing file is a directory-folder-
                    System.out.println("[DIR ] " + file.getName());       //if it is a directory,its name will be print Preceded with [DIR ]
                } else if (file.isFile()) {                     //to check if the next listing file is a file
                    System.out.println("[FILE] " + file.getName());           //if it is a file,its name will be print Preceded with [FILE ]
                } else {                                                    // Optional:  symbolic links or unknown types,if it is not a file or either a directory will print the the name preceded with [UNKW]
                    System.out.println("[UNKW] " + file.getName()); 
                }
            }
        } else {
            System.out.println("The current directory is empty or cannot be accessed.");     //if the recieved directory is empty,the sentence"The current directory is empty or cannot be accessed." will be printed
        }
    }

    >>>>>> public void changeDirectory(String name) {                //function recieves a name from the user to Implement the change directory command
        private static File currentDirectory = new File(System.getProperty("user.dir"));   
        if (name == null || name.trim().isEmpty()) {                      //checks if the varriable that was recieved by the user is empty
            System.out.println("Usage: cd [directory_name]");              //if it's impty "Usage: cd [directory_name]" will be printed and then exits the function
            return;
        }

        if (name.equals("..")) {          //checks if the varriable that was recieved by the user is ..                  
            File parentDirectory = currentDirectory.getParentFile();    //a new object from the type-file- will be initialized
            if (parentDirectory != null && parentDirectory.exists()) {    //check if the directory is not empty and is exists
                currentDirectory = parentDirectory;                        //The parentDirectory will be attributed to currentDirectory
                System.out.println("Changed directory to: " + currentDirectory.getAbsolutePath());
            } else {                          //if the directory is empty or not exists this sentenceAlready at the root directory. Cannot move up will be printed
                System.out.println("Already at the root directory. Cannot move up.");
            }
        } else {          //if the recieved name is not null or (..) will initialize a new object and implements the changing operation
            File nextnewDir = new File(currentDirectory, name);        //initialize a new object by using the constructer
            if (nextnewDir.exists() && nextnewDir.isDirectory()) {        //checks if the nextnewDir is already exists and if it is a Directory
                currentDirectory = nextnewDir;                  //if yes,the change operation will be done and the nextnewDir value will be attributed to the  currentDirectory value and then this-Changed directory to: " + currentDirectory.getAbsolutePath()- will be printed
                System.out.println("Changed directory to: " + currentDirectory.getAbsolutePath());
            } else {                          //if no,witch means that the nextnewDir is not already exists or if it is not a Directory,this-"Directory not found: " + the name of the directory- will be printed
                System.out.println("Directory not found: " + name);
            }
    }

   >>>> public void makeDirectory(String name) {      //a function to Implement the make directory command
            private static File currentDirectory = new File(System.getProperty("user.dir"));
                if (name == null || name.trim().isEmpty()) {      //checks if the recieved value name from the user  is null,will show usage message: "Usage: mkdir [directory_name]"
                    System.out.println("Usage: mkdir [directory_name]");
                    return;
                }

                File newDir = new File(currentDirectory, name);

                if (newDir.exists()) {           //checks If the directory already exists,will print: "Directory already exists."
                    if (newDir.isDirectory()) {
                        System.out.println("Directory already exists.");
                    } else {                               //if it is exists but as a file not as a direstory,will print ("A file with that name already exists.");
                        System.out.println("A file with that name already exists.");
                    }
                    return;
                }

                if (newDir.mkdir()) {        // If directory creation is successful,will print: "Directory created: [name]"
                    System.out.println("Directory created: " + name);
                } else {                                // If directory creation fails, print: "Failed to create directory."
                    System.out.println("Failed to create directory.");
                }

    public void createFile(String name) {      //function to Implement the create file command
        private static File currentDirectory = new File(System.getProperty("user.dir"));
                if (name == null || name.trim().isEmpty()) {         //checks If the recieved name is null, show usage message: "Usage: touch [file_name]"
                    System.out.println("Usage: touch [file_name]");
                    return;
                }

                File newFile = new File(currentDirectory, name);

                if (newFile.exists()) {                               // If file already exists, print: "File already exists."
                    if (newFile.isFile()) {
                        System.out.println("File already exists.");
                    } else {                                       // If it is already exists but as a directory, print:"A directory with that name already exists."
                        System.out.println("A directory with that name already exists.");
                    }
                    return;
                }

                try {
                    if (newFile.createNewFile()) {          // If file creation is successful, print: "File created: [name]"
                        System.out.println("File created: " + name);
                    } else {                            // If file creation is not successful, print: "Failed to create file."
                        System.out.println("Failed to create file.");
                    }
                } catch (IOException e) {                       // If file creation fails, print error message with exception details
                    System.out.println("Error creating file: " + e.getMessage());
                }
    }

    public void printHelp() {        // function that helps the user by giving him a list that contains the available commands with it's mission,Implement help command to print information about all available commands,the method Lists all commands with their descriptions as shown:      
            System.out.println("there are an available Commands that you can use:");
            System.out.println(" 1.cd [directory_name]    - Change current directory");
            System.out.println(" 2.cd..[with adding ..]    - Use '..' to move to parent directory");
            System.out.println(" 3.mkdir [directory_name] - Create a new directory");
            System.out.println(" 4.touch [file_name]      - Create a new file");
            System.out.println(" 5.ls                     - List files and directories in the current directory");
            System.out.println(" 6.pwd                    - Print current working directory path");
            System.out.println(" 7.help                   - Show this help message");
            System.out.println(" 8.exit                   - Exit the program");
        
    }

    public File getCurrentDirectory() {        //to Return the current directory(it is a getter gor the private attribute-currentDirectory-
            return currentDirectory;; 
    }











