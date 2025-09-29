# Data Manipulation
This module contains 6 challenges that include Translating characters, Deleting characters, Deleting newlines, Extracting the first lines with head, Extracting specific sections of text and Sorting data.

# Translating characters
The challenge asks us to use the `tr` command to correct the output of `/challenge/run`. The command prints the flag with inverted case (uppercase becomes lowercase and vice-versa). Our task is to use `tr` to swap the casing back and reveal the correct flag.


## My solution
**Flag:** `pwn.college{0KpsIfytWGXDuYO21u0rahJPsxr.01MxEzNxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
    ```bash
    neel@NeelTech:~$ ssh -i ./key hacker@dojo.pwn.college
    Connected!
    ```
2. Now the shell is connected to dojo.  Now since we have to change `a-z` to `A-Z` and vice versa using `tr`. I remember that instead of writing abc....z we can write a-z.
    ```bash
    hacker@data~translating-characters:~$ /challenge/run | tr A-Za-z a-zA-Z
    yOUR CASE-SWAPPED FLAG:
    pwn.college{0KpsIfytWGXDuYO21u0rahJPsxr.01MxEzNxwCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/data/) to complete the challenge.

**My mistake:** I first wrote only the first part and not the opposite case which gave incorrect flag.
```bash
hacker@data~translating-characters:~$ /challenge/run | tr A-Z a-z
your case-swapped flag:
pwn.college{0kpsifytwgxduyo21u0rahjpsxr.01mxeznxwco2kjnzezw}
```

## What I learned
1. `tr` translates characters it receives over standard input and prints them to standard output.
2. `t`r` translates the character provided in its first argument to the character provided in its second argument.
3. We can specify whole ranges like `a-z` or `A-Z` instead of listing characters individually.
4. It can also handle multiple characters.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/data/) - Data Manipulation / Translating characters module pages.