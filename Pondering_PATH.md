# Pondering PATH
This module contains 5 challenges that includes The PATH Variable, Setting PATH, Finding Commands, Adding Commands and Hijacking Commands.



# The PATH Variable
The challenge requires manipulating the PATH environment variable to prevent program from finding the `rm` command. By modifying the PATH, we can cause the program to fail when trying to delete a flag, allowing us to retrieve it instead. 

## My solution
**Flag:** `pwn.college{8j1Bzv6axf_Y9rz21x6IC9F0NII.QX2cDM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. I decided to empty the PATH variable so that commands like rm won't be found. I tried setting it with spaces first but realized that was incorrect:
    ```bash
    hacker@path~the-path-variable:~$ PATH = ""
    bash: PATH: command not found
    ```

4. Corrected the command by removing the spaces:
    ```bash
    hacker@path~the-path-variable:~$ PATH=""
    ```

5. Then I executed the challenge program:
    ```bash
    hacker@path~the-path-variable:~$ /challenge/run
    Trying to remove /flag...
    /challenge/run: line 4: rm: No such file or directory
    The flag is still there! I might as well give it to you!
    pwn.college{8j1Bzv6axf_Y9rz21x6IC9F0NII.QX2cDM1wCO2kjNzEzW}
    ```

## What I learned

- The PATH variable determines where the shell looks for executable commands.
- Proper syntax is crucial in shell commands and spaces can cause unexpected errors.

## References
- [pwn.college](https://pwn.college/linux-luminarium/path/) - Pondering PATH / The PATH Variable module.




# Setting PATH
The challenge asks us to modify the PATH environment variable to include a specific directory containing an executable needed by a script.

## My solution
**Flag:** `pwn.college{Q9yKBsFZbdix8bpCMmkJAY6H3qV.QX1cjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. I needed to set the PATH to include the directory where the 'win' command is located. I So I ran the following command to set PATH:

    ```bash
    hacker@path~setting-path:~$ PATH=/challenge/more_commands
    ```

4. After setting PATH, I executed the run script to test if the 'win' command is recognized without specifying its absolute path:

    ```bash
    hacker@path~setting-path:~$ /challenge/run
    Invoking 'win'....
    Congratulations! You properly set the flag and 'win' has launched!
    ```

5. The command executed successfully, confirming that the PATH was set correctly.

## What I learned
- The PATH variable is a list of directories where the shell looks for executable commands.
- Modifying PATH allows users to run commands from specific directories without typing the full path.

## References
- [pwn.college](https://pwn.college/linux-luminarium/path/) - Pondering PATH /  Setting PATH module.




# Finding Commands
The shell looks through each directory in $PATH in order and executes the first matching command. We need to find a hidden 'win' command in our PATH and locate the associated flag in its directory using the which command.

## My solution
**Flag:** `pwn.college{gGDjnpyi27PJIMNB1d6WmfhuGyp.01NzEzNxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. I used the `which` command to find the location of the 'win' executable. The output showed the path to 'win'.

    ```bash
    hacker@path~finding-commands:~$ which win
    /challenge/paths/22411/win
    ```

4. I listed the contents of the directory where 'win' was found to check for the flag file.

    ```bash
    hacker@path~finding-commands:~$ ls /challenge/paths/22411
    flag  win
    ```

5. I used the `cat` command to read the flag file in the same directory.

    ```bash
    hacker@path~finding-commands:~$ cat /challenge/paths/22411/flag
    pwn.college{gGDjnpyi27PJIMNB1d6WmfhuGyp.01NzEzNxwCO2kjNzEzW}
    ```

## What I learned
- The shell uses the $PATH variable to search for executable commands in order.
- The `which` command helps locate the exact path of a command.
- Important to check directory permissions when accessing hidden files like the flag.

## References
- [pwn.college](https://pwn.college/linux-luminarium/path/) - Pondering PATH / Finding Commands module pages.




# Adding Commands
The challenge requires creating a shell script named `win` that retrieves the flag by executing `cat /flag`. The script must be added to the PATH so that it can be found and executed by the `/challenge/run` command, which runs as root.

## My solution
**Flag:** `pwn.college{wDcMNEO5pfkLonUHNNuFwhqsWd8.QX2cjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. I checked the current PATH environment variable to find where `cat` is located:
   ```bash
   hacker@path~adding-commands:~$ cat "$PATH"
   cat: '/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin': No such file or directory
   ```
   The error indicated the current PATH. I then looked for 'cat' in these directories.

4. I found that 'cat' is located in '/usr/bin/':
   ```bash
   hacker@path~adding-commands:~$ /usr/bin/ca
   cal                 callgrind_control   cat                 cautious-launcher
   ```
   
5. I created a new file `win` in my home directory and added the command to execute 'cat /flag':
   ```bash
   hacker@path~adding-commands:~$ nano win
   ```
   ```bash
   /usr/bin/cat /flag
   ```
   
6. Made the 'win' script executable:
   ```bash
   hacker@path~adding-commands:~$ chmod u+x win
   ```
   
7. Added my home directory to the PATH to ensure `win` can be found:
   ```bash
   hacker@path~adding-commands:~$ PATH="/home/hacker/:$PATH"
   ```
   
8. Verified the updated PATH:
   ```bash
   hacker@path~adding-commands:~$ cat "$PATH"
   cat: '/home/hacker/:/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin': No such file or directory
   ```
   
9. Ran the `/challenge/run` command to execute `win` as root:
   ```bash
   hacker@path~adding-commands:~$ /challenge/run
   Invoking 'win'....
   pwn.college{wDcMNEO5pfkLonUHNNuFwhqsWd8.QX2cjM1wCO2kjNzEzW}
   ```

## What I learned
- Understanding how the PATH variable works and how the shell locates executables.
- Creating and executing custom shell scripts.
- Using absolute paths to ensure commands are found.

## References
- [pwn.college](https://pwn.college/linux-luminarium/path/) - Pondering PATH / Adding Commands module





# Hijacking Commands
This challenge involves hijacking commands on a Linux system by manipulating the PATH environment variable. The goal is to modify the behavior of the `rm` command to retrieve a hidden flag. The challenge requires creating a custom executable so that `rm` command ensures it is found before the system's actual `rm` when commands are executed.

## My solution
**Flag:** `pwn.college{gd3S0MUGmgFkaQFtfEMOHFu3Izf.QX3cjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. First, I checked the current PATH variable to understand where the system searches for commands:
   ```bash
   hacker@path~hijacking-commands:~$ cat "$PATH"
   cat: '/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin': No such file or directory
   ```

4. I tried to list commands starting with 'ca' to see if any important commands are present:
   ```bash
   hacker@path~hijacking-commands:~$ /bin/ca
   cal                 callgrind_control   cat                 cautious-launcher
   calendar            captoinfo           catchsegv
   callgrind_annotate  cas_help            catman
   ```

5. I used `cat` to check if it works:
   ```bash
   hacker@path~hijacking-commands:~$ /bin/cat
   ^C
   ```

6. I created a custom `rm` script that displays the flag:
   ```bash
   hacker@path~hijacking-commands:~$ nano rm
   ```

   Content of the `rm` script:
   ```bash
   /bin/cat /flag
   ```

7. I made the script executable:
   ```bash
   hacker@path~hijacking-commands:~$ chmod u+x rm
   ```

8. I modified the PATH to include my current directory first:
   ```bash
   hacker@path~hijacking-commands:~$ PATH="/home/hacker/"
   ```

9. I tested if the system can find `cat` with the new PATH:
   ```bash
   hacker@path~hijacking-commands:~$ cat "$PATH"
   bash: cat: command not found
   ```

10. Finally, I executed the challenge script to get the flag:
    ```bash
    hacker@path~hijacking-commands:~$ /challenge/run
    Trying to remove /flag...
    pwn.college{gd3S0MUGmgFkaQFtfEMOHFu3Izf.QX3cjM1wCO2kjNzEzW}
    ```

## What I learned

- The **PATH variable** determines the order in which directories are searched for commands.
- Placing a custom executable in a directory that appears first in PATH allows it to override system commands.
- Creating an executable script with the same name as a system command can intercept its behavior.

## References
- [pwn.college](https://pwn.college/linux-luminarium/path/) - Pondering PATH / Hijacking Commands module page.