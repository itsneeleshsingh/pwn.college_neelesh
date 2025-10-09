# Perceiving Permissions
This module contains 8 challenges that include Changing File Ownership, Groups and Files, Fun With Groups Names, Changing Permissions, Executable Files, Permission Tweaking Practice, Permissions Setting Practice and The SUID Bit.




# Changing File Ownership
The challenge focuses on understanding and modifying file ownership in Linux. The goal is to change the ownership of the `/flag` file from root to the hacker user, allowing the hacker to read the flag.

## My Solution
**Flag:** `pwn.college{IEgDk6OcOoF2O4c5WxmP0qz4b3Z.QXxEjN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I checked the current ownership and permissions of the `/flag` file:
   ```bash
   hacker@practice~permissions~changing-file-ownership:~$ ls /flag -l
   -r-------- 1 root root 22 Oct  9 17:32 /flag
   ```
4. I used the chown command to change the ownership of `/flag` to the hacker user:
   ```bash
   hacker@practice~permissions~changing-file-ownership:~$ chown hacker /flag
   ```
5. I verified the ownership change by listing the file again:
   ```bash
   hacker@practice~permissions~changing-file-ownership:~$ ls /flag -l
   -r-------- 1 hacker root 22 Oct  9 17:32 /flag
   ```
6. Finally, I read the contents of /flag using cat using unprivileged mode:
   ```bash
   hacker@permissions~changing-file-ownership:~$ cat /flag
   pwn.college{IEgDk6OcOoF2O4c5WxmP0qz4b3Z.QXxEjN0wCO2kjNzEzW}
   ```

## What I Learned
- Understanding the `chown` command to change file ownership.
- The importance of file permissions in controlling access to sensitive data.
- How ownership affects read/write/execute permissions for users and groups.

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions / Changing File Ownership module.




# Groups and Files
The challenge focuses on understanding Linux file permissions, particularly the role of groups in controlling access to files. It explains that each file has an owning user and group, and that group memberships determine access. The challenge involves changing the group ownership of a restricted flag to gain access and retrieve the flag.

## My solution
**Flag:** `pwn.college{I6Fwc2m_bZfT9HT92ysGPagXUcU.QXxcjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I checked the current permissions of the flag file by running `ls -l /flag`:
   ```bash
    hacker@practice~permissions~groups-and-files:~$ ls /flag -l
    -r--r----- 1 root root 22 Oct  9 17:54 /flag
   ```
4. I changed the group ownership of the flag file to the hacker group using `chgrp hacker /flag`.
5. Verified the change by running `ls -l /flag` again, showing the group updated to hacker:
   ```bash
    hacker@practice~permissions~groups-and-files:~$ ls /flag -l
    -r--r----- 1 root hacker 22 Oct  9 17:54 /flag
   ```
6. Accessed the flag by running `cat /flag`, which displayed the flag in unprivileged mode.
    ```bash
    hacker@permissions~groups-and-files:~$ cat /flag
    pwn.college{I6Fwc2m_bZfT9HT92ysGPagXUcU.QXxcjM1wCO2kjNzEzW}
    ```

Hacker has only group as itself.
```bash
hacker@permissions~groups-and-files:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
```

## What I learned
- Understanding of Linux file permissions, focusing on group ownership.
- Use of `id` to check user groups and `ls -l` to view file permissions.
- Usage of `chgrp` to change a file's group ownership.

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions / Groups and Files module.




# Fun With Groups Names
This challenge requires understanding how group ownership works in Linux and how to change it. The goal is to modify the group ownership of flag. We have to identify our current group using the `id` command and then use the `chgrp` command to change the group of the target file.

## My solution
**Flag:** `pwn.college{w7lCn-tLsl9X-UdHsQlkzqlCZfW.QXycjM1wCO2kjNzEzW}`

1. I connected the dojo host using the SSH command.
2. Now the shell is connected to dojo.
3. I first listed the permissions of the `/flag` file to understand its current ownership:
   ```bash
   hacker@permissions~fun-with-groups-names:~$ ls /flag -l
   -r--r----- 1 root root 60 Oct  9 18:25 /flag
   ```
   This showed that the file was owned by `root` with the group `root`.

4. I ran the `id` command to find out the group I belonged to:
   ```bash
   hacker@permissions~fun-with-groups-names:~$ id
   uid=1000(hacker) gid=1000(grp10547) groups=1000(grp10547)
   ```
   My group was `grp10547`.

5. Knowing that I needed to change the group of `/flag` to my own group, I used the `chgrp` command:
   ```bash
   hacker@permissions~fun-with-groups-names:~$ chgrp grp10547 /flag
   ```

6. After changing the group, I listed the permissions again to verify:
   ```bash
   hacker@permissions~fun-with-groups-names:~$ ls /flag -l
   -r--r----- 1 root grp10547 60 Oct  9 18:25 /flag
   ```
   The group was now `grp10547`, allowing me to access the file.

7. Finally, I read the contents of `/flag`:
   ```bash
   hacker@permissions~fun-with-groups-names:~$ cat /flag
   pwn.college{w7lCn-tLsl9X-UdHsQlkzqlCZfW.QXycjM1wCO2kjNzEzW}
   ```

## What I learned
- I learned the importance of understanding group memberships and permissions in Linux. 
- I understood how to use the `id` command to identify my current group.
- I practiced using the `chgrp` command to change the group ownership of a file.
- I realized that being part of a specific group grants access to files owned by that group, even if we are not the owner.

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions / Fun With Groups Names module pages.
