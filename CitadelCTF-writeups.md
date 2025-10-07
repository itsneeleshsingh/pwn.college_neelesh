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
