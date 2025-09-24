# Digesting Documentation
This module contains 7 challenges that include Learning From Documentation, Learning Complex Usage, Reading Manuals, Searching Manuals, Searching For Manuals, Helpful Programs and Help for Builtins.

# Learning From Documentation
This challenge emphasizes the importance of reading the documentation. Programs accept arguments that change their behavior.

> _Welcome to the documentation for /challenge/challenge! To properly run this program, you will need to pass it the argument of `--giveflag`. Good luck!_

Thus after reading the documentation we have to run `/challenge/challenge --giveflag`.

## My solution
**Flag:** `pwn.college{0Jy2NO9XwJzdgxJgWG4I8osgBmu.QX0ITO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Run the program with the documented argument.
    ```bash 
    hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
    Correct argument! Here is your flag:
    pwn.college{0Jy2NO9XwJzdgxJgWG4I8osgBmu.QX0ITO0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/man/) to complete the challenge.

The program expects a long-form option `--giveflag`. Long options start with `--` and are typically more descriptive than single letter options.

- If you will not pass argument it will give you an error. It means you havent read the documentation properly.
    ```bash
    hacker@man~learning-from-documentation:~$ /challenge/challenge
    Incorrect usage! You must pass an argument to me (read the challenge
    description for details).
    ```

## What I learned
1. Read the documentation first. The docs often tell us exactly which arguments to pass.
2. Long arguments like `--giveflag` or anything are common and clearer than single letter options.
3. We should try the inbuilt documentation of the commands using `--help` command.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation / Learning From Documentation module pages [This was the only documentation that we have to refer in this challenge]


# Learning Complex Usage
In this challenge we have to invoke `/challenge/challenge` with `--printfile` and pass it the path to the flag (for example `/flag`) so the program prints the flag.

## My solution
**Flag:** `pwn.college{s7NIk5Nt7FqODQKZ0HO1jsGeChF.QX1ITO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Run the program with the `--printfile` option pointing at the flag file.
    ```bash
    hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
    Correct argument! Here is the /flag file:
    pwn.college{s7NIk5Nt7FqODQKZ0HO1jsGeChF.QX1ITO0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/man/) to complete the challenge.

Here I first tried the first command given in documentation.
```bash
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /challenge/DESCRIPTION.md
Correct argument! Here is the /challenge/DESCRIPTION.md file:
(and so on.....)
```
## What I learned
1. Arguments can take arguments. Like in this case after `--printfile` we have to mention path also as an argument.
2. More practise of writing longer commands like `--printfile`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation / Learning Complex Usage module pages
