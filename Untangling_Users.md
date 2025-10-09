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


# Other users with su
In this challenge we have to switch to the zardus user using `su` where the password is provided, then run `/challenge/run` as that user to get the flag.

## My solution
**Flag:** `pwn.college{gM2zqWi-8zm7eL_HfOjZVP2CnxM.QX2UDN1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now first we have to change user to `zardus` using `su` command and then passing the user as argument. Then give the password to enter the user.
    ```bash
    hacker@users~other-users-with-su:~$ su zardus
    Password:
    zardus@users~other-users-with-su:/home/hacker$
    ```
3. Now we can execute `/challenge/run` program to get our flag.
    ```bash
    zardus@users~other-users-with-su:/home/hacker$ /challenge/run
    Congratulations, you have become Zardus! Here is your flag:
    pwn.college{gM2zqWi-8zm7eL_HfOjZVP2CnxM.QX2UDN1wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/users/) to complete the challenge.


## What I learned
1. We can give a username as an argument to switch to that user instead of root.
2. by default `su` will start a root shell.
## References 
- [pwn.college](https://pwn.college/linux-luminarium/users/) - Untangling Users / Other users with su module pages.




# Cracking passwords
This challenge involves cracking a password from a leaked `/etc/shadow` file. The task is simulating a scenario where a hacker gains access to a system's shadow file, which contains hashed user passwords. The goal is to crack the hash to obtain the plaintext password, switch users using 'su', and execute a run program to retrieve the flag.

## My solution
**Flag:** `pwn.college{UCTane0kZMK0EzP0x7r1Cfz20o1.QX3UDN1wCO2kjNzEzW}`
1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I started by running John the Ripper on the provided /`challenge/shadow-leak` file:
    ```
    hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
    Created directory: /home/hacker/.john
    Loaded 1 password hash (crypt, generic crypt(3) [?/64])
    Press 'q' or Ctrl-C to abort, almost any other key for status
    aardvark         (zardus)
    1g 0:00:00:20 100% 2/3 0.04957g/s 288.6p/s 288.6c/s 288.6C/s Johnson..buzz
    Use the "--show" option to display all of the cracked passwords reliably
    Session completed
    ```
4. After cracking, the password for zardus was found to be `aardvark`. I then used `su zardus` to switch user:
    ```
    hacker@users~cracking-passwords:~$ su zardus
    Password: 
    zardus@users~cracking-passwords:/home/hacker$ 
    ```
5. Finally, I executed the run script to get the flag:
    ```
    zardus@users~cracking-passwords:/home/hacker$ /challenge/run
    Congratulations, you have become Zardus! Here is your flag:
    pwn.college{UCTane0kZMK0EzP0x7r1Cfz20o1.QX3UDN1wCO2kjNzEzW}
    ```
6. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/users/) to complete the challenge.


## What I Learned
- Passwords are stored in `/etc/shadow` with hashing for security.
- Backup leaks can expose sensitive data like shadow files.
- **John the Ripper:** A tool used to crack password hashes.
- Importance of strong passwords and securing sensitive files.
- Basic understanding of how hashes are cracked.

## References
- [pwn.college](https://pwn.college/linux-luminarium/users/) - Untangling Users / Cracking passwords module pages.
- John the Ripper documentation(The link was provided in the pwn college challenge question itself)




# Using sudo
This challenge tells of how to understand the use of sudo for privilege escalation in a Linux system. The task is to access a restricted file using sudo, which requires knowledge of how sudo works and its configuration. The challenge shows the difference between sudo and su, highlighting sudo's role for securely elevating privileges without needing the root password.

## My solution
**Flag:** `pwn.college{wOnu16b8i0NnDcuSnOcB-qb-zWF.QX4UDN1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I checked my current user by running `whoami`, which displayed `hacker`.
    ```bash
    hacker@users~using-sudo:~$ whoami
    hacker
    ```
4. I attempted to read the flag without sudo: `cat /flag`, but it was denied due to insufficient permissions.
    ```bash
    hacker@users~using-sudo:~$ cat /flag
    cat: /flag: Permission denied
    ```
5. I used sudo to escalate privileges and read the flag: `sudo cat /flag`, which successfully displayed the flag.
    ```bash
    hacker@users~using-sudo:~$ sudo cat /flag
    pwn.college{wOnu16b8i0NnDcuSnOcB-qb-zWF.QX4UDN1wCO2kjNzEzW}
    ```

## What I learned
- The concept of using `sudo` for privilege escalation, which is essential for system administration tasks.
- `sudo` uses a policy file `/etc/sudoers` to grant users permission to run commands as root without the need for the root password.
- The difference between sudo and su: `sudo` allows specific commands to be run with elevated privileges, while `su` typically launches a root shell.
- Knowledge of how to use sudo to access restricted files and execute commands that require root privileges.

## References
- [pwn.college](https://pwn.college/linux-luminarium/users/) - Untangling Users / Using sudo module.