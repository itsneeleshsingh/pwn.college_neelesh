# Comprehending Commands
This module contains 14 challenges that includes cat: not the pet, but the command!, catting absolute paths, more catting practice, grepping for a needle in a haystack, comparing files, listing files, touching files, removing files, moving files, hidden files, An Epic Filesystem Quest, making directories, finding files, Symbolic Links and linking files.

# Comprehending Commands
`cat` - short for *concatenate* is most commonly used to print file contents to the terminal. It can also concatenate multiple files or read from standard input if given no filenames. In this challenge the flag is stored and copied into a file in our home directory. Our task is to read that file using `cat`.

## My solution
**Flag:** `pwn.college{gWb-UmMf2GFb1z_bzUfqLfvLn8V.QXxcTN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Read the flag file with `cat` and `flag` as argument to it.
    ```bash
    hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
    pwn.college{gWb-UmMf2GFb1z_bzUfqLfvLn8V.QXxcTN0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/commands/) to complete the challenge.

Also we can check if we are in home directory or not and is the flag present with `pwd` and `ls` commands.
```bash
hacker@commands~cat-not-the-pet-but-the-command:~$ pwd
/home/hacker
hacker@commands~cat-not-the-pet-but-the-command:~$ ls
Desktop  flag  t
```

## What I learned
1. Basic usage of cat — printing file contents and concatenating files
2. `cat` can concatenate multiple files as written in the dojo description - `cat will concatenate (hence the name) multiple files if provided multiple arguments.`
3. If we give no arguments at all, cat will read from the terminal input and output it.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/commands/) - Comprehending Commands / cat: not the pet, but the command! module pages
- Watched a short [video](https://www.youtube.com/watch?v=C1btVko0CVE) to get some more arguments like `ls -a` and `ls -l`.


# Catting absolute paths
The challenge asks us to enter `cat` argument as an absolute path. So here the flag is not copied but we can read it from the absolute path which is under the root directory `/flag`.

## My solution
**Flag:** `pwn.college{M6Uf6P27xg9n73ArA46hkjaFDNN.QX5ETO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Read the flag using the absolute path `/flag` with `cat`
    ```bash
    hacker@commands~catting-absolute-paths:~$ cat /flag
    pwn.college{M6Uf6P27xg9n73ArA46hkjaFDNN.QX5ETO0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/commands/) to complete the challenge.

Here flag was not there in the hom directory.
```bash
hacker@commands~catting-absolute-paths:~$ ls
Desktop  t
```
## What I learned
1. Absolute vs Relative:
    - Absolute: `/flag` always refers to the same file regardless of cwd.
    - Relative: `flag` interpreted relative to our current working directory.
2. `cat` can take absolute path arguments as well as relative(previous challenge).

## References 
- [pwn.college](https://pwn.college/linux-luminarium/commands/) - Comprehending Commands / Catting absolute paths module pages


# More catting practice
In this challenge we have to read files with `cat` using absolute paths — but we dont know the location where it is.

## My solution
**Flag:** `pwn.college{U1SrFSMqS1Gw7yqfF9mJRUI1fNt.QXwITO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. But here there is condition that we cannot use `cd` that means we cannot simply change into the directory and use a relative path like `cat flag`. Thus I tried to write any random relative path.
    ```bash
    hacker@commands~more-catting-practice:~$ cd flag
    You used 'cd'! In this level, I don't allow you to change the working directory
    --- you MUST chase pass 'cat' the absolute path of where I put it on the
    filesystem (which is /lib/llvm-10/flag).
    ```
3. Thus we get to know that the absolute path is `/lib/llvm-10/flag`.
    ```bash
    hacker@commands~more-catting-practice:~$ cat /lib/llvm-10/flag
    pwn.college{U1SrFSMqS1Gw7yqfF9mJRUI1fNt.QXwITO0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/commands/) to complete the challenge.

My mistake was just I tried to `cat` flag directly instead i have to try any random `cd` command.
```bash
hacker@commands~more-catting-practice:~$ cat flag
cat: flag: No such file or directory
```

## What I learned
1. `cd` restrictions dont block absolute path usage.
2. Absolute paths proved to be better ONLY in this case than relative paths. Even without changing directories, we can always reference the exact file location.
3. We can use tab key to autocomplete directory - which I tried.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/commands/) - Comprehending Commands / More catting practice module pages


# Grepping for a needle in a haystack
In this challenge we have to use `grep` function. `grep` scans files line by line for text matching the given string or set of words and prints matching lines.

## My solution
**Flag:** `pwn.college{kpN-701uCggM27tZB3obSPoBO6A.QX3EDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. So we will write `pwn.college` which is argument to search for in the file `/challenge/data.txt` as 2nd argument to the `grep` command.
    ```bash
    hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
    pwn.college{kpN-701uCggM27tZB3obSPoBO6A.QX3EDO0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/commands/) to complete the challenge.

Here flag was not printed or stored in a single file. There was a filee with hundreds thousands of lines. So grep allowed to search the flag using string matching.

## What I learned
1. `grep` basics — how to find lines that contain a search string in large files.
2. Got to know about its implementation - where we have to search some parrticular piece of text from a bunch of lines and texts.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/commands/) - Comprehending Commands / Grepping for a needle in a haystack module pages   
- Just learned some 2-3 more arguments from [grep command](https://www.geeksforgeeks.org/linux-unix/grep-command-in-unixlinux/) like `grep -c` to count the number of lines it matches with the given string.


# Comparing files
In this challenge we have to use `diff` command. `diff` is useful when you want to find small differences across large files like spotting the single real flag among many decoys in this case.

## My solution
**Flag:** `pwn.college{4VilRrjuTlAfvdo1K4u1glcbvn9.01MwMDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. `/challenge/decoys_only.txt` contains 100 fake flags.  
and `/challenge/decoys_and_real.txt` contains those 100 fake flags **plus** one real flag. Thus use `diff`  with specifying both the files to get the flag as that is what the difference between the flag is..
    ```bash
    hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
    8a9
    > pwn.college{4VilRrjuTlAfvdo1K4u1glcbvn9.01MwMDOxwCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/commands/) to complete the challenge.

Here I used the tab key to autocomplete the path. That saves time when the paths are long specially cases like this one.
- Also `8a9` shows that the file `/challenge/decoys_and_real.txt` contained the real extra flag on the line 9.

## What I learned
1. How to read `diff` between two files.
2. `8a9` in this case showed the difference in the line 9 of `/challenge/decoys_and_real.txt` compared to after line 8 of `/challenge/decoys_only.txt`.
3. Here in `diff`, absolute paths are provided. On searching on internet - I got to know that we can also provide relative paths to the `diff` command.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/commands/) - Comprehending Commands / Comparing files module pages   


# Listing files
In this challenge the `/challenge/run` is renamed to any other name. We have to explore the file names under the `/challenge` directory. Thus using `ls` command we can find the renamed program and can run using its path.

## My solution
**Flag:** `pwn.college{Y86GSKPgSPPx9qe_vQxbWs7ANbO.QX4IDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Therefore to search under `challenge` path we can use `ls` command for that and challenge as an argument.
    ```bash
    hacker@commands~listing-files:~$ ls /challenge
    2373-renamed-run-9470  DESCRIPTION.md
    ```
3. Now `2373-renamed-run-9470` is most probably the program as it was mentioned that the program was renamed. Thus we have to run it normally using absolute path.
    ```bash
    hacker@commands~listing-files:~$ /challenge/2373-renamed-run-9470
    Yahaha, you found me! Here is your flag:
    pwn.college{Y86GSKPgSPPx9qe_vQxbWs7ANbO.QX4IDO0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/commands/) to complete the challenge.

Here I tried to use `grep` function in it. But it is only useful when we know the name of the file. Thus here it shows that it is a directory.
```bash
hacker@commands~listing-files:~$ grep pwn.college /challenge/
grep: /challenge/: Is a directory
```
## What I learned
1. `ls` is the primary discovery tool for finding files and directories that lists out the files and folders.
2. I noticed that only directories were showing. Thus after some research i got to know that we can use `ls --all` to get all the files and folers with hidden files starting with `.` dot.
3. If we only write `ls` - It shows the files and folders of the cwd while we can provide any relative or absolute path in it.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/commands/) - Comprehending Commands / Listing files module pages   


# Touching files
This challenge teaches how to create empty files with the `touch` command. `touch` is a command to create empty file with the name passed on argument.
In this challenge we have to create two files `/tmp/pwn` and `/tmp/college` and then execute the `challenge/run` program to get the flag.

## My solution
**Flag:** `pwn.college{s7rtLMruOyesMLOR6WEQBXE5jJM.QXwMDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we have to create the two required files with `touch`.
    ```bash
    hacker@commands~touching-files:~$ touch /tmp/pwn
    hacker@commands~touching-files:~$ touch /tmp/college
    ```
3. We can verify it by using `ls` command.
    ```bash
    hacker@commands~touching-files:~$ ls /tmp
    bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
    ```
4. Now execute the run command.
    ```bash
    hacker@commands~touching-files:~$ /challenge/run
    Success! Here is your flag:
    pwn.college{s7rtLMruOyesMLOR6WEQBXE5jJM.QXwMDO0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/commands/) to complete the challenge.

We can also do the same challenge by going into `/tmp` first then using the `touch` command where then we have to just provide the file name as now they are relative to the cwd.
```bash
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
```

## What I learned
1. touch filename creates an empty file if filename does not exist otherwise it updates the files modification timestamps.(found other usecase from net)
2. We can give absolute as well as relative paths in `touch` command.
3. It creates a empty file - I used the `cat` command to see it whether its true or not.
    ```bash
    hacker@commands~touching-files:/tmp$ cat pwn
    hacker@commands~touching-files:/tmp$
    ```
    Since no output was there, it means that it created an empty file.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/commands/) - Comprehending Commands / Touching files module pages   