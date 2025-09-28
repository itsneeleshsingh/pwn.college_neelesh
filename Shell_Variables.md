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