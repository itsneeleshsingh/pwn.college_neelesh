# Pondering Paths
This module contains nine challenges that includes The Root, Program and absolute paths, Position thy self, Position elsewhere, Position yet elsewhere, implicit relative paths, explicit relative paths, implicit relative path and home sweet home.

# The Root
In this challenge a program is placed under the root directory `/pwn`. We have to execute the command using its absolute path in the terminal.

## My solution
**Flag:** `pwn.college{4UEP9jpFyLqynPjQNln38ooLBgU.QX4cTO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now on typing `/pwn` that is the absolute path for the program, It shows us the flag.
    ```bash
    hacker@paths~the-root:~$ /pwn
    BOOM!!!
    Here is your flag:
    pwn.college{4UEP9jpFyLqynPjQNln38ooLBgU.QX4cTO0wCO2kjNzEzW}
    ```
3. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

Here If I type only `pwn` - it will search for the directories in the relative path. Thus by using `/pwn`, It searches for it under the root directory.

## What I learned

1. Filesystem hierarchy basics
    - `/` is the root directory and all directories and files exist under it.
    - if I want to see all the files and directories under the root directory, I can specify `/` after `ls` as an argument.
        ```bash
        neel@NeelTech:~$ ls /
        ```
2. Absolute path vs Relative path
    - **In Absolute path** - It starts from `/` and we have to mention the file path, starting from the root.
    - **In Relative path** - It depends on the current directory. To specify file path we do not have to write the whole path starting from root.

3. Programs can be run not just by name but also by specifying their location in the filesystem. I get to know this because it was written in this challenge - `You can invoke a program by providing its path on the command line.`

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / The Root module pages
- Got to know about - `/home`, `/etc`, `/usr`, `/bin` and some others from the [Linux file system](https://docs.google.com/presentation/d/1rZYXk2waekELrSYIiBTk0z0XXx8e8ovvARrH0n6XeO8/edit?slide=id.g88f71ddc4c_0_0#slide=id.g88f71ddc4c_0_0) provided in the pwn.college dojo itself.


# Program and absolute paths
In this challenge, the program we need to run is named `run`, and it is located inside `/challenge`. Thus, the full absolute path to execute is `/challenge/run` and by invoking this path correctly, we can retrieve the flag.

## My solution

**Flag:** `pwn.college{IjVe1JAvbz_WiMRnAsMccJyYSm-.QX1QTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now on typing `/challenge/run` which is the absolute path to the program `run`, the flag is displayed.
    ```bash
    hacker@paths~program-and-absolute-paths:~$ /challenge/run
    Correct!!!
    /challenge/run is an absolute path! Here is your flag:
    pwn.college{IjVe1JAvbz_WiMRnAsMccJyYSm-.QX1QTN0wCO2kjNzEzW}
    ```

3. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

If I type `run` without the writing the absolute path, It will not run the program as we are presently in root directory.
```bash
hacker@paths~program-and-absolute-paths:~$ cd /challenge
hacker@paths~program-and-absolute-paths:/challenge$ ./run
Incorrect...
You did not call this challenge using an absolute path!
An absolute path is anchored at the root of the filesystem, so it starts with /
```
Thus If we go inside the challenge directory and execute the `run` program, it will show an error as we have to execute the program ONLY through absolute path.

## What I learned
1. Programs are often stored inside specific directories like `/bin`, `/usr/bin`, or `/challenge` in this challenge. 

2. Absolute vs Relative execution  
   - In Absolute path: `/challenge/run` always works no matter where we are in the filesystem.  
   - In Relative path: If I were already inside `/challenge`, I could have run it as `./run`. But this challenge doesn't accept that.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / Program and absolute paths module pages


# Position Thy self
This challenge introduced the `cd` command in linux. In this challenge we have to navigate to a specific directory which it will tell after some commands. Then after changing the directory we can run the `/challenge/run` to execute the program.

## My solution

**Flag:** `pwn.college{gvA7JDmbM_UfF0Smz2OZdKs9oXC.QX2QTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now execute any command or try to run `/challenge/run`.
    ```bash
    hacker@paths~position-thy-self:~$ /challenge/run
    Incorrect...
    You are not currently in the /var/lib/apt/lists directory.
    Please use the `cd` utility to change directory appropriately.
    ```
3. It shows the correct path. Thus change the directory using the `cd` command followed by the correct path as an argument.
    ```bash
    hacker@paths~position-thy-self:~$ cd /var/lib/apt/lists
    hacker@paths~position-thy-self:/var/lib/apt/lists$
    ```
4. Now execute the `/challenge/run` command to run the program.
    ```bash
    hacker@paths~position-thy-self:/var/lib/apt/lists$ /challenge/run
    Correct!!!
    /challenge/run is an absolute path, invoked from the right directory!
    Here is your flag:
    pwn.college{gvA7JDmbM_UfF0Smz2OZdKs9oXC.QX2QTN0wCO2kjNzEzW}
    ```
5. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

The `cd` command does not produce any output if successful. Just the prompt changes to reflect the new entered directory.
- I was stuck at the first command of how to get the correct path. But after some trials, I got that by just executing the run program in the current wrong directory will tell the correct directory through its output.

## What I learned

1. Using the cd command
    - `cd` is a command (change directory) and accepts arguments after that (paths)
    - `cd` accepts both absolute and relative paths.

2. The `~` shows the current path that your shell is located at. (Also written in dojo documentation)

3. Interaction with challenge programs
    - Some programs need to be executed from specific directories.
    - If we are in wrong directory, it can cause program to fail or give error.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / Position Thy self module pages
- Explored some things from [cd command](https://www.geeksforgeeks.org/linux-unix/cd-command-in-linux-with-examples/) like - `cd` or `cd ~` for going back to home directory and including dot in paths to access hidden files.


# Position elsewhere
This challenge introduced the `cd` command in linux. In this challenge we have to navigate to a specific directory which it will tell after some commands. Then after changing the directory we can run the `/challenge/run` to execute the program.

## My solution

**Flag:** `pwn.college{EUalv-oL6jCl9pdRSM8JmbGT9CR.QX3QTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now execute any command or try to run `/challenge/run`.
    ```bash
    hacker@paths~position-elsewhere:~$ /challenge/run
    Incorrect...
    You are not currently in the /tmp directory.
    Please use the `cd` utility to change directory appropriately.
    ```
3. It shows the correct path. Thus change the directory using the `cd` command followed by the correct path as an argument.
    ```bash
    hacker@paths~position-elsewhere:/$ cd tmp
    hacker@paths~position-elsewhere:/tmp$
    ```
4. Now execute the `/challenge/run` command to run the program.
    ```bash
    hacker@paths~position-elsewhere:/tmp$ /challenge/run
    Correct!!!
    /challenge/run is an absolute path, invoked from the right directory!
    Here is your flag:
    pwn.college{EUalv-oL6jCl9pdRSM8JmbGT9CR.QX3QTN0wCO2kjNzEzW}
    ```
5. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

Here `/challenge/run` is an absolute path as it is invoked from the right directory.

## What I learned

1. Using the cd command
    - `cd` is a command and accepts arguments after that.
    - `cd` accepts both absolute and relative paths.

2. Interaction with challenge programs
    - Some programs need to be executed from specific directories like here from `/tmp`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / Position elsewhere module pages.