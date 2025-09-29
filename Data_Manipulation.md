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


# Deleting characters
In this challenge the program `/challenge/run` prints the flag but intersperses decoy characters (`^` and `%`) among the real characters. So we havee to use `tr -d` to remove those decoys and reveal the flag.

## My solution
**Flag:** `pwn.college{MD32r-z7BW21OMmovCtnWovwn1W.0FNxEzNxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we will first pipe `/challenge/run` and then use `tr -d` to delete some decoys from the flag.
    ```bash
    hacker@data~deleting-characters:~$ /challenge/run | tr -d %^
    Your character-stuffed flag:
    pwn.college{MD32r-z7BW21OMmovCtnWovwn1W.0FNxEzNxwCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/data/) to complete the challenge.

**Note:** If you will give space between the characters to delete it will show error.
```bash
hacker@data~deleting-characters:~$ /challenge/run | tr -d % ^
tr: extra operand ‘^’
Only one string may be given when deleting without squeezing repeats.
Try 'tr --help' for more information.
```

## What I learned
1. `tr -d` deletes every occurrence of the characters specified.
2. We can provide characters to delete all without spaces.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/data/) - Data Manipulation / Deleting characters module pages.


# Deleting newlines
The challenge here is about handling streams of text that contain unwanted newline characters `\n`. The challenge is to use the `tr` command with the `-d` flag to delete all newline characters from the flags output so that it becomes a single continuous string.

## My solution
**Flag:** `pwn.college{g4Czz_-Ug1eO6YdX8ohTZRAKSVR.0VNxEzNxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we will use `tr -d` to remove newline characters `\n`.
    ```bash
    hacker@data~deleting-newlines:~$ /challenge/run | tr -d "\n"
    Your line-split flag: pwn.college{g4Czz_-Ug1eO6YdX8ohTZRAKSVR.0VNxEzNxwCO2kjNzEzW}hacker@data~deleting-newlines:~$
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/data/) to complete the challenge.

## What I learned
1. If quotes were not used, the shell itself would misinterpret it instead of passing it to `tr`.
2. `\n` cannot be typed directly into the terminal because pressing Enter will execute the command. Tha is why we must use the escape sequence "\n" inside quotes.
3. Using `tr -d` lets us strip away characters we dont want.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/data/) - Data Manipulation / Deleting newlines module pages.


# Extracting the first lines with head
In this challenge `/challenge/pwn` prints a lot of data. We have to take the first 7 lines of its output and pipe them into `/challenge/college` that will return the flag.

## My solution
**Flag:** `pwn.college{UVpSW8_MNDW4XDCZHVJpn0SIikk.0lNxEzNxwCO2kjNzEzW}`

1. I connected the dojo host using SSH command.
2. Now the shell is connected to dojo. Now we will pipe `/challenge/pwn` then use `head -n 7` to print first 7 files and redirect again it sdout to `/challenge/college` to get flag.
    ```bash
    hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
    Congratulations, you piped the right codes!
    pwn.college{UVpSW8_MNDW4XDCZHVJpn0SIikk.0lNxEzNxwCO2kjNzEzW}
    ```
3. I copied this flag and submitted it on [pwn.college](https://pwn.college/linux-luminarium/data/) to complete the challenge.

## What I learned
1. The `head` command is used to display the first few lines of its input.
2. We can control how many lines to be printed using `-n` argument and then writing that number after that as second argument.
3. By default, it shows the first 10 lines.

## References 
- [pwn.college](https://pwn.college/linux-luminarium/data/) - Data Manipulation / Extracting the first lines with head module pages.