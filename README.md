ALX task 0x16.C simple_shell group project with David Chetty and Favour Nnenna

This file contains the steps taken in building the simple shell project.

After a command is entered, the following things are done:

Command is entered and if length is non-null, keep it in history.
Parsing : Parsing is the breaking up of commands into individual words and strings
Checking for special characters like pipes, etc is done
Checking if built-in commands are asked for.
If pipes are present, handling pipes.
Executing system commands and libraries by forking a child and calling execvp.
Printing current directory name and asking for next input.
For keeping history of commands, recovering history using arrow keys and handling autocomplete using the tab key, we will be using the readline library provided by GNU.

Printing the directory can be done using getcwd.
Getting user name can be done by getenv(“USER”)
Parsing can be done by using strsep(“”). It will separate words based on spaces. Always skip words with zero length to avoid storing of extra spaces.
After parsing, check the list of built-in commands, and if present, execute it. If not, execute it as a system command. To check for built-in commands, store the commands in an array of character pointers, and compare all with strcmp().
Note: “cd” does not work natively using execvp, so it is a built-in command, executed with chdir().
For executing a system command, a new child will be created and then by using the execvp, execute the command, and wait until it is finished.
Detecting pipes can also be done by using strsep(“|”).To handle pipes, first separate the first part of the command from the second part. Then after parsing each part, call both parts in two separate new children, using execvp. Piping means passing the output of first command as the input of second command.
Declare an integer array of size 2 for storing file descriptors. File descriptor 0 is for reading and 1 is for writing.
Open a pipe using the pipe() function.

Create two children.

In child 1->

Here the output has to be taken into the pipe.
Copy file descriptor 1 to stdout.
Close  file descriptor 0.
Execute the first command using execvp()

In child 2->

Here the input has to be taken from the pipe.
Copy file descriptor 0 to stdin.
Close file descriptor 1.
Execute the second command using execvp()
Wait for the two children to finish in the parent.

General Requirements

Allowed editors: vi, vim, emacs
All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options -Wall -Werror -Wextra -pedantic -std=gnu89
All your files should end with a new line
A README.md file, at the root of the folder of the project is mandatory
Your code should use the Betty style. It will be checked using betty-style.pl and betty-doc.pl
Your shell should not have any memory leaks
No more than 5 functions per file
All your header files should be include guarded
Use system calls only when you need to (why?)
Write a README with the description of your project
You should have an AUTHORS file at the root of your repository, listing all individuals having contributed content to the repository. Format, see Docker

GitHub

*There should be one project repository per group. If you and your partner have a repository with the same name in both your accounts, you risk a 0% score. Add your partner as a collaborator. *

More Info

Output

Unless specified otherwise, your program must have the exact same output as sh (/bin/sh) as well as the exact same error output.
The only difference is when you print an error, the name of the program must be equivalent to your argv[0]
