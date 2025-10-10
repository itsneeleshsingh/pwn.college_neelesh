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





# Changing Permissions
The challenge is about understanding and modifying file permissions in Linux. We need to change the permissions of the `/flag` file to allow reading it. The file is owned by root with read-only access, so we must use `chmod` to modify its permissions and make it readable for others.

## My solution
**Flag:** `pwn.college{0XSkcqbAl72k1eFT6Zb7v1enE-n.QXzcjM1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I checked the current permissions of the `/flag` file:
   ```bash
   hacker@permissions~changing-permissions:~$ ls -l /flag
   -r-------- 1 root root 60 Oct 10 01:43 /flag
   ```
4. I observed that only root can read the file, so I need to change the permissions.
5. I used chmod to add read access for others so that they can also read the file:
   ```bash
   hacker@permissions~changing-permissions:~$ chmod o+r /flag
   ```
6. I checked the updated permissions to confirm:
   ```bash
   hacker@permissions~changing-permissions:~$ ls -l /flag
   -r-----r-- 1 root root 60 Oct 10 01:43 /flag
   ```
7. With read access granted, I read the flag using cat:
   ```bash
   hacker@permissions~changing-permissions:~$ cat /flag
   pwn.college{0XSkcqbAl72k1eFT6Zb7v1enE-n.QXzcjM1wCO2kjNzEzW}
   ```

## What I learned
In this challenge, I learned how to modify file permissions using the chmod command, using the symbolic mode to add read access for others. I understood how permissions are structured for user, group, and others.

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions / Changing Permissions module pages.





# Executable Files
This challenge focuses on understanding execute permissions in Linux. The goal is to make the `/challenge/run` program executable so that it can be run to retrieve the flag. The program initially lacks execute permissions for the user, requiring the use of chmod to set the appropriate permissions.

## My solution
**Flag:** `pwn.college{oKTus0SwdhhU8b8OxOoRGzl8GUR.QXyEjN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I first checked the permissions of `/challenge/run` using the `ls` command with `-l` option:
   ```bash
   hacker@permissions~executable-files:~$ ls /challenge/run -l
   -r--r--r-- 1 hacker hacker 32 Jan 14  2025 /challenge/run
   ```
   The output showed that the file had r--r--r-- permissions, meaning no execute permissions for anyone.
4. I tried to execute the program to see if it would run:
   ```bash
   hacker@permissions~executable-files:~$ /challenge/run
   bash: /challenge/run: Permission denied
   ```
   It resulted in a permission denied error, confirming the lack of execute permissions.
5. To resolve this, I used chmod to add execute permissions for the user `u+x`:
   ```bash
   hacker@permissions~executable-files:~$ chmod u+x /challenge/run
   hacker@permissions~executable-files:~$
   ```
6. After changing the permissions, I checked again with  `ls -l` to verify:
   ```bash
   hacker@permissions~executable-files:~$ ls /challenge/run -l
   -r-xr--r-- 1 hacker hacker 32 Jan 14  2025 /challenge/run
   ```
   The permissions were now r-xr--r--, indicating execute access for the user.
7. Finally, I executed the program, which ran successfully and displayed the flag:
   ```bash
   hacker@permissions~executable-files:~$ /challenge/run
   Successful execution! Here is your flag:
   pwn.college{oKTus0SwdhhU8b8OxOoRGzl8GUR.QXyEjN0wCO2kjNzEzW}
   ```

## What I learned
- Understanding the importance of execute permissions in Linux file systems.
- Familiarity with using `chmod` to modify permissions, specifically adding execute access.
- Recognizing how file ownership and permissions affect program execution.

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions /Executable Files module pages.




# Permission Tweaking Practice
This challenge is all about understanding and correctly modifying file permissions. The task requires us to change the permissions of a specific file multiple times, each time to match the given criteria. After successfully setting the permissions correctly eight times in a row, we will be allowed to modify the permissions of the flag file and thus we can read the flag.

## My solution
**Flag:** `pwn.college{EfN6YmimKc9T71UnuAjU_vO9pN5.QXwEjN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I started the challenge by running the command `/challenge/run` to begin the first round.
   ```bash
   hacker@permissions~permission-tweaking-practice:~$ /challenge/run
   Round 1 of 8!

   Current permissions of "/challenge/pwn": rw-r--r--
   * the user does have read permissions
   * the user does have write permissions
   - the user doesn't have execute permissions
   * the group does have read permissions
   - the group doesn't have write permissions
   - the group doesn't have execute permissions
   * the world does have read permissions
   - the world doesn't have write permissions
   - the world doesn't have execute permissions

   Needed permissions of "/challenge/pwn": rw-r--rw-
   * the user does have read permissions
   * the user does have write permissions
   - the user doesn't have execute permissions
   * the group does have read permissions
   - the group doesn't have write permissions
   - the group doesn't have execute permissions
   * the world does have read permissions
   * the world does have write permissions
   - the world doesn't have execute permissions
   ```

4. To set the correct permissions, I added write permissions for others using the command `chmod o+w /challenge/pwn`.
   ```bash
   hacker@permissions~permission-tweaking-practice:~$ chmod o+w /challenge/pwn
   ```

5. Proceeding to the next rounds, I continued adjusting the permissions as required:

- Added write permissions for others: `chmod o+w /challenge/pwn`
- Removed write permissions for others: `chmod o-w /challenge/pwn`
- Set read, write, and execute for all: `chmod ugo+rwx /challenge/pwn`
- Removed write and execute for group: `chmod g-wx /challenge/pwn`
- Added write and execute for group: `chmod g+wx /challenge/pwn`
- Removed read and execute for user and group: `chmod ug-rx /challenge/pwn`
- Removed read and execute for others: `chmod o-rx /challenge/pwn`

6. After successfully completing eight rounds, I was allowed to modify the permissions of the flag file.

   ```bash
   hacker@permissions~permission-tweaking-practice:~$ chmod ugo+x /challenge/pwn
   You set the correct permissions!
   You've solved all 8 rounds! I have changed the ownership
   of the /flag file so that you can 'chmod' it. You won't be able to read
   it until you make it readable with chmod!
   ```

7. The flag file had no permissions initially, so I added read permissions for the user. Then i printed the flag file.

   ```bash
   hacker@permissions~permission-tweaking-practice:~$ chmod u+r /flag
   hacker@permissions~permission-tweaking-practice:~$ cat /flag
   pwn.college{EfN6YmimKc9T71UnuAjU_vO9pN5.QXwEjN0wCO2kjNzEzW}
   ```

## What I learned
- Use the `chmod` command to set specific permissions for the user, group, and others.
- Understand the octal notation and how each digit corresponds to permissions read, write, execute.

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions / Permission Tweaking Practice module.




# Permissions Setting Practice
The goal is to learn how to use the `=` operator to set exact permissions, how to chain multiple permissions using commas, and how to remove permissions using the `-` operator. The challenge requires us to apply these concepts to achieve the desired permissions for a file through multiple rounds.

## My solution
**Flag:** `pwn.college{QkWgJkaIKQULWZ0yYE12bSvFNDi.QXzETO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. The first step was to understand the current permissions and the target permissions for each round. For example, in the first round, the current permissions were `-----xrwx`, and the target was `--xr-x-wx`. I needed to use `chmod` to set the correct permissions. I used the command:
   ```bash
   hacker@permissions~permissions-setting-practice:~$ chmod u=-,g=x,o+wx /challenge/pwn
   ```
   - This command sets the user permissions to none (u=-), group permissions to execute (g=x), and adds read, write, and execute for others (o+wx).

4. In the next rounds, I had to use different combinations of chmod commands. For example, in one round, I had to set user execute, group read, and world read and write permissions. I used:
   ```bash
   hacker@permissions~permissions-setting-practice:~$ chmod u=x,g+r,o=rw /challenge/pwn
   ```

5. Another round required setting group write and execute permissions but removing group read permissions. I used:
   ```bash
   hacker@permissions~permissions-setting-practice:~$ chmod g=-,o=wx /challenge/pwn
   ```

6. In the final round, after completing all 8 rounds, I was given a file /flag with no permissions. I needed to add read permissions for the user to view the flag:
   ```bash
   hacker@permissions~permissions-setting-practice:~$ chmod u+r /flag
   ```
   - After setting the permissions, I was able to read the flag:
   ```bash
   hacker@permissions~permissions-setting-practice:~$ cat /flag
   pwn.college{QkWgJkaIKQULWZ0yYE12bSvFNDi.QXzETO0wCO2kjNzEzW}
   ```

## What I learned
- Using `=` to set exact permissions.
- Chaining multiple permissions using commas.
- Using `-` to remove permissions.
- Understanding the difference between using - after =

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions / Permissions Setting Practice module page.




# The SUID Bit
The challenge requires setting the SUID bit on a program to execute it with root privileges. This allows a user to run the program as the file's owner, which in this case is root. The goal is to modify the permissions of the `/challenge/getroot` file so that it runs with elevated privileges, enabling access to the restricted flag file.

## My solution
**Flag:** `pwn.college{E6Ad3PAxN4FAd9RhOgYgwjh3da_.QXzEjN0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. First, I checked the current permissions of the `/challenge/getroot` file:
   ```bash
   hacker@permissions~the-suid-bit:~$ ls /challenge/getroot -l
   -rwxr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
   ```
   The output shows that the SUID bit is not set since the permissions are `-rwxr-xr-x`.

4. I set the SUID bit using the `chmod` command:
   ```bash
   hacker@permissions~the-suid-bit:~$ chmod u+s /challenge/getroot
   ```

5. After setting the SUID bit, I verified the permissions again:
   ```bash
   hacker@permissions~the-suid-bit:~$ ls /challenge/getroot -l
   -rwsr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
   ```
   Now, the permissions are `-rwsr-xr-x`, indicating that the SUID bit is set.

6. I executed the program to get a root shell:
   ```bash
   hacker@permissions~the-suid-bit:~$ /challenge/getroot
   SUCCESS! You have set the suid bit on this program, and it is running as root!
   Here is your shell...
   root@permissions~the-suid-bit:~#
   ```

7. Finally, I read the flag:
   ```bash
   root@permissions~the-suid-bit:~# cat /flag
   pwn.college{E6Ad3PAxN4FAd9RhOgYgwjh3da_.QXzEjN0wCO2kjNzEzW}
   ```

## What I learned
This challenge taught me how to set the SUID bit to allow a program to run with root privileges. I learned that the SUID bit is crucial for allowing non-root users to execute certain programs with elevated permissions. I also understand the importance of carefully assigning SUID permissions to avoid security risks.

## References
- [pwn.college](https://pwn.college/linux-luminarium/permissions/) - Perceiving Permissions / The SUID Bit module page.