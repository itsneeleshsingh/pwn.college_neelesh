# File Globbing
This module contains 10 challenges including Matching with , Matching with ?, Matching with [], Matching paths with [], Multiple globs, Mixing globs, Exclusionary globbing, Tab completion, Multiple options for tab completion and Tab completion on commands.

# Matching with *
This challenge teaches the shell glob: `*`. When the shell sees a `*` in an argument it will expand that pattern to any filenames that match.In this challenge we have to start from our home directory and change directory to `/challenge` without giving 4 characters long path to `cd`. Then run `/challenge/run` to get the flag.

## My solution
**Flag:** `pwn.college{IDP7XiDnCTclNld3p7VKhf7NAEQ.QXxIDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now I used a 4-character glob to cd into `/challenge` that is `cd /ch*`.
    ```bash
    hacker@globbing~matching-with-:~$ cd /ch*
    hacker@globbing~matching-with-:/challenge$
    ``
3. Now we can run `/challenge/run` to get our flag.
    ```bash
    hacker@globbing~matching-with-:/challenge$ /challenge/run
    You ran me with the working directory of /challenge! Here is your flag:
    pwn.college{IDP7XiDnCTclNld3p7VKhf7NAEQ.QXxIDO0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/globbing/) to complete the challenge.

**Note:** here maximum limit is 4 characters thus ` cd /cha*` will not work.

## What I learned
1. `*` is a wildcard that matches any string (except `/` and leading `.`)
2. Researched what is `glob` - A glob is a string pattern, used for matching file and directory names on a computer, that includes literal characters and wildcards.
3. Globs are expanded by the shell before a command runs.
4. A glob may match multiple names,  if that happens the shell will pass multiple arguments. We can `echo` it as given in challenge documentation. Or if none match, shell leave the pattern unchanged.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing / Matching with * module pages
- Google (to search glob definition)


# Matching with ?
This challenge teaches the single-character glob `?`, which matches exactly one character.In this challenge we have to execute `cd` into `/challenge`, but in the argument we cannot write `c` and `l`. Once done we can run `/challenge/run` to get the flag.

## My solution
**Flag:** `pwn.college{s27WjWlO8pdxskmuoytMiqiWFup.QXyIDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we have to use `?` instead of words that are not allowed to be used. Thus we can write - `cd /?ha??enge` which will do the job.
    ```bash
    hacker@globbing~matching-with-:/$ cd /?ha??enge
    hacker@globbing~matching-with-:/challenge$
    ```
3. Now we can run our program to get the flag.
    ```bash
    hacker@globbing~matching-with-:/challenge$ /challenge/run
    You ran me with the working directory of /challenge! Here is your flag:
    pwn.college{s27WjWlO8pdxskmuoytMiqiWFup.QXyIDO0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/globbing/) to complete the challenge.

**Note** that here any combination can be used which is correct but logically incorrect according to the challenge. For example `cd /?????enge` this is also correct.
```bash
hacker@globbing~matching-with-:~$ cd /?????enge
hacker@globbing~matching-with-:/challenge$
```

## What I learned
1. `?` matches exactly one character.(single-character wildcard)
2. Combine multiple ? to match multiple single characters.(in this challenge)
3. Mixed searches with `*` and `?` can also be used.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing / Matching with ? module pages


# Matching with []
This challenge teaches bracket globs `[]`, which matches exactly one character from a given subset. In this challenge we have to change directory to `/challenge/files` and run `/challenge/run` with a single argument that bracket-globs into the four files - `file_b, file_a, file_s, and file_h`.

## My solution
**Flag:** `pwn.college{obNyIiRb9Qrb6JZ9zihnS3gk-Xt.QXzIDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. I changed to the challenge files directory.
    ```bash
    hacker@globbing~matching-with-:~$ cd /challenge/files/
    hacker@globbing~matching-with-:/challenge/files$
    ```
3. I tried to check which files are there. On using `ls` I got to know that there were many files.
    ```bash
    hacker@globbing~matching-with-:/challenge/files$ ls
    file_a  file_d  file_g  file_j  file_m  file_p  file_s  file_v  file_y
    file_b  file_e  file_h  file_k  file_n  file_q  file_t  file_w  file_z
    file_c  file_f  file_i  file_l  file_o  file_r  file_u  file_x
    ```
4. Now since we have to run commands only with thode file names. We can put `file_[bash]` for files `file_b, file_a, file_s, and file_h`.
    ```bash
    hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
    You got it! Here is your flag!
    pwn.college{obNyIiRb9Qrb6JZ9zihnS3gk-Xt.QXzIDO0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/globbing/) to complete the challenge.

Here we do not mentioned absolute paths for `file_[bash]` because our cwd was `/challenge/files` itself, which contained all the files.

## What I learned
1. `[]` matches one character from a set we provide. Also written in challenge documentation - `is a wildcard for some subset of potential characters, specified within the brackets.`

## References 
- [pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing / Matching with [] module pages
