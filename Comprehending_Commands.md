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


