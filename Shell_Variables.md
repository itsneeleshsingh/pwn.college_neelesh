# Shell Variables
This module contains 8 modules that includes Printing Variables, Setting Variables, Multi-word Variables, Exporting Variables, Printing Exported Variables, Storing Command Output, Reading Input and Reading Files.


# Printing Variables
 The program `/challenge/run` doesn't print the flag, but the flag is stored in a shell variable named `FLAG`. Print it to retrieve the flag.


## My solution
**Flag:** `pwn.college{gHvkCMiKRdFAVBFqZID717Et3Sr.QX3UTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now we have to retrieve the flag using `echo` function and adding `$` before the variable name `FLAG`.
    ```bash
    hacker@variables~printing-variables:~$ echo $FLAG
    pwn.college{gHvkCMiKRdFAVBFqZID717Et3Sr.QX3UTN0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

## What I learned
1. Shell variables are accessed with `$VAR` with prepend letter `$`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Printing Variables module pages


# Setting Variables
Set the variable `PWN` to the value `COLLEGE`.

## My solution
**Flag:** `pwn.college{Agvw5Pjth--eC5_g_52orS7kS7Y.QX5UTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we have to assign value to variable.
    ```bash
    hacker@variables~setting-variables:~$ PWN=COLLEGE
    You've set the PWN variable properly! As promised, here is the flag:
    pwn.college{Agvw5Pjth--eC5_g_52orS7kS7Y.QX5UTN0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

**Note:** here if you will give space before or after `=` then we you will get error as it will treat it like command.
```bash
hacker@variables~setting-variables:~$ PWN = COLLEGE
bash: PWN: command not found

You put spaces around your '=' in your assignment! This caused the shell to
execute the 'PWN' command instead of assigning it to the environment variable
as you intended. Try again without spaces around '='!
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{Agvw5Pjth--eC5_g_52orS7kS7Y.QX5UTN0wCO2kjNzEzW}
```

## What I learned
1. We can assign value to a variable with `NAME=value`.
2. Variable names and values are case-sensitive.
3. Do not add spaces before or after the `=` because it will treat it like command.
4. No need to mention `$` while appending.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Setting Variables module pages


# Multi-word Variables
Set the variable `PWN` to the value `COLLEGE YEAH`.

## My solution
**Flag:** `pwn.college{8RFizxWZ322TYCkAwioNGfSj2MA.QXwYTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now since i have to add multiple word value into variable, i need to use `""`.
    ```bash
    hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
    You've set the PWN variable properly! As promised, here is the flag:
    pwn.college{8RFizxWZ322TYCkAwioNGfSj2MA.QXwYTN0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

## What I learned
1. To add multi word value to variable we have to specify it under quotation marks.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Multi-word Variables module pages


# Exporting Variables
In this challenge we have to invoke `/challenge/run` with:
- `PWN` exported and set to `COLLEGE`
- `COLLEGE` set to `PWN` in the current shell but not exported.

## My solution
**Flag:** `pwn.college{g_uUPqCumCPXKV_gzgnFyua2BKM.QXyYTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we create the variable `PWN` and value as `COLLEGE` and export it.
    ```bash
    hacker@variables~exporting-variables:~$ PWN=COLLEGE
    You've set the PWN variable to the proper value!
    hacker@variables~exporting-variables:~$ export PWN
    You've set the PWN variable to the proper value!
    You've set the COLLEGE variable to the proper value!
    ```
3. Now set `COLLEGE` variable and value to `PWN` but we do not have to export it.
    ```bash
    hacker@variables~exporting-variables:~$ export PWN
    You've set the PWN variable to the proper value!
    You've set the COLLEGE variable to the proper value!
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

## What I learned
1. Assignment without export keeps the variable local to the current shell.
2. export NAME=value makes NAME visible to child processes that is - it adds it to environment variables.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Exporting Variables module pages


# Printing Exported Variables
Find the `FLAG` variable among exported environment variables.

## My solution
**Flag:** `pwn.college{Q1Naku2MAuqqkTaEfSxDA1FKoUh.QX4UTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now execute `env` to get list of all environment variables and find flag in it.
    ```bash
    hacker@variables~printing-exported-variables:~$ env
    SHELL=/run/dojo/bin/bash
    HOSTNAME=variables~printing-exported-variables
    PWD=/home/hacker
    MANPATH=/run/dojo/share/man:
    DOJO_AUTH_TOKEN=109cd69edcd3d1d500f0f2ea92de18ff39d0f4bd617987220ca47145b08fc1dd
    HOME=/home/hacker
    LANG=C.UTF-8
    FLAG=pwn.college{Q1Naku2MAuqqkTaEfSxDA1FKoUh.QX4UTN0wCO2kjNzEzW}
    TERMINFO=/run/dojo/share/terminfo
    TERM=xterm-256color
    SHLVL=2
    LC_CTYPE=C.UTF-8
    SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
    PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    DEBIAN_FRONTEND=noninteractive
    _=/run/dojo/bin/env
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

Note: We can also use `grep` in this.
```bash
hacker@variables~printing-exported-variables:~$ env | grep pwn.college
FLAG=pwn.college{Q1Naku2MAuqqkTaEfSxDA1FKoUh.QX4UTN0wCO2kjNzEzW}
```

## What I learned
1. `env` is used to print all the environment variables stored at once.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Printing Exported Variables module pages


# Storing Command Output
Read the output of `/challenge/run` directly into a variable named `PWN` so it contains the flag.

## My solution
**Flag:** `pwn.college{8uc63JGF7ZleaKJmhCJhFFd2Y_t.QX1cDN1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now first we will run the ecommand `/challenge/run` and store it in `PWN` variable.
    ```bash
    hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
    Congratulations! You have read the flag into the PWN variable. Now print it out
    and submit it!
    ```
3. Now print the value stored in the variable.
    ```bash
    hacker@variables~storing-command-output:~$ echo $PWN
    pwn.college{8uc63JGF7ZleaKJmhCJhFFd2Y_t.QX1cDN1wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

## What I learned
1. Command Substitution is used to store the output of some command into a variable.
2. Use $(...) over `...` for command substitution. 

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Storing Command Output module pages


# Reading Input
Use `read` to set the `PWN` variable to `COLLEGE`.

## My solution
**Flag:** `pwn.college{41aQDNzL9paydQ31gVkrWXVF_EU.QX4cTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we have to input the `COLLEGE` value into `PWN` variable using `read`.
    ```bash
    hacker@variables~reading-input:~$ read -p "Enter:" PWN
    Enter:COLLEGE
    You've set the PWN variable properly! As promised, here is the flag:
    pwn.college{41aQDNzL9paydQ31gVkrWXVF_EU.QX4cTN0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

## What I learned
1. `read` reads from standard input into shell variables.
2. `-p` argument, which lets you specify a prompt.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Reading Input module pages.


# Reading Files
The challenge asks us to read the contents of `/challenge/read_me` directly into a variable called `PWN`. Unlike earlier where we used $(cat file) to capture file contents, this time we learn a cleaner way using the read builtin with input redirection `<`.

## My solution
**Flag:** `pwn.college{Qcpd-KDHo_fbQ6RsJJuYuJE49Gn.QXwIDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we will input the `/challenge/read_me` as input into the `PWN`.
    ```bash
    hacker@variables~reading-files:~$ read PWN < /challenge/read_me
    You've set the PWN variable properly! As promised, here is the flag:
    pwn.college{Qcpd-KDHo_fbQ6RsJJuYuJE49Gn.QXwIDO0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/variables/) to complete the challenge.

## What I learned
1. Files can be read directly into variables using the `<` operator without needing external tools like `cat`.
2. Both the variable name PWN and the expected value COLLEGE are case-sensitive.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables / Reading Files module pages.
