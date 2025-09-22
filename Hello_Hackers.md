# Hello Hackers
This module contains three challenges that includes Intro to Commands, Intro to Arguments and Command History

# Intro to Commands
The challenge asks to invoke the `hello` command to retrieve the module flag. 
Since the Linux commands are case sensitive, thus we should run exactly the same way in the shell to get the flag.

## My solution
**Flag:** `pwn.college{g4yaXFF365j7pf6W0H9hOWxGD9r.QX3YjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now on typing `hello` and clicking on Enter, I get the flag that I can submit on [pwn.college](https://pwn.college/linux-luminarium/hello/) to complete the challenge.
    ```bash
    hacker@hello~intro-to-commands:~$ hello
    Success! Here is your flag:
    pwn.college{g4yaXFF365j7pf6W0H9hOWxGD9r.QX3YjM1wCO2kjNzEzW}
    ```
**Note:** Here We have to be cautious while writing commands as Linux filenames and command names are case-sensitive.

- Since we have to invoke the command `hello`, I assumed that there is a pre defined command set by pwn.college.
- Also we have to take care to START the challenge first on pwn.college and then execute the command.

## What I learned
1. Basic structure of linux commands.
    - Every command in shell follows a structure like - `whoami`
    - and we can execute the commands with Enter key.
    - When command is entered, the shell invokes it and performs the operation and prints the output.
    - After execution shell prompt reappears for next command.
2. Commands in Linux are case sensitive.
    - `hello` will work while all others like `Hello` or `HELLO` will not work in this particular case.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/hello/) - Hello Hackers / Intro to Commands module pages
- [Basic writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) - To refer some markdown elements like nested points/lists


# Intro to Arguments
The challenge asks to run the `hello` command but this time with an argument that is `hackers`.
Instead of just typing `hello` that is a single command, we have to write command + argument that is `hello hackers`.

## My solution
**Flag:** `pwn.college{g4CgO5T_DvafOLCxxGOVG1UkQ4H.QX4YjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. I typed the command `hello hackers`
    ```bash
    hacker@hello~intro-to-arguments:~$ hello hackers
    Success! Here is your flag:
    pwn.college{g4CgO5T_DvafOLCxxGOVG1UkQ4H.QX4YjM1wCO2kjNzEzW}
    ```
3.  The flag appeared on the screen, which I then copied and submitted on [pwn.college](https://pwn.college/linux-luminarium/hello/) to complete the challenge.


**My mistake:** When i was connecting the SSH I was not in the directory where my private key was.
```bash
neel@NeelTech:~/pwn.college_neelesh$ ssh -i ./key hacker@dojo.pwn.college
Warning: Identity file ./key not accessible: No such file or directory.
hacker@dojo.pwn.college: Permission denied (publickey).
```
Thus I corrected it by coming out of that directory and executing the same command again...
```bash
neel@NeelTech:~/pwn.college_neelesh$ cd ..
neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
Connected!
```

- The challenge asked not to use `echo hackers` because echo simply prints arguments and will not provide the flag.

## What I learned

1. Commands and arguments structure
    - Command - first word (In our case `hello`)
    - Argument - They are additional values passed to commands (in this case `hackers`)
2. Difference in commands
    - On running `hello hackers` it returns flag for the input as the challenge says.
    - But on running `echo hackers`, it only prints the text as the echo function just prints the argument provided after it.
3. Concept of multiple arguments
    - Some commands can accept multiple arguments like - `echo Hello Hackers!`
    - But in our case we need only one argument.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/hello/) - Hello Hackers / Intro to Arguments module pages
- Just went through a part of [Linux arguments](https://www.w3resource.com/linux-system-administration/commands-and-arguments.php) - Got to know how arguments are taken and whitespaces are removed during execution.