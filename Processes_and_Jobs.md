# Processes and Jobs
This module contains 10 challenges that includes Listing Processes, Killing Processes, Interrupting Processes, Killing Misbehaving Processes, Suspending Processes, Resuming Processes, Backgrounding Processes, Foregrounding Processes, Starting Backgrounded Processes and Process Exit Codes.

# Listing Processes
The challenge hides the `/challenge/run` by renaming it and preventing us from listing `/challenge` with `ls`. However, the challenge process is running so we can discover its filename by inspecting the running processes with `ps` after we can invoke it directly to get the flag.

## My solution
**Flag:** `pwn.college{0m7VnMhLCTTyq1wHI3o_G98jz1V.QX4MDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo. Now to list all the running process we will use `ps` command.
    ```bash
    hacker@processes~listing-processes:~$ ps -ef
    UID          PID    PPID  C STIME TTY          TIME CMD
    root           1       0  0 09:24 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/pro
    root           7       1  0 09:24 ?        00:00:00 /run/dojo/bin/sleep 6h
    root         132       1  0 09:24 ?        00:00:00 /challenge/30404-run-19725
    root         135     132  0 09:24 ?        00:00:00 sleep 6h
    hacker       137       0  0 09:24 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms
    hacker       143     137  0 09:24 pts/0    00:00:00 /run/dojo/bin/bash --login
    hacker       154     143  0 09:34 pts/0    00:00:00 ps -ef
    ```
3. Now we can see the `/challenge/30404-run-19725` which is the renamed file. We can invoke it to get our flag.
    ```bash
    hacker@processes~listing-processes:~$ /challenge/30404-run-19725
    Yahaha, you found me! Here is your flag:
    pwn.college{0m7VnMhLCTTyq1wHI3o_G98jz1V.QX4MDO0wCO2kjNzEzW}
    Now I will sleep for a while (so that you could find me with 'ps').
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. `ps` lists the processes running in our terminal.
2. `ps` has two popular syntaxes:
    - System (Unix) style: `ps -ef` (with options like -e, -f).
    - BSD style: `ps aux` (with options like a, u, x).
3. ps output gets truncated to terminal width by default. We use `w/ww` to avoid truncation.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Listing Processes module pages.


# Killing Processes
In this level `/challenge/run` refuses to execute while `/challenge/dont_run` is running. We have to locate the `dont_run` process and terminate it so we can run `/challenge/run` and get the flag.

## My solution
**Flag:** `pwn.college{YAxzS_lmRvhACXLQreHarnlCz2h.QXyQDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we will search for processes using `ps -ef` for `dont_run`.
    ```bash
    hacker@processes~killing-processes:~$ ps -ef | grep dont_run
    hacker       136     135  0 11:59 ?        00:00:00 /challenge/dont_run
    hacker       159     145  0 11:59 pts/0    00:00:00 grep --color=auto dont_run
    ```
3. Now we get the PID as `136`. Now we can use `kill` command.
    ```bash
    hacker@processes~killing-processes:~$ kill 136
    hacker@processes~killing-processes:~$
    ```
4. Now if we check process has stopped.
    ```bash
    hacker@processes~killing-processes:~$ ps -ef | grep dont_run
    hacker       163     145  0 12:00 pts/0    00:00:00 grep --color=auto dont_run
    ```
5. Now we can run `/challenge/run`.
    ```bash
    hacker@processes~killing-processes:~$ /challenge/run
    Great job! Here is your payment:
    pwn.college{YAxzS_lmRvhACXLQreHarnlCz2h.QXyQDO0wCO2kjNzEzW}
    ```
6. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. `kill` command is used to terminate processes.
2. `sleep` is a program that simply hangs out for the number of seconds specified on the commandline.
3.  `kill` to terminate it by passing the process identifier (the PID from ps) as an argument.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Killing Processes module pages.