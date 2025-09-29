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


# Interrupting Processes
This challenge requires us to interrupt `/challenge/run`. `/challenge/run` will refuse to give you the flag until we interrupt it with Ctrl-C.

## My solution
**Flag:** `pwn.college{kBR4TU-SfKky1ML4O1ZS5SJtXR7.QXzQDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. So we have to execute `/challenge/run` and then press ctrl+C to interrupt the process that gives us the flag.
    ```bash
    hacker@processes~interrupting-processes:~$ /challenge/run
    I could give you the flag... but I won't, until this process exits. Remember,
    you can force me to exit with Ctrl-C. Try it now!
    ^C
    Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
    pwn.college{kBR4TU-SfKky1ML4O1ZS5SJtXR7.QXzQDO0wCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. The Ctrl key and pressing C sends an interrupt to whatever application is waiting on input from the terminal and this causes the application to exit.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Interrupting Processes module pages.


# Killing Misbehaving Processes
In this challenge a decoy process `/challenge/decoy` is holding open a named pipe (FIFO) at `/tmp/flag_fifo`. That prevents `/challenge/run` from writing the flag cleanly into the FIFO. So we have to find and kill the decoy process, then run `/challenge/run` so it can write the flag into `/tmp/flag_fifo`.

## My solution
**Flag:** `pwn.college{86EAtJN8iODKOvt1RLu1h3OyfIX.0FNzMDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now will first see the processes and find the one with `/challenge/decoy` path.
    ```bash
    hacker@processes~killing-misbehaving-processes:~$ ps aux
    USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root           1  0.0  0.0   1056   640 ?        Ss   13:38   0:00 /sbin/docker-init -- /nix/var/n
    root           7  0.0  0.0 231708  2560 ?        S    13:38   0:00 /run/dojo/bin/sleep 6h
    root         137  0.0  0.0   4132  1280 ?        S    13:38   0:00 /bin/bash /challenge/.init
    root         138  0.0  0.0   4132  1280 ?        S    13:38   0:00 /bin/bash /challenge/.init
    root         139  0.0  0.0   5204  3520 ?        S    13:38   0:00 su -c exec /challenge/decoy > /
    root         140  0.0  0.0   2744  1280 ?        S    13:38   0:00 sleep 6h
    root         141  0.0  0.0   2744  1600 ?        S    13:38   0:00 sleep 6h
    hacker       142  0.0  0.0  13516  9280 ?        Ss   13:38   0:00 /usr/bin/python /challenge/deco
    hacker       144  0.0  0.0 231576  3520 pts/0    Ss   13:38   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj
    hacker       150  0.0  0.0 231972  4160 pts/0    S    13:38   0:00 /run/dojo/bin/bash --login
    hacker       167  0.0  0.0 231576  3520 pts/1    Ss   14:02   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj
    hacker       173  0.0  0.0 231972  4160 pts/1    S+   14:02   0:00 /run/dojo/bin/bash --login
    hacker       190  0.0  0.0 233600  3840 pts/0    R+   14:07   0:00 ps aux
    ```
3. Now we will kill the 142 process.
    ```bash
    hacker@processes~killing-misbehaving-processes:~$ kill 142
    hacker@processes~killing-misbehaving-processes:~$
    ```
4. Now execute the `/challenge/run`.
    ```bash
    hacker@processes~killing-misbehaving-processes:~$ /challenge/run
    Sending the flag to /tmp/flag_fifo!
    ```
5. Now open another terminal and try to read the flag.
    ```bash
    hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo
    pwn.college{E9nSj7c5EvFb1RBXDT9B9QTVxbkCHoj0kO9q0H3g9Sb5c-b}
    pwn.college{-g6Yz9HNx6tEPWmEJHi9lJenmKgiOwPK.8nqxw3y5Oir.ta}
    pwn.college{yYhwrreDRrrwCOxMpXwrUPxYwZ6uwO8iF44anR1a.DQwM1p}
    (and so on..........)
    ```
6. These are some random flags that was buffered through pipes. For that we will again execute `/challenge/run` in and on another terminal again catch it.
    ```bash
    hacker@processes~killing-misbehaving-processes:~$ /challenge/run
    Sending the flag to /tmp/flag_fifo!

    hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo
    pwn.college{86EAtJN8iODKOvt1RLu1h3OyfIX.0FNzMDOxwCO2kjNzEzW}
    ```
7. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. Learned to use kill and list processes.
2. How FIFOs buffer data killing a process does not remove data already in the pipe.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Killing Misbehaving Processes module pages.


# Suspending Processes
This challenge requires us to launch `/challenge/run`, suspend it, then launch another copy while the first is suspended (the program wants to see another copy sharing the same terminal).

## My solution
**Flag:** `pwn.college{ATbMjL25KDbBV7L0FoP0B2QakOQ.QX1QDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we will first execute `/challenge/run` and then suspend it using ctrl+z.
    ```bash
    hacker@processes~suspending-processes:~$ /challenge/run
    I'll only give you the flag if there's already another copy of me running in
    this terminal... Let's check!

    UID          PID    PPID  C STIME TTY          TIME CMD
    root         138     129  0 14:36 pts/0    00:00:00 bash /challenge/run
    root         140     138  0 14:36 pts/0    00:00:00 ps -f

    I don't see a second me!

    To pass this level, you need to suspend me and launch me again! You can
    background me with Ctrl-Z or, if you're not ready to do that for whatever
    reason, just hit Enter and I'll exit!
    ^Z
    [1]+  Stopped                 /challenge/run
    ```
3. Now we will again execute it to get our flag.
    ```bash
    hacker@processes~suspending-processes:~$ /challenge/run
    I'll only give you the flag if there's already another copy of me running in
    this terminal... Let's check!

    UID          PID    PPID  C STIME TTY          TIME CMD
    root         138     129  0 14:36 pts/0    00:00:00 bash /challenge/run
    root         145     129  0 14:36 pts/0    00:00:00 bash /challenge/run
    root         147     145  0 14:36 pts/0    00:00:00 ps -f

    Yay, I found another version of me! Here is the flag:
    pwn.college{ATbMjL25KDbBV7L0FoP0B2QakOQ.QX1QDO0wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. We can suspend a running process with Ctrl-Z.
2. We can also resume those suspended processes.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Suspending Processes module pages.


# Resuming Processes
The challenge requires us to suspend a running process and then resume it back into the foreground.

## My solution
**Flag:** `pwn.college{4rqWJdPSf-1XtOvgrXidFU7p1hd.QX2QDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now first we will run the program and then suspend it.
    ```bash
    hacker@processes~resuming-processes:~$ /challenge/run
    Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
    the 'fg' command! Or just press Enter to quit me!
    ^Z
    [1]+  Stopped                 /challenge/run
    ```
3. then we will again resume the program to get our flag.
    ```bash
    hacker@processes~resuming-processes:~$ fg
    /challenge/run
    I'm back! Here's your flag:
    pwn.college{4rqWJdPSf-1XtOvgrXidFU7p1hd.QX2QDO0wCO2kjNzEzW}
    Don't forget to press Enter to quit me!

    Goodbye!
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. Suspending and resuming processes in Linux
    - Ctrl+C kills a process, but Ctrl+Z only pauses it, allowing us to resume later.
    - This is useful when we want temporary control of our shell back without terminating the running program.
2. fg (foreground) resumes the most recent suspended job.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Resuming Processes module pages.


# Backgrounding Processes
The challenge asks us to understand how to move a suspended process into the background using the `bg` command. This allows a program to keep running while still giving us back the shell to run other commands.

## My solution
**Flag:** `pwn.college{UeCd0hnGaFSRhjzSgWW-tQzS_E1.QX3QDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now first we will execute run program and then suspend it using ctrl+z.
    ```bash
    hacker@processes~backgrounding-processes:~$ /challenge/run
    I'll only give you the flag if there's already another copy of me running *and
    not suspended* in this terminal... Let's check!

    UID          PID STAT CMD
    root         153 S+   bash /challenge/run
    root         155 R+   ps -o user=UID,pid,stat,cmd

    I don't see a second me!

    To pass this level, you need to suspend me, resume the suspended process in the
    background, and then launch a new version of me! You can background me with
    Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
    do that for whatever reason, just hit Enter and I'll exit!
    ^Z
    [1]+  Stopped                 /challenge/run
    ```
3. Then we will background the proccess with `bg`.
    ```bash
    hacker@processes~backgrounding-processes:~$ bg
    [1]+ /challenge/run &
    hacker@processes~backgrounding-processes:~$


    Yay, I'm now running the background! Because of that, this text will probably
    overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
    to scroll this text out.
    ```
4. Now we will again run the program to get our flag.
    ```bash
    hacker@processes~backgrounding-processes:~$ /challenge/run
    I'll only give you the flag if there's already another copy of me running *and
    not suspended* in this terminal... Let's check!

    UID          PID STAT CMD
    root         153 S    bash /challenge/run
    root         163 S    sleep 6h
    root         164 S+   bash /challenge/run
    root         166 R+   ps -o user=UID,pid,stat,cmd

    Yay, I found another version of me running in the background! Here is the flag:
    pwn.college{UeCd0hnGaFSRhjzSgWW-tQzS_E1.QX3QDO0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. Difference between suspended and background processes
    - Suspended: paused that is not executing (STAT = T).
    - Backgrounded: running in background and not blocking the shell (STAT = S)

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Backgrounding Processes module pages.


# Foregrounding Processes
The challenge asks us to bring a backgrounded process back into the foreground using the `fg` command. This is similar to how we resume suspended processes, but here we are working with jobs that were already running in the background.

## My solution
**Flag:** `pwn.college{ciA37v080UPACwli35TizXEsY4m.QX4QDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we have to first run the program and suspend it.
    ```bash
    hacker@processes~foregrounding-processes:~$ /challenge/run
    To pass this level, you need to suspend me, resume the suspended process in the
    background, and *then* foreground it without re-suspending it! You can
    background me with Ctrl-Z (and resume me in the background with 'bg') or, if
    you're not ready to do that for whatever reason, just hit Enter and I'll exit!
    ^Z
    [1]+  Stopped                 /challenge/run
    ```
3. Now we have to make it as background process.
    ```bash
    hacker@processes~foregrounding-processes:~$ bg
    [1]+ /challenge/run &
    hacker@processes~foregrounding-processes:~$


    Yay, I'm now running the background! Because of that, this text will probably
    overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
    to scroll this text out. After that, resume me into the foreground with 'fg';
    I'll wait.

    hacker@processes~foregrounding-processes:~$ 
    ```
4. Now make it foreground using `fg` and then click enter to get the flag.
    ```bash
    hacker@processes~foregrounding-processes:~$ fg
    /challenge/run
    YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

    pwn.college{ciA37v080UPACwli35TizXEsY4m.QX4QDO0wCO2kjNzEzW}
    ```
5. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. Difference between bg and fg
    - bg: lets the process continue running in the background.
    - fg: brings it back to the foreground so we can interact with it directly.
2. With suspend (Ctrl+Z), background (bg), and foreground (fg), we have full control over how processes use the terminal.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Foregrounding Processes module pages.


# Starting Backgrounded Processes
In this challenge, we have to start a process directly in the background without suspending it first.

## My solution
**Flag:** `pwn.college{Ip02W_JE9RZFM6fIAGwDJ0wI9iY.QX5QDO0wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. So we can directly make the program run in background using `&`.
    ```bash
    hacker@processes~starting-backgrounded-processes:~$


    Yay, you started me in the background! Because of that, this text will probably
    overlap weirdly with the shell prompt, but you're used to that by now...

    Anyways! Here is your flag!
    pwn.college{Ip02W_JE9RZFM6fIAGwDJ0wI9iY.QX5QDO0wCO2kjNzEzW}

    [1]+  Done                    /challenge/run
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. Starting with `&` - directly launches process in the background.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Starting Backgrounded Processes module pages.


# Process Exit Codes
In this challenge, `/challenge/get-code` produces a hidden exit code. We then need to use that code as input to `/challenge/submit-code` to retrieve the flag.

## My solution
**Flag:** `pwn.college{UGrACFvhLB2YMexoQsBSinbkcHD.QX5YDO1wCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now run `/challenge/get-code` and get the value of the exit code using `echo $?`.
    ```bash
    hacker@processes~process-exit-codes:~$ /challenge/get-code
    Exiting with an error code!
    hacker@processes~process-exit-codes:~$ echo $?
    254
    ```
3. Now we will submit code 254 as argument to `/challenge/submit-code`.
    ```bash
    hacker@processes~process-exit-codes:~$ /challenge/submit-code 254
    CORRECT! Here is your flag:
    pwn.college{UGrACFvhLB2YMexoQsBSinbkcHD.QX5YDO1wCO2kjNzEzW}
    ```
4. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/processes/) to complete the challenge.

## What I learned
1. Every program exits with an exit code when it finishes running and terminates. 
2. We can access the exit code of the most recently terminated command using the special `?` variable with `$` prepend to it to read its value.
3. Commands that succeed typically return `0` and commands that fail typically return a non-zero value, most commonly `1`.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/processes/) - Processes and Jobs / Process Exit Codes module pages.