# Untangling Users
This module contains 4 modules that includes Becoming root with su, Other users with su, Cracking passwords and Using sudo.

# Becoming root with su
In this challenge we have to use `su` to become the root user with given password, then read the flag.

## My solution
**Flag:** `pwn.college{MYEuewGkH1ia9PAiDteLS-cIGV9.QX1UDN1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now we will get root acess through `su` and then we will provide the password.
    ```bash
    hacker@users~becoming-root-with-su:~$ su
    Password:
    root@users~becoming-root-with-su:/home/hacker# su
    root@users~becoming-root-with-su:/home/hacker#
    ```
3. Now to get our flag we can cat our flag.
    ```bash
    root@users~becoming-root-with-su:/home/hacker# cat /flag
    pwn.college{MYEuewGkH1ia9PAiDteLS-cIGV9.QX1UDN1wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/users/) to complete the challenge.

**My mistake:** I was not able to guess where the flag was so i used run program.
```bash
root@users~becoming-root-with-su:/home/hacker# /challenge/run
It's not just hackers that need to become `root`.
Oftentimes, you, as the owner of your computer, need to use `root` access to administer it.
Becoming `root` is a fairly common action........
```

## What I learned
1. `su` lets us switch to root if we know roots password.
2. After `su` succeeds we have a root shell (prompt typically ends with #).
3. This is not typically used to elevate to root access anymore.
4. It has the SUID bit set, `su` runs as root.
5.  The full list of users on a Linux system is specified in the `/etc/passwd` file.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/users/) - Untangling Users / Becoming root with su module pages.