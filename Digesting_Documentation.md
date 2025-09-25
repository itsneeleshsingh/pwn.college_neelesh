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


# Reading Manuals
This challenge introduces the `man` command that has the official documentation for most installed commands.  
`man` displays a formatted manual page that typically contains important sections such as `NAME`, `SYNOPSIS`, `DESCRIPTION`, `OPTIONS`, and `SEE ALSO`. In this challenge `/challenge/challenge` contains a secret option documented in its manpage that will print the flag. We have to read its documentation, interpret and we get the flag.

## My solution
**Flag:** `pwn.college{MCDky4JXFv_SRnCc2_y8GrokEwm.QX0EDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now I opened the manual for the challenge program using `man` command.
    ```bash
    hacker@man~reading-manuals:~$ man challenge
    ```
3. Now it shows its manpage.
    ```bash
    CHALLENGE(1)                           Challenge Commands                          CHALLENGE(1)

    NAME
        /challenge/challenge - print the flag!

    SYNOPSIS
        challenge OPTION

    DESCRIPTION
        Output the flag when called with the right arguments.

        --fortune
                read a fortune

        --version
                output version information and exit

        --kyvncy NUM
                print the flag if NUM is 428
    (and so on...)
    ```
4. Now under `NAME` its written that `/challenge/challenge` will print the flag and under `DESCRIPTION` its written that `--kyvncy NUM` with NUM as 428 will print us with the flag. Now press q to quit from thre manpage and then run the following commands to get the flag.
    ```bash
    hacker@man~reading-manuals:~$ /challenge/challenge  --kyvncy 428
    Correct usage! Your flag: pwn.college{MCDky4JXFv_SRnCc2_y8GrokEwm.QX0EDO0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/man/) to complete the challenge.

My Mistake: I was in hurry and put 428 as the number after the NUM argument instead of replacing it.
```bash
hacker@man~reading-manuals:~$ /challenge/challenge  --kyvncy NUM 428
Incorrect usage! Please read the challenge man page!
```
## What I learned
1. `man` command basics - (short for manual) and it displays the manual of the command we pass as an argument.
2. It contains important sections such as `NAME`, `SYNOPSIS`, `DESCRIPTION`, `OPTIONS`, and `SEE ALSO`.
3. We can scroll around the manpage with arrow keys and PgUp/PgDn. After reading we can hit `q` to quit.
4. Manpages are stored in a centralized database under `/usr/share/man`. I tried to enter it in my machine. It showed me many functions list. I `cat` any one of them but it contained garbage values and some encrypted texts.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation / Reading Manuals module pages
- [Online repository of man pages](https://man7.org/linux/man-pages/) - Explored its pages.


# Searching Manuals
This challenge teaches how to search inside man pages. `man` supports searching with `/`or and `?`(for backward). In this challenge we have to open the manpage for the `challenge` program and search the manpage for the option that prints the `flag`, then run the program with that option.

## My solution
**Flag:** `pwn.college{UGAjUO1CccrzNd5i7O8xuXGjD-A.QX1EDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now I opened the manpage for the challenge program using `man`.
    ```bash
    hacker@man~searching-manuals:~$ man challenge
    ```
3. Now we have to search for the flag. Thus I pressed `/` and there was option to write, I entered `flag` and was confused how will it search. I pressed entered and it worked. It shows in highlighted text where the flag was written. It found the flag in 3 locations with lines :
    ```bash
    NAME
        /challenge/challenge - print the flag!
    ```
    ```bash
    DESCRIPTION
        Output the flag when called with the right argument.
    ```
    ```bash
        --errksy
                This argument will give you the flag!
    ``` 
4. Thus I got that `/challenge/challenge` with `--errksy` as argument will print the job. So i quit the manpage with q and executed the command.
    ```bash
    hacker@man~searching-manuals:~$ /challenge/challenge  --errksy
    Initializing...
    Correct usage! Your flag: pwn.college{UGAjUO1CccrzNd5i7O8xuXGjD-A.QX1EDO0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/man/) to complete the challenge.

We can also use `?` to search backwards. It works same as searching with `/`.

## What I learned
1. `man` with `/` is a fast way to find specific options or keywords in documentation.
2. `n` and `N` let us move forward/backward through matched keywords.
3. Instead of `/` we can use `?` to search backwards. I also tried the same challenge with that also. Works exactly same just backwards search.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation / Searching Manuals module pages


# Searching For Manuals
This challenge hides the manpage for the challenge behind a randomized manpage name. Using `man man`, We will get to know how to search for a manpage from databse. We have to find the randomly named manpage that documents the challenge, read it, then run `/challenge/challenge` with the option it has.

## My solution
**Flag:** `pwn.college{YaecsIufTFAXFusR5Hiyi7bPJ53.QX2EDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we have to read the man manual to learn how to search the manpage database. Thus we will search `man man` and will search for anything that searches the database.
    ```bash
    hacker@man~searching-for-manuals:~$ man man
    ```
3. After 5-6 minutes reading it, I discovered function that searches through manpage database.
    ```bash
        -k, --apropos
                Approximately  equivalent  to apropos.  Search the short manual page descriptions
                for keywords and display any matches.  See apropos(1) for details.
    ```
4. Thus using `-k` I searches for the keyword `challenge`. I found `aecsufusiy` as the only manpage. So I opened it again through its documentation.
    ```bash
    hacker@man~searching-for-manuals:~$ man -k challenge
    aecsufusiy (1)       - print the flag!
    hacker@man~searching-for-manuals:~$ man aecsufusiy
    ```
5. Now After reading, i got the command and the arguments to run, wwhich i run to get the flag.
    ```bash
    NAME
        /challenge/challenge - print the flag!

    SYNOPSIS
        challenge OPTION

    DESCRIPTION
        Output the flag when called with the right arguments.

        --fortune
                read a fortune

        --version
                output version information and exit

        --aecsuf NUM
                print the flag if NUM is 575
    ```
6. Thus i executed the `/challenge/challenge` command with `--aecsuf 575` as argument as listed in the manpage.
    ```bash
    hacker@man~searching-for-manuals:~$ /challenge/challenge  --aecsuf 575
    Correct usage! Your flag: pwn.college{YaecsIufTFAXFusR5Hiyi7bPJ53.QX2EDO0wCO2kjNzEzW}
    ```
7. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/man/) to complete the challenge.

Initially I gave more time from reading the `man man` manpage from starting, Instead i could directly jump into the `OPTIONS` section.

## What I learned
1. `man man` — read how to use man itself using the `man` command.
2. `man -k` or apropos to search the manpage index for any keyword provided.
3. Inside `man` use `/` to search, `n / N` to navigate matches, `q` to quit.(Practised it again)
4. Learned how to look for a specific feature argument in verly long manpages.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation / Searching For Manuals module pages