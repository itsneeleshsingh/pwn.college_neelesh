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