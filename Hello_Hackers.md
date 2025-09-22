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
2. Now the shell is connected to dojo. Now on typing `hello` and clicking on Enter, We get the flag that we can submit on [pwn.college](https://pwn.college/linux-luminarium/hello/) to complete the challenge.
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
