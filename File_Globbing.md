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


# Matching paths with []
This challenge shows that globs apply to path components which means that we can use bracket globs inside full absolute paths.In this challenge we have to run command from our home directory, run `/challenge/run` with a single argument that bracket-globs into the absolute paths for four files: `file_b, file_a, file_s, and file_h`.

## My solution
**Flag:** `pwn.college{gmHc4yCPLthwKVXM2wKsap9zaqe.QX0IDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. So we have to run the challenge program with that single glob argument - that is ` /challenge/files/file_[bash]` that is absolute path.
    ```bash
    hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
    You got it! Here is your flag!
    pwn.college{gmHc4yCPLthwKVXM2wKsap9zaqe.QX0IDO0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/globbing/) to complete the challenge.

**Note:** that here we have to run the command through home directory. By mistake i executed it through `/challenge/files`.
```bash
hacker@globbing~matching-paths-with-:~$ cd /challenge/files/
hacker@globbing~matching-paths-with-:/challenge/files$ /challenge/run /challenge/files/file_[bash]
Error: please run with a working directory of /home/hacker!
hacker@globbing~matching-paths-with-:/challenge/files$ cd ~
hacker@globbing~matching-paths-with-:~$
```

## What I learned
1. Bracket `[]` patterns also work inside absolute paths as inside filenames.
2. The bracket expression `[bash]` matches one character in that set (b, a, s, h).
3. We are passing one argument to `/challenge/run` but the shell expands that into four pathnames before the program runs.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing / Matching paths with [] module pages
- Only small part i read from [Matching paths with []](https://www.files.com/docs/automations/matching-source-path-and-filenames) and found that for series matchin we can use - `[a-d]` for all letters a to d matching instead of writing manually.


# Multiple globs
This challenge teaches that a single word may contain multiple glob. In this challnege first we have to change directory to `/challenge/files`, then run `/challenge/run` with one argument - a 3 characters or less globbed word that contains two `*` globs and matches every filename that contains the letter `p` in that directory.

## My solution
**Flag:** `pwn.college{kpzkSDkOBJXhvo-wmJqCXGiKJfl.0lM3kjNxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. First we have to Change into the files directory.
    ```bash
    hacker@globbing~multiple-globs:~$ cd /challenge/files/
    hacker@globbing~multiple-globs:/challenge/files$
    ```
3. We can see all the files.
    ```bash
    hacker@globbing~multiple-globs:/challenge/files$ ls
    amazing      educational  incredible  magical     queenly    uplifting   youthful
    beautiful    fantastic    jovial      nice        radiant    victorious  zesty
    challenging  great        kind        optimistic  splendid   wonderful
    delightful   happy        laughing    pwning      thrilling  xenial
    ```
4. Now we have to run the `/challenge/run` but with all the files that contains `p`. This can be done with `*p*` which means that before p and after p anything can be there.
    ```bash
    hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
    You got it! Here is your flag!
    pwn.college{kpzkSDkOBJXhvo-wmJqCXGiKJfl.0lM3kjNxwCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/globbing/) to complete the challenge.

Here the `*p*` is less than 3 characters which ssatisfy the condition provided.

## What I learned
1. We can place multiple globs inside a single word.
2. `*x*` is an common approach to match filenames that contain single letter `x`. Here x may not be a single letter, it can be substring also.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing / Multiple globs module pages


# Mixing globs
This challenge combines the previous globbing techniques to create a single short pattern that matches multiple files with different names. In this challenge we have to change directory into `/challenge/files`, then run `/challenge/run` with one glob argument with less than 6 characters that matches the files - `challenging` , `educational` and `pwning`.

## My solution
**Flag:** `pwn.college{8K2lbeRQMDO7P97eQCaTpLjAKXm.QX1IDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. So first we have to change directory.
    ```bash
    hacker@globbing~mixing-globs:~$ cd /challenge/files/
    hacker@globbing~mixing-globs:/challenge/files$
    ```
3. Now try to guess the pattern. First i though that `i` and `n` was common in all of them. So i executed it. But apart from it it also matached with some other.
    ```bash
    hacker@globbing~mixing-globs:/challenge/files$ /challenge/run *[in]*
    Your expansion did not expand to the requested files (challenging, educational,
    pwning). Instead, it expanded to:
    amazing beautiful challenging delightful educational fantastic incredible jovial kind laughing magical nice optimistic pwning queenly radiant splendid thrilling uplifting victorious wonderful xenial
    ```
4. So after some more thoughts i decided to match only the first letter with all three files name and all others can be anything. So i executed `[cep]*` which is 6 characters and matches with first letter of all 3 file names.
    ```bash
    hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
    You got it! Here is your flag!
    pwn.college{8K2lbeRQMDO7P97eQCaTpLjAKXm.QX1IDO0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/globbing/) to complete the challenge.

Note here multiple answers can be correct that matches with ONLY those 3 filenames and not matches with any.

## What I learned
1. Globs can be combined to match multiple files with different names.
2. This question was there to build the logic and to test thinking capabilities.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing / Mixing globs module pages


# Exclusionary globbing
This challenge introduces globbing with `[]` but in opposite manner that is exclusion.  
But if the first character is `!` or `!`, the meaning is inverted — it matches any character not listed. So we have to navigate to `/challenge/files` and run `/challenge/run` with a single glob argument that matches all files that do not start with - `p`, `w` and `n`.

## My solution
**Flag:** `pwn.college{Y7lqjvGHh7Dur2Rwg1JUCU4ixnA.QX2IDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. So first we have to go to `/challenge/files` directory.
    ```bash
    hacker@globbing~exclusionary-globbing:~$ cd /challenge/files/
    hacker@globbing~exclusionary-globbing:/challenge/files$
    ```
3. Now we have to run in such a way that files which do not have starting with `p`, `w` and `n` are there. So we can write - `[!pwn]*`.
    ```bash
    hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
    You got it! Here is your flag!
    pwn.college{Y7lqjvGHh7Dur2Rwg1JUCU4ixnA.QX2IDO0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/globbing/) to complete the challenge.

**Note:** Here `^` will also work.
```bash
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{Y7lqjvGHh7Dur2Rwg1JUCU4ixnA.QX2IDO0wCO2kjNzEzW}
```
## What I learned
1. Exclusionary globbing allows filtering files by excluding characters which is useful when we want to avoid certain prefixes while keeping the rest.
2. The `!` must be the first character inside the brackets as it has a different special meaning in bash.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing / Exclusionary globbing module pages
