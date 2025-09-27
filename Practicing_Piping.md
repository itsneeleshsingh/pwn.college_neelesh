# Practicing Piping
This module has 14 module that includes Redirecting output, Redirecting more output, Appending output, Redirecting errors, Redirecting input, Grepping stored results, Grepping live output, Grepping errors, Filtering with grep -v, Duplicating piped data with tee, Process substitution for input, Writing to multiple programs, Split-piping stderr and stdout and Named pipes.

# Redirecting output
This challenge teaches us - redirecting a command's standard output (stdout) into a file using `>`.In this challenge we have to write the word `PWN` into a file called `COLLEGE` in the current directory using output redirection.

## My solution
**Flag:** `pwn.college{k46ApWvlsZxP_XskdI-yKrsng5W.QX0YTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now write `echo PWN > COLLEGE` to write in the file COLLEGE.
    ```bash
    hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
    Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
    flag:
    pwn.college{k46ApWvlsZxP_XskdI-yKrsng5W.QX0YTN0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/piping/) to complete the challenge.

Note we can check the written file using `cat` command.
```bash
hacker@piping~redirecting-output:~$ cat COLLEGE
PWN
You have created the COLLEGE file and wrote the right value to it, but it
doesn't look like you did it via input redirection.
```

## What I learned
1. How to redirect stdout to a file with `>`. This redirects the shell output to a file.
2. Filenames on Linux are case-sensitive. we have to be careful with uppercase/lowercase.(in this case PWN and COLLEGE both were uppercase)
3. Also searched on google to find some other properties related to this and found that - Using `>` overwrites the file. If we wanted to add to an existing file, use `>>`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping / Redirecting output module pages
- Google for some extra properties.


# Redirecting more output
In this challenge - `/challenge/run` prints its flag on stdout. We have to capture only the stdout into the file `myflag` so the flag ends up in that file.

## My solution
**Flag:** `pwn.college{gVgayRzemwtyhATl1vsxhxDrdc8.QX1YTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we ghave to write `/challenge/run` but also store output in the file `myflag`.
    ```bash
    hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
    [INFO] WELCOME! This challenge makes the following asks of you:
    [INFO] - the challenge will check that output is redirected to a specific file path : myflag
    [INFO] - the challenge will output a reward file if all the tests pass : /flag

    [HYPE] ONWARDS TO GREATNESS!

    [INFO] This challenge will perform a bunch of checks.
    [INFO] If you pass these checks, you will receive the /flag file.

    [TEST] You should have redirected my stdout to a file called myflag. Checking...

    [PASS] The file at the other end of my stdout looks okay!
    [PASS] Success! You have satisfied all execution requirements.
    ```
3. Now we have to read the flag using `cat` command.
    ```bash
    hacker@piping~redirecting-more-output:~$ cat myflag

    [FLAG] Here is your flag:
    [FLAG] pwn.college{gVgayRzemwtyhATl1vsxhxDrdc8.QX1YTN0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/piping/) to complete the challenge.

**Note:** if we only run `/challenge/run` without storing into the file. We may not able to get our flag.
```bash
hacker@piping~redirecting-more-output:~$ /challenge/run
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[FAIL] You did not satisfy all the execution requirements.
[FAIL] Specifically, you must fix the following issue:
[FAIL]   You have not redirected anything for this process' stdout.
```

## What I learned
1. I learned how to redirect the shell output into the file itself without using predefined commands such as `echo`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping / Redirecting more output module pages


# Appending output
This challenge teaches the difference between truncating redirection `>` and append redirection `>>`. Now `/challenge/run` writes the first half of the flag to the file and the second half to stdout if stdout is redirected to a file.

## My solution
**Flag:** `pwn.college{QMjIAVyiVZo-z3hvRs4F_IeQ7Ef.QX3ATO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we have to run `/challenge/run` but through append mode so `>>` to `the-flag` sso we will get the whole flag.
    ```bash
    hacker@piping~appending-output:~$ /challenge/run >> the-flag
    [INFO] WELCOME! This challenge makes the following asks of you:
    [INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

    [HYPE] ONWARDS TO GREATNESS!

    [INFO] This challenge will perform a bunch of checks.
    [INFO] Good luck!

    [TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

    [HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
    [HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
    [HINT] creating and trying to pass in FDs in python.

    [PASS] The file at the other end of my stdout looks okay!
    [PASS] Success! You have satisfied all execution requirements.
    I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
    the first write directly to the file, and the second write, I'll do to stdout
    (if it's pointing at the file). If you redirect the output in append mode, the
    second write will append to (rather than overwrite) the first write, and you'll
    get the whole flag!
    ```
3. Now we have to read the flag using `cat` command.
    ```bash
    hacker@piping~appending-output:~$ cat the-flag
    |
    \|/ This is the first half:
    v
    pwn.college{QMjIAVyiVZo-z3hvRs4F_IeQ7Ef.QX3ATO0wCO2kjNzEzW}
                                ^
        that is the second half /|\
                                |

    If you only see the second half above, you redirected in *truncate* mode (>)
    rather than *append* mode (>>), and so the write of the second half to stdout
    overwrote the initial write of the first half directly to the file. Try append
    mode!
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/piping/) to complete the challenge.

Note that here if you run the output in normal stdout redirection mode that is in truncation mode, it will overwrite the second half on the first half.

## What I learned
1. `>` works aas truncation that is, it will create a new output file every time, deleting the old contents.
2. While `>>` just appends and redirect the output in the same file.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping / Appending output module pages
- Got to know from [How do I append text to a file?](https://stackoverflow.com/questions/17701989/how-do-i-append-text-to-a-file) that we can use `printf` directly in terminal as an alternative to `echo`.


# Redirecting errors
This challenge teaches us how to  redirect both standard output and standard error separately to files using file descriptor numbers. So we have to run `/challenge/run` so that - stdout that is the the flag goes into the file `myflag`, and stderr that is the instructions goes into the file instructions,and we get the flag in myflag.

## My solution
**Flag:** `pwn.college{EVJ6KprjFY68zI-hp8_enCLgjgg.QX3YTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now since we have to reduirect output into `myflag` we will use FD1 and for error/logs into `instructions` file we will use FD2...
    ```bash
    hacker@piping~redirecting-errors:~$ /challenge/run 1> myflag 2> instructions
    hacker@piping~redirecting-errors:~$
    ```
3. Now we can see using `ls` that two files are created.
    ```bash
    hacker@piping~redirecting-errors:~$ ls
    COLLEGE  Desktop  instructions  myflag  not-the-flag  t  the-flag
    ```
4. Now we can `cat` our file to get our flag.
    ```bash
    hacker@piping~redirecting-errors:~$ cat myflag

    [FLAG] Here is your flag:
    [FLAG] pwn.college{EVJ6KprjFY68zI-hp8_enCLgjgg.QX3YTN0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/piping/) to complete the challenge.

Now we can also use - `>` instead of `1>` as it is by default set to redirect to Standard Output.
```bash
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$
```

Also we can see what's written in `instructions` file.
```bash
hacker@piping~redirecting-errors:~$ cat instructions
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will check that error output is redirected to a specific file path : instructions
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!

[TEST] You should have redirected my stderr to instructions. Checking...

[PASS] The file at the other end of my stderr looks okay!
[PASS] Success! You have satisfied all execution requirements.
```

## What I learned
1. A File Descriptor (FD) is a number that describes a communication channel in Linux.
    - FD 0: Standard Input
    - FD 1: Standard Output
    - FD 2: Standard Error
2. `>` without a number implies `1>`.
3.  We can redirect multiple file descriptors at the same time.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping / Redirecting errors module pages. (It was enough)


# Redirecting input

This challenge teaches input redirection - feeding a file into a program as if its contents were typed on standard input. The redirection operator for this is `<`. So we have to `/challenge/run` its input from stdin.We have to create a file named `PWN` in which we have to write the word `COLLEGE`.
Then invoke `/challenge/run`, redirecting `PWN` into it via from stdin and then it gives us the flag.

## My solution
**Flag:** `pwn.college{Em6KSFj5oz-H199f6fwzsj7x8AV.QXwcTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now first I have to write `COLLEGE` inside filename `PWN` using previously used echo function.
    ```bash
    hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
    hacker@piping~redirecting-input:~$
    ```
3. Now we have to input redirect from the file `PWN` to `/challenge/run`.
    ```bash
    hacker@piping~redirecting-input:~$ /challenge/run < PWN
    Reading from standard input...
    Correct! You have redirected the PWN file into my standard input, and I read
    the value 'COLLEGE' out of it!
    Here is your flag:
    pwn.college{Em6KSFj5oz-H199f6fwzsj7x8AV.QXwcTN0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/piping/) to complete the challenge.

## What I learned
1. `<` redirects a file into a programs standard input (FD 0).
2. Reuse of `echo > file` as in the previous challenges.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping / Redirecting input module pages.
- Just out of curiosity reading [this](https://askubuntu.com/questions/883786/how-does-input-redirection-work) and here found how `ls file1` and `ls < file1` behaves.
    ```bash
    $ ls
    file1  file2
    $ ls file1   ## lists only file1: ls takes file names as arguments
    file1
    $ ls < file1 ## ls ignores its standard input, this is the same as ls alone
    file1 file2
    ```

