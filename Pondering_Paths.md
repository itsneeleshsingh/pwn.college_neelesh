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
    - **In Absolute path** - It starts from `/` and you have to mention the file path, starting from the root.
    - **In Relative path** - It depends on the current directory. To specify file path we do not have to write the whole path starting from root.

3. Programs can be run not just by name but also by specifying their location in the filesystem. I get to know this because it was written in this challenge - `You can invoke a program by providing its path on the command line.`

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / The Root module pages
- Got to know about - `/home`, `/etc`, `/usr`, `/bin` and some others from the [Linux file system](https://docs.google.com/presentation/d/1rZYXk2waekELrSYIiBTk0z0XXx8e8ovvARrH0n6XeO8/edit?slide=id.g88f71ddc4c_0_0#slide=id.g88f71ddc4c_0_0) provided in the pwn.college dojo itself.