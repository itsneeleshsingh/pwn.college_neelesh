# Terminal Multiplexing
This module contains 6 modules that includes Launching Screen, Detaching and Attaching, Finding Sessions, Switching Windows, Detaching and Attaching (tmux) and Switching Windows (tmux)




# Launching Screen
The challenge requires us to use the `screen` program to create a virtual terminal. Screen allows multiple terminal sessions within a single session, providing features similar to tabbed browsing but for the command line. We have to launch `screen` which will display the flag directly.

## My solution
**Flag:** `pwn.college{QCqcu3saXKjuGvuC8pvMH2F0DL7.0VN4IDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I ran the `screen` command to start a new session. 

   ```bash
   hacker@terminal-multiplexing~launching-screen:~$ screen
   ```

4. Upon entering the screen session, the flag was displayed.

   ```bash
   Congratulations! You're inside a screen session!
   Here's your flag:
   pwn.college{QCqcu3saXKjuGvuC8pvMH2F0DL7.0VN4IDOxwCO2kjNzEzW}
   ```

5. To exit, I typed `exit`.

   ```bash
   hacker@terminal-multiplexing~launching-screen:~$ exit
   ```

6. After exiting, I verified that the screen session terminated.

   ```bash
   hacker@terminal-multiplexing~launching-screen:~$ screen
   [screen is terminating]
   ```

## What I learned

- The `screen` command creates a virtual terminal within the existing terminal.
- Starting and stopping sessions with `screen` and `exit`/`Ctrl-D`.
- Understanding terminal multiplexing benefits like managing multiple terminal sessions.

## References
- [pwn.college](https://pwn.college/modules/terminal-multiplexing) - Terminal Multiplexing / Launching Screen Module.




# Detaching and Attaching
The challenge asks us to use `screen` to create a session, detach from it, run command that sends a flag to the detached session, and then reattach to retrieve the flag. 

## My solution
**Flag:** `pwn.college{AZeISjFTVGWAjlSfFEI7EWocQv7.0lN4IDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.
3. I launched screen by typing `screen` in the terminal.
   ```bash
   hacker@terminal-multiplexing~detaching-and-attaching:~$ screen
   ```
4. After starting screen, I detached from the session using the shortcut `Ctrl+A` followed by `d`.
   ```bash
   [detached from 149.pts-0.terminal-multiplexing~detaching-and-attaching]
   ```
5. I then ran the command `/challenge/run` to send the flag to the detached session.
   ```bash
   hacker@terminal-multiplexing~detaching-and-attaching:~$ /challenge/run
   Found detached screen session: 140.pts-0.terminal-multiplexing~detaching-and-attaching
   Sending flag to your screen session...
   
   Flag sent! Now reattach to your screen session with:
   
     screen -r
   ```
6. Finally, I reattached to the screen session using `screen -r` and retrieved the flag.
   ```bash
   hacker@terminal-multiplexing~detaching-and-attaching:~$ screen -r

   hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{AZeISjFTVGWAjlSfFEI7EWocQv7.0lN4IDOxwCO2kjNzEzW}
   ```

## What I learned
- The `screen` command allows creating persistent terminal sessions that can be detached and reattached.
- Detaching with `Ctrl+A d` keeps the session running in the background.
- Reattaching is done using `screen -r`.

## References
- [pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing) - Terminal Multiplexing / Detaching and Attaching Module






# Finding Sessions
In this challenge, we need to identify the correct screen session out of three that contains the flag. The other two sessions are decoys.

## My solution
**Flag:** `pwn.college{sLmAYpHR-ssAStsJsSl08J6XKHh.01N4IDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. I listed all running screen sessions to identify which ones are available:
   ```bash
   hacker@terminal-multiplexing~finding-sessions:~$ screen -ls
   There are screens on:
           171.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
           140.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
           144.session_5cf234879ad9bea8    (Detached)
           147.session_0684d3ec973d8f1c    (Detached)
           150.session_7e3de0a10a2e927d    (Detached)
   5 Sockets in /home/hacker/.screen.
   ```

4. Next, I tried reattaching to the first detached session using its PID:
   ```bash
   hacker@terminal-multiplexing~finding-sessions:~$ screen -r 144
   ```

5. Inside the session, I found the flag message, confirming it's the correct session:
   ```
   Well done! You've found the right ses-
   ght session!'
   Congratulations! You found the right session!
    hacker@terminal-multiplexing~finding-sessions:~$echo pwn.college{sLmAYpHR-ssAStsJsSl08J6XKHh.01N4IDOxwCO2kjNzEzW}
    pwn.college{sLmAYpHR-ssAStsJsSl08J6XKHh.01N4IDOxwCO2kjNzEzW}
   ```

6. I detached from this session using `Ctrl-A d` to ensure I could return to the main shell and potentially check others if needed, but since I found the flag, I stopped here.

## What I learned
- The `screen` command that allows managing multiple sessions.
- `screen -ls` lists all active and detached sessions.
- Using `screen -r [PID/session_name]` reattaches to a specific session.
- `Ctrl-A d` detaches the current session without closing it.

## References
- [pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) - Terminal Multiplexing / Finding Sessions Module.




# Switching Windows
In this challenge, we need to work within a screen session that already has two windows set up. Window 0 contains a flag, while window 1 has a welcome message. Our task is to switch to window 0 using the appropriate screen commands and retrieve the flag.

## My solution
**Flag:** `pwn.college{schfuhlJL9EAgXjAZ1f9ORoVtoD.0FO4IDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. I listed the available screen sessions using the command `screen -ls` to find the correct session to attach to.

    ```bash
    hacker@terminal-multiplexing~switching-windows:~$ screen -ls
    There are screens on:
            171.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
            140.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
            150.session_7e3de0a10a2e927d    (Remote or dead)
            135.challenge_session   (Detached)
    4 Sockets in /home/hacker/.screen.
    ```

4. I reattached to the session using `screen -r 135`.

    ```bash
    hacker@terminal-multiplexing~switching-windows:~$ screen -r 135
    ```

5. Once attached, I received a message indicating that I was in window 1 and that the flag was in window 0.

6. I used the command `Ctrl-A p` to switch to the previous window (window 0).

7. In window 0, I used the following command to display the flag.

    ```bash
    hacker@terminal-multiplexing~switching-windows:~$ cat <<MSG
    > Excellent work! You found window 0!
    > Here is your flag: pwn.college{schfuhlJL9EAgXjAZ1f9ORoVtoD.0FO4IDOxwCO2kjNzEzW}
    > MSG
    Excellent work! You found window 0!
    Here is your flag: pwn.college{schfuhlJL9EAgXjAZ1f9ORoVtoD.0FO4IDOxwCO2kjNzEzW}
    ```

## What I learned

- The basics of using screen sessions to create and manage multiple windows within a session.
- Keyboard shortcuts like:
    - `Ctrl-A c` - Create a new window
    - `Ctrl-A n` - Next window
    - `Ctrl-A p` - Previous window
    - `Ctrl-A 0` through `Ctrl-A 9` - Jump directly to window 0-9
    - `Ctrl-A "` - bring up a selection menu of all of the windows
- How to list and reattach to existing screen sessions using commands like `screen -ls` and `screen -r`.

## References

- [pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) - Terminal Multiplexing / Switching Windows module.





# Detaching and Attaching (tmux)
The challenge introduces using tmux, a replacement for screen with different key bindings. The task is to launch tmux, detach and run the `/challenge/run` to send a flag and reattach to retrieve it.

## My solution
**Flag:** `pwn.college{MDNb3VCSaccvMqApbhHKiltEL1c.0VO4IDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. The shell is connected to dojo.

3. I started a new tmux session:
    ```bash
    hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux
    ```

4. I detached from the session by pressing `Ctrl-B` and then `d`:
    ```bash
    [Press Ctrl-B, then d]
    [detached (from session 0)]
    hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ 
    ```

5. I executed the `/challenge/run` script to send the flag:
    ```bash
    hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ /challenge/run
    Found detached tmux session: 0
    Sending flag to your tmux session...
    Flag sent! Now reattach to your tmux session with:
    tmux attach
    ```

6. I reattached to the tmux session:
    ```bash
    hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux attach
    ```

7. The flag is now printed:
    ```bash
    hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ echo Congratulations, here is your flag: pwn.college{MDNb3VCSaccvMqApbhHKiltEL1c.0VO4IDOxwCO2kjNzEzW}
    Congratulations, here is your flag: pwn.college{MDNb3VCSaccvMqApbhHKiltEL1c.0VO4IDOxwCO2kjNzEzW}
    ```

## What I learned
- tmux uses `Ctrl-B` as its command prefix.
- Key functions in tmux include detaching with `Ctrl-B d`, listing sessions with `tmux ls`, and attaching with `tmux attach`.

## References
- [pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing) - Terminal Multiplexing / Detaching and Attaching (tmux) module.




# Switching Windows (tmux)
The challenge requires navigating between windows in tmux, a terminal multiplexer. Tmux uses different key combinations compared to screen for managing windows. We need to switch windows using the specified key bindings to find the flag hidden in a different window(Window 0).

## My solution
**Flag:** `pwn.college{E0Z06hrHoXY2uvLZcG1aQXst7QD.0FM5IDOxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo.

3. So first i reaatach to the session.
    ```bash
    hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux a
    ```
4. I knew I needed to switch windows in tmux. I remembered that `Ctrl-B n` and `Ctrl-B p` are used to switch to the next and previous windows respectively.
    ```bash
    cat <<MSG
    Welcome to the tmux window switching challenge!
    You are currently in window 1.
    The flag is hidden in window 0.
    Use Ctrl-B 0 to switch to window 0!
    MSG
    ```

5. I decided to switch to window 0 using `Ctrl-B 0` since the flag was hidden there. Once I switched to window 0, I saw the flag in the terminal output.
    ```bash
    hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
    > Excellent work! You found window 0!
    > Here is your flag: pwn.college{E0Z06hrHoXY2uvLZcG1aQXst7QD.0FM5IDOxwCO2kjNzEzW}
    > MSG
    Excellent work! You found window 0!
    Here is your flag: pwn.college{E0Z06hrHoXY2uvLZcG1aQXst7QD.0FM5IDOxwCO2kjNzEzW}
    hacker@terminal-multiplexing~switching-windows-tmux:~$
    ```

## What I learned

- How to create and manage multiple windows in tmux.
- How to switch between windows using key bindings like `Ctrl-B n`, `Ctrl-B p`, and `Ctrl-B 0-9`.
- Understanding the status bar in tmux that shows active windows and the current window with an asterisk.

## References
- [pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) - Terminal Multiplexing / Switching Windows (tmux) module.