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

## What I learned

1. Using the cd command
    - `cd` is a command and accepts arguments after that.
    - `cd` accepts both absolute and relative paths.

2. Interaction with challenge programs
    - Some programs need to be executed from specific directories like here from `/tmp`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / Position elsewhere module pages.


# Position yet elsewhere
This challenge introduced the `cd` command in linux. In this challenge we have to navigate to a specific directory which it will tell after some commands. Then after changing the directory we can run the `/challenge/run` to execute the program.

## My solution

**Flag:** `pwn.college{YAZ-ZsgNs_Kr_wd4NUiHTfPKdEv.QX4QTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now execute any command or try to run `/challenge/run`.
    ```bash
    hacker@paths~position-yet-elsewhere:~$ /challenge/run
    Incorrect...
    You are not currently in the /usr/include directory.
    Please use the `cd` utility to change directory appropriately.
    ```
3. It shows the correct path. Thus change the directory using the `cd` command followed by the correct path as an argument.
    ```bash
    hacker@paths~position-yet-elsewhere:~$ cd /usr/include
    ```
4. Now execute the `/challenge/run` command to run the program.
    ```bash
    hacker@paths~position-yet-elsewhere:/usr/include$ /challenge/run
    Correct!!!
    /challenge/run is an absolute path, invoked from the right directory!
    Here is your flag:
    pwn.college{YAZ-ZsgNs_Kr_wd4NUiHTfPKdEv.QX4QTN0wCO2kjNzEzW}
    ```
5. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

Here `/challenge/run` is an absolute path as it is invoked from the right directory.
<br>
I was wondering about what are the similarities and differences in Position Thy self, Position elsewhere and Position yet elsewhere. I could not found any differences except the variations in the location paths. Will try to look after some time.

## What I learned

1. Role of the current working directory
    - The shell prompt always shows where the shell is currently located.
    - Current working directory can be changed with commands like `cd`, which affects how relative paths are interpreted.

2. Interaction with challenge programs
    - Some programs need to be executed from specific directories like here from `/tmp`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / Position elsewhere module pages.


# Implicit relative paths, from /
In this challenge we have to use relative path instead of absolute path as in previous challenges. The task is to run the program `/challenge/run` but using a relative path while staying in the root directory `/`. Since challenge folder is directly under the root, the relative path would be `challenge/run`.

## My solution

**Flag:** `pwn.college{8D52wvZWPCwNcLrjYRIoPIc9DZ9.QX5QTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now execute the `challenge/run` command because to access challenge directory which is under root itself. Hence we can use without specifiying `/` which is used for absolute paths.
    ```bash
    hacker@paths~implicit-relative-paths-from-:/$ challenge/run
    Correct!!!
    challenge/run is a relative path, invoked from the right directory!
    Here is your flag:
    pwn.college{8D52wvZWPCwNcLrjYRIoPIc9DZ9.QX5QTN0wCO2kjNzEzW}
    ```

3. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

The challenge tests how relative paths change depending on cwd(current working directory).

- According to me - The hint provided : "your relative path starts with the letter c" confirmed that the path was `challenge/run`

- I also tried to execute `ls` command and i found the challenge directory which confirms the hint.
    ```bash
    hacker@paths~implicit-relative-paths-from-:/$ ls
    bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
    boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
    ```

## What I learned

1. Relative paths are depend on the current working directory
    - From `/` the relative path to the program is `challenge/run`.
    - From `/challenge` the relative path would be `run`.

2. Special notations in paths
    - `.` refers to the current directory.
    - `..` refers to the parent directory.

3. cwd is the directory that your prompt is currently located at and relative path is interpreted relative to your cwd.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths / Implicit relative paths, from / module pages.
- Got to know difference between `cwd` and `pwd` from a [QNA website](https://unix.stackexchange.com/questions/709896/what-is-the-difference-between-cwd-and-pwd). `pwd` prints the current working directory (a command) while `cwd` is like a concept that shows the current working directory.


# Explicit relative paths, from /
In this challenge we have to first go to root directory and from there run a relative path but using `.` which represents same directory. From `/` (the root), the relative path `challenge/run` and the explicit relative path `./challenge/run` both refer to the same file `/challenge/run`.

## My solution

**Flag:** `pwn.college{0iMuPP_SssrnyxhXqkQvvRT2KZU.QXwUTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Ensure I am at the root directory and confirm cwd
    ```bash
    hacker@paths~explicit-relative-paths-from-:~$ pwd
    /home/hacker
    hacker@paths~explicit-relative-paths-from-:~$ cd /
    hacker@paths~explicit-relative-paths-from-:/$ pwd
    /
    ```
3. Run the challenge program using one of them - here I have used `./challenge/run` — which is explicit relative from `/` to get the flag.
    ```bash
    hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
    Correct!!!
    ./challenge/run is a relative path, invoked from the right directory!
    Here is your flag:
    pwn.college{0iMuPP_SssrnyxhXqkQvvRT2KZU.QXwUTN0wCO2kjNzEzW}
    ```
4. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

Here any example can work as long as the explicit relative path points to same location...
```bash
hacker@paths~explicit-relative-paths-from-:/$ ././challenge/./run
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/././run
```
## What I learned

1. `.` explicitly shows the current-directory, `./file` is a relative path that starts from the cwd.

2. Special notations in paths
    - `.` refers to the current directory.
    - `..` refers to the parent directory.

3. Practical use-cases:
    - Using `./program` is good practise to ensure you do not run file with the same name on another location.
4. Redundancy is allowed
    - multiple `./` or `././` fragments are allowed and points to same cwd.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths /  Explicit relative paths, from / module pages.


# Implicit relative path
This level highlights an important Linux security feature: the current directory `.` is not automatically searched when running commands.  
That means if we are in `/challenge` and simply type `run`, Linux will not execute `./run`. In this challenge we have to go inside `challenge` directory and then execute the `run` command explicilty from that cwd.

## My solution

**Flag:** `pwn.college{QGREmlu87s3CqdFk9mw65Sf3HjY.QXxUTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Change into the `/challenge` directory
    ```bash
    hacker@paths~implicit-relative-path:~$ cd /challenge
    hacker@paths~implicit-relative-path:/challenge$
    ```
3. If we try to directly run the command it will show error.
    ```bash
    hacker@paths~implicit-relative-path:/challenge$ run
    bash: run: command not found
    ```
4. Run explicitly using `./` to reference the current directory
    ```bash
    hacker@paths~implicit-relative-path:/challenge$ ./run
    Correct!!!
    ./run is a relative path, invoked from the right directory!
    Here is your flag:
    pwn.college{QGREmlu87s3CqdFk9mw65Sf3HjY.QXxUTN0wCO2kjNzEzW}
    ```
5. The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/paths/) to complete the challenge.

This is intentional: if Linux always searched the current directory, attackers could trick users into running malicious programs named like system utilities (e.g., a fake `ls` in a download folder).  
Therefore to run a file in the current directory, you must explicitly tell the shell with `./`.

## What I learned
1. Linux does not auto-execute from cwd.
2. Security: This prevents accidental execution of malicious programs placed in user directories.
3. Always run local executables with `./`

## References 
- [pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering Paths /  Implicit relative path module pages.


