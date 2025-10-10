# Chaining Commands
This module contains 12 challenges that include Chaining with Semicolons, Building on Success, Handling Failure, Your First Shell Script, Redirecting Script Output, Executable Shell Scripts, Understanding Shebangs, Scripting with Arguments, Scripting with Conditionals, Scripting with Default Cases, Scripting with Multiple Conditions and Reading Shell Scripts



# Chaining with Semicolons
The challenge asks to chain two commands using a semicolon in the shell. We need to execute `/challenge/pwn` followed by `/challenge/college` in sequence, using a semicolon to separate them. The goal is to understand how semicolons can be used to run multiple commands in a single line without needing to wait for each command to finish.

## My solution

**Flag:** `pwn.college{EIt4GK3pnJl8fb-FtZ75zVczWrr.QX1UDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I ran the command `/challenge/pwn` followed by `/challenge/college`, chaining them with a semicolon to ensure they execute sequentially.

    ```bash
    hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn ; /challenge/college
    Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
    pwn.college{EIt4GK3pnJl8fb-FtZ75zVczWrr.QX1UDO0wCO2kjNzEzW}
    ```

## What I learned

In this challenge, I learned how to chain commands using a semicolon in the shell. This allows running multiple commands sequentially without the need for multiple lines or scripts. The semicolon acts as a command separator, executing each command in order.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Chaining with Semicolons module page.




# Building on Success
The challenge requires you to use the `&&` operator in Linux to chain two commands together. The && operator executes the second command only if the first one succeeds, which means it exits with a status code of 0. In this challenge, we need to chain the programs `/challenge/first-success` and `/challenge/second` using the && operator. 

## My solution
**Flag:** `pwn.college{onTSX8V5Xh6hLNLwJnlIDYTC4XW.0lM0MDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. First, I tried running `/challenge/first-success` separately:
   ```bash
   hacker@chaining~building-on-success:~$ /challenge/first-success
   ```
   This didn't give any output, but I know it probably exited successfully since it didn't throw an error.

4. Next, I tried running `/challenge/second` separately:
   ```bash
   hacker@chaining~building-on-success:~$ /challenge/second
   ```
   This displayed an error message indicating that `/challenge/first-success` must be successfully chained with `/challenge/second` using `&&`.

5. Then, I chained the two commands using `&&`:
   ```bash
   hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
   Nice chaining! Flag: pwn.college{onTSX8V5Xh6hLNLwJnlIDYTC4XW.0lM0MDOxwCO2kjNzEzW}
   ```
   This command executed both `/challenge/first-success` and `/challenge/second` successfully, and the flag was displayed.

## What I learned
- The `&&` operator in Linux is used to chain commands where the second command runs only if the first one succeeds.
- Exit codes are crucial in determining whether a command has succeeded (exit code 0) or failed (non-zero exit code).

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Building on Success module page.





# Handling Failure
The challenge is about understanding and using the logical OR operator `||` in shell commands. This operator allows you to execute a second command only if the first one fails. The goal is to chain two specific commands, `/challenge/first-failure` and `/challenge/second`, using the || operator.

## My Solution
**Flag:** `pwn.college{cEQ_0SCkqWlt-aZ4ARoMFVE1mZg.01M0MDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I first tried running /challenge/first-failure alone to see what it does:
   ```bash
   hacker@chaining~handling-failure:~$ /challenge/first-failure
   ```
   It failed, producing an error message.
4. Then I ran /challenge/second by itself to observe its behavior:
   ```bash
   hacker@chaining~handling-failure:~$ /challenge/second
   Error: /challenge/first-failure must be successfully chained with
    /challenge/second using ||
   ```
5. Finally, I combined both commands using the || operator:
   ```bash
   hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
   ```
   Since /challenge/first-failure failed, the second command executed, giving me the flag.

## What I Learned

- The `||` operator is used for error handling, allowing fallback commands to run when the first command fails.
- Logical operators like && and || are essential for creating conditional execution in shell scripting.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Handling Failure module pages.





# Your First Shell Script
The challenge asks us to create a shell script that executes two specific commands sequentially. These commands are `/challenge/pwn` and `/challenge/college`. The task involves writing these commands into a file, saving it with a `.sh` extension, and then executing the script using the bash shell.

## My solution
**Flag:** `pwn.college{0BhT50YPgfIN7cSJnN5MatTHpz8.QXxcDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I opened the nano editor to create a new shell script file called `x.sh`.
    ```bash
    hacker@chaining~your-first-shell-script:~$ nano x.sh
    ```
4. Inside the nano editor, I typed the two commands that need to be executed:
   - `/challenge/pwn`
   - `/challenge/college`
   After saving the file, it looked like this:
    ```bash
    hacker@chaining~your-first-shell-script:~$ cat x.sh
    /challenge/pwn
    /challenge/college
    ```
5. I exited nano and executed the shell script using bash:
    ```bash
    hacker@chaining~your-first-shell-script:~$ bash x.sh
    Great job, you've written your first shell script! Here is the flag:
    pwn.college{0BhT50YPgfIN7cSJnN5MatTHpz8.QXxcDO0wCO2kjNzEzW}
    ```

## What I learned
- Shell scripts allow us to combine multiple commands into a single executable file, making it easier to run complex sequences of commands.
- To execute a shell script, we can use the `bash` command followed by the script's name.
- File extensions like `.sh` are common for shell scripts but are not required for execution.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Your First Shell Script module page.





# Redirecting Script Output
In this challenge we have to redirect the output of a script to another command. The script needs to execute two commands, `/challenge/pwn` and `/challenge/college`, and then pipe the combined output into the `/challenge/solve` command. This requires understanding how to redirect output from a script and pipe it effectively to another program in the shell.

## My solution
**Flag:** `pwn.college{85XQYHJI5ImHBvqh0TclD7MWHHn.QX4ETO0wCO2kjNzEzW}`

1. I connected the dojo host using the SSH command.
2. Now the shell is connected to dojo.
3. I created a new script called `challenge.sh` using the nano editor. I wrote the script with commands `/challenge/pwn` and `/challenge/college`.

    ```bash
    hacker@chaining~redirecting-script-output:~$ nano challenge.sh
    ```

4. I executed the script and piped its output to the /challenge/solve command.

    ```bash
    hacker@chaining~redirecting-script-output:~$ bash challenge.sh | /challenge/solve
    ```

5. Initially, I forgot to specify `bash` when running the script and encountered an error. I corrected the command to include `bash`, ensuring the script executed properly.

    ```bash
    hacker@chaining~redirecting-script-output:~$ challenge.sh | /challenge/solve
    bash: challenge.sh: command not found
    ```

    ```bash
    hacker@chaining~redirecting-script-output:~$ bash challenge.sh | /challenge/solve
    Correct! Here is your flag:
    pwn.college{85XQYHJI5ImHBvqh0TclD7MWHHn.QX4ETO0wCO2kjNzEzW}
    ```

## What I learned
- How to redirect output from a script to another command using pipes.
- Using redirection operators like `>` and `|` effectively in shell scripting.
- Specifying the shell e.g., `bash` when executing a script.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Redirecting Script Output module pages.




# Executable Shell Scripts
The challenge asks us to create a shell script that can be executed without explicitly invoking the bash command. Instead of running the script using `bash challenge.sh`, we need to make the script executable and run it directly.

## My solution
**Flag:** `pwn.college{Yz8mRrD0Z8htP00BVqLzrhBe9yl.QX0cjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. First, I created a new shell script file called `challenge.sh` using the `nano` editor:
   ```bash
   hacker@chaining~executable-shell-scripts:~$ nano challenge.sh
   ```

4. I added the following content to the script to execute the desired command:
   ```bash
   hacker@chaining~executable-shell-scripts:~$ cat challenge.sh
   /challenge/solve
   ```

5. I checked the file permissions to ensure it was not executable:
   ```bash
   hacker@chaining~executable-shell-scripts:~$ ls challenge.sh -l
   -rw-r--r-- 1 hacker hacker 17 Oct 10 11:31 challenge.sh
   ```

6. I made the script executable by changing its permissions with `chmod u+x`:
   ```bash
   hacker@chaining~executable-shell-scripts:~$ chmod u+x challenge.sh
   ```

7. I verified the updated permissions to confirm it was now executable:
   ```bash
   hacker@chaining~executable-shell-scripts:~$ ls challenge.sh -l
   -rwxr--r-- 1 hacker hacker 17 Oct 10 11:31 challenge.sh
   ```

8. Finally, I executed the script directly without invoking bash:
   ```bash
   hacker@chaining~executable-shell-scripts:~$ ./challenge.sh
   Congratulations on your shell script execution! Your flag:
   pwn.college{Yz8mRrD0Z8htP00BVqLzrhBe9yl.QX0cjM1wCO2kjNzEzW}
   ```

Note: It will not allow to print the flag using bash command.
```bash
hacker@chaining~executable-shell-scripts:~$ bash challenge.sh
You must make a shellscript in your home directory that will launch
/challenge/solve, make it executable, and invoke it without explicitly
specifying 'bash'!
```

## What I learned
- How to use `chmod` to change file permissions.
- Understanding that adding execute permissions allows a script to be run directly without specifying the `bash` command.
- The difference between running a script with `bash script.sh` and making it executable to run as `./script.sh` which is obviously same.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Executable Shell Scripts module page.





# Understanding Shebangs
This challenge is about understanding the importance and usage of shebangs in shell scripts. Shebangs are essential for determining the interpreter to be used when executing a script. The task requires creating a script with a correct shebang, setting the right permissions, and ensuring it outputs "hack the planet".

## My solution
**Flag:** `pwn.college{ImN1Jq0bsiouTWRTiLONT6YB_V_.0VOzMDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. Created a new file called solve.sh using nano:
   ```bash
   hacker@chaining~understanding-shebangs:~$ nano solve.sh
   ```
   Inside the file, I added the shebang line and the echo command:
   ```bash
   #!/bin/bash

   echo "hack the planet"
   ```

4. After saving, viewed the script's content to confirm:
   ```bash
   hacker@chaining~understanding-shebangs:~$ cat solve.sh
   #!/bin/bash

   echo "hack the planet"
   ```

5. Checked the file permissions:
   ```bash
   hacker@chaining~understanding-shebangs:~$ ls solve.sh -l
   -rw-r--r-- 1 hacker hacker 36 Oct 10 11:48 solve.sh
   ```

6. Made the script executable:
   ```bash
   hacker@chaining~understanding-shebangs:~$ chmod u+x solve.sh
   ```

7. Verified the new permissions:
   ```bash
   hacker@chaining~understanding-shebangs:~$ ls solve.sh -l
   -rwxr--r-- 1 hacker hacker 36 Oct 10 11:48 solve.sh
   ```

8. Ran the challenge script to verify:
   ```bash
   hacker@chaining~understanding-shebangs:~$ /challenge/run
   Testing your script...
   Perfect! Your flag:
   Flag: pwn.college{ImN1Jq0bsiouTWRTiLONT6YB_V_.0VOzMDOxwCO2kjNzEzW}
   ```

## What I learned
- Shebangs are crucial for specifying script interpreters.
- **Shebang Syntax:** Must be the first line, starting with `#!`.
- Scripts need execute permissions (chmod +x).

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Understanding Shebangs  module





# Scripting with Arguments
This challenge requires writing a bash script that can accept two arguments and output them in reverse order. The script should be created at `/home/hacker/solve.sh` and must be executable. Once the script works correctly, running the `/challenge/run` command will provide the flag.

## My solution
**Flag:** `pwn.college{oez84_a2gyJaQIlxF_wiwl_Vc8W.0VNzMDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. I opened the nano editor to create the solve.sh script.
    ```bash
    hacker@chaining~scripting-with-arguments:~$ nano solve.sh
    ```

4. I wrote the script to echo the second argument followed by the first.
    ```bash
    hacker@chaining~scripting-with-arguments:~$ cat solve.sh
    #!/bin/bash

    echo "$2 $1"
    ```

5. I changed the permissions of the script to make it executable which was already there as we changed in the previous challenge.
    ```bash
    hacker@chaining~scripting-with-arguments:~$ ls solve.sh -l
    -rwxr--r-- 1 hacker hacker 26 Oct 10 11:56 solve.sh
    ```

6. I tested the script with arguments to ensure it reverses them.
    ```bash
    hacker@chaining~scripting-with-arguments:~$ bash /home/hacker/solve.sh pwn college
    college pwn
    ```

7. Finally, I ran the challenge script to get the flag.
    ```bash
    hacker@chaining~scripting-with-arguments:~$ /challenge/run
    Correct! Your script properly reversed the arguments.
    Here's your flag:
    pwn.college{oez84_a2gyJaQIlxF_wiwl_Vc8W.0VNzMDOxwCO2kjNzEzW}
    ```

## What I learned
- The use of `$1`, `$2` to access the first and second arguments respectively and so on.
- The importance of setting the correct file permissions using `chmod`.
- Using nano editor for creating and editing scripts.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Scripting with Arguments module pages.





# Scripting with Conditionals
This challenge requires creating a bash script that uses conditional logic to make decisions based on input arguments. The script must check if the provided argument is "pwn" and output "college" if true, while printing nothing for any other input.

## My solution
**Flag:** `pwn.college{gqIwThZZ1TJAh-hXnrfBvXlCj3S.0lNzMDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I opened the nano editor to create a new script file called `solve.sh`.
4. I wrote the following bash script to check the condition:

    ```bash
    hacker@chaining~scripting-with-conditionals:~$ nano solve.sh
    ```

    ```bash
    #!/bin/bash

    if [ "$1" == "pwn" ]
    then
            echo "college"
    fi
    ```

5. After saving the script, I tested it with the argument "pwn" to see if it outputs "college":

    ```bash
    hacker@chaining~scripting-with-conditionals:~$ bash solve.sh pwn
    college
    ```

6. I also tested it with a different argument "hello" to ensure it outputs nothing:

    ```bash
    hacker@chaining~scripting-with-conditionals:~$ bash solve.sh hello
    ```

7. Finally, I ran the /challenge/run command to submit my solution and receive the flag:

    ```bash
    hacker@chaining~scripting-with-conditionals:~$ /challenge/run
    Correct! Your script properly handles all the conditions.
    Here's your flag:
    pwn.college{gqIwThZZ1TJAh-hXnrfBvXlCj3S.0lNzMDOxwCO2kjNzEzW}
    ```

## What I learned
- The proper syntax for if statements in bash, including mandatory spaces and line breaks.
- How to use conditional checks for string equality in scripts.
- The importance of testing scripts with different inputs to ensure correctness.
- How to write and execute bash scripts on a Linux system.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Scripting with Conditionals module pages.





# Scripting with Default Cases
The challenge asks to create a bash script that uses an if-else statement to handle both a specific case and a default case. The script should take one argument. If the argument is "pwn," it should output "college." For any other input, it should output "nope".

## My solution
**Flag:** `pwn.college{Mqo5b99ONWkBfhnYd61x7UWcnBX.01NzMDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I opened the nano editor to create a new script called `solve.sh` at `/home/hacker/solve.sh`.
4. I wrote the following bash script:

    ```bash
    #!/bin/bash

    if [ "$1" == "pwn" ]
    then
            echo "college"
    else
            echo "nope"
    fi
    ```

5. I saved and exited nano.
6. I tested the script with the command bash solve.sh pwn and got the output college.
    ```bash
    hacker@chaining~scripting-with-default-cases:~$ bash solve.sh pwn
    college
    ```
7. I tested it again with bash solve.sh hello and got nope as expected.
    ```bash
    hacker@chaining~scripting-with-default-cases:~$ bash solve.sh hello
    nope
    ```
8. Finally, I ran /challenge/run and received the flag.
    ```bash
    hacker@chaining~scripting-with-default-cases:~$ /challenge/run
    Correct! Your script properly handles the if/else conditions.
    Here's your flag:
    pwn.college{Mqo5b99ONWkBfhnYd61x7UWcnBX.01NzMDOxwCO2kjNzEzW}
    ```

## What I learned
- Understanding the use of if statements with string comparison.
- Using the else clause in bash scripting to handle all other cases.
- The structure of if-else statements in bash, including proper syntax.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Scripting with Default Cases module.





# Scripting with Multiple Conditions
This challenge requires you to create a bash script that handles multiple conditions using if-elif statements. The script should take a single argument and output specific results based on the value of that argument. If the argument is "hack", the script should output "the planet". If the argument is "pwn", it should output "college". If the argument is "learn", it should output "linux". For any other input, the script should output "unknown".

## My solution
**Flag:** `pwn.college{8hKJzM2boHRyBmxEaoDPaTp3JNH.0FOzMDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.

2. Now the shell is connected to dojo.

3. I accessed the nano editor to create the script file solve.sh using the command:
   ```bash
   nano solve.sh
   ```

4. I wrote the following bash script to handle multiple conditions:
   ```bash
   #!/bin/bash

   if [ "$1" == "hack" ]
   then
           echo "the planet"
   elif [ "$1" == "pwn" ]
   then
           echo "college"
   elif [ "$1" == "learn" ]
   then
           echo "linux"
   else
           echo "unknown"
   fi
   ```

5. I saved and exited the nano editor by pressing `Ctrl + X`.

6. I tested the script by running it with different arguments to ensure it works correctly:
   ```bash
   bash solve.sh hack
   bash solve.sh pwn
   bash solve.sh learn
   bash solve.sh foo
   ```

7. After verifying that the script works as expected, I ran the command `/challenge/run` to get the flag.

8. The flag was successfully retrieved.
    ```bash
    hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
    Correct! Your script properly handles all the conditions with elif.
    Here's your flag:
    pwn.college{8hKJzM2boHRyBmxEaoDPaTp3JNH.0FOzMDOxwCO2kjNzEzW}
    ```


## What I learned
- How to use if-elif statements in bash scripting to check multiple conditions.
- The importance of proper spacing in bash conditions like `[ "$1" == "hack" ]` requires spaces between the brackets and the content.
- How to handle command-line arguments in bash scripts using `$1` and so on.
- The difference between `if`, `elif`, and `else` statements in bash.

## References
- [pwn.college](https://pwn.college/linux-luminarium/chaining/) - Chaining Commands / Scripting with Multiple Conditions module page.





# Reading Shell Scripts
The goal is to find a hardcoded secret password within a given shell script and use it to retrieve the flag. The script in question is located at `/challenge/run`, and by examining its code we can extract the password.

## My solution
**Flag:** `pwn.college{gMdXM_ugh71SwPgr25q3XiAxA2h.0lMwgDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.  
2. Now the shell is connected to dojo.  
3. To find the password, I needed to read the contents of the shell script located at `/challenge/run`.  
   ```bash
   hacker@chaining~reading-shell-scripts:~$ cat /challenge/run
   #!/opt/pwn.college/bash

   read GUESS
   if [ "$GUESS" == "hack the PLANET" ]
           then
               echo "CORRECT! Your flag:"
               cat /flag
   else
               echo "Read the /challenge/run file to figure out the correct password!"
   fi
   ```
4. By examining the script, I found that the hardcoded password is "hack the PLANET".  
5. I executed the script and entered the password to retrieve the flag.  
   ```bash
   hacker@chaining~reading-shell-scripts:~$ /challenge/run
   hack the PLANET
   CORRECT! Your flag:
   pwn.college{gMdXM_ugh71SwPgr25q3XiAxA2h.0lMwgDOxwCO2kjNzEzW}
   ```

## What I learned  
- Shell scripts are plaintext files that can be easily read using commands like `cat`.  
- Understanding the basics of shell scripting, such as `read` and `if` statements.
- The `file` command can help determine if a file is a shell script or machine code.  

## References  
- [pwn.college](https://pwn.college) - Chaining Commands / Reading Shell Scripts module page.