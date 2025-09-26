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


