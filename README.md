<div style="text-align:center"><img src="https://i.imgur.com/ZA4UOgO.png"/></div>

## **Crypto**

### **(30p) Those Are Rookie Numbers:**
#### Solver(s): PinkiePie1189#7418, Gabies#3036
The problem was giving us the RSA parameters n, c and e. N was small so using factordb.com we factorize n to get p, q and phi, and d using the extended euclidean algorithm. Now, we just do c^d % n to get the plaintext and decode it (it's encoded in hexadecimal form) to get the flag. <br> <br>
Tools used: Python, factordb.com <br>
<br>
<br>

### **(50p) Back in Time:**
#### Solver(s): Gabies#3036

In this problem we were given a ciphertext and an encryption python script. The script just applies on the plaintext an alphabet shuffle for lowercase letters. The ciphertext just contains the encypted flag: hsijhk{Pc3nvO_R4NvwM_1S_Nwh_RArD0M}. We can see that some of the words can be deducted: RArD0M-> RAnD0M so r=n; R4NvwM->R4NdoM so v=d and w=o also hsijhk-> timctf. From all these observations the flag becomes timctf{Pc3ndo_R4NdoM_1S_Not_RAnD0M}. Looking up for words that look like p?e?do in english we quickly see that the flag is timctf{Ps3udo_R4NdoM_1S_Not_RAnD0M}. <br> <br>
Tools used: Google <br>
<br>
<br>

### **(75p) SSS Part 1:**
#### Solver(s): Gabies#3036
The problem had attached to it a .png file which was showing a linear function and 3 values in the XY coordinate system, also the picture shows a dot at the value of f(0). The problem statement was the big hint, looking up for Lagrange in cryptography you can read about Lagrange Interpolation and Shamir's Secret Sharing. So after a good read time it was clear that we were given 3 keys for an SSS which needed only 2 keys.

SO:
S=f(0) <br>
S+X1=K1 <br>
S+X2=K2 <br>
2*S=K1+K2-X1-X2 <br>
S=(K1+K2-X1-X2)/2 <br>
Transform S in hexadecimal and then into ascii and that's the flag. <br> <br>
Tools used: - <br>
<br>
<br>

### **(100p) Not your average RSA:**
#### Solver(s): PinkiePie1189#7418, Gabies#3036
This problem was very similar to "Those are rookie numbers", only that n was way larger and we didn't know e.
To factorize n would be imposible, but the hint about MP told us something, n wasn't semiprime, it was a Multiple Prime RSA, so easily factorizable. Now that we know the factorization we can calculate Carmichael(n) which is equal to lcm(primes-1), this gives us phi. Now to get e we assumed that it was equal to the most common value 65537=(2^16+1)(the largest Fermat Prime known). Then we proceed in the same manner as in "Those are rookie numbers" to get the flag. <br> <br>
Tools used: Python, factordb.com <br>
<br>
<br>

### **(100p) Substitute Teacher:**
#### Solver(s): Gabies#3036
In this problem we were given a ciphertext.txt. The encryption was just a alphabet shuffle for lowercase letters, so when I found a paragraph that was written in uppercase i just copied it and pasted it in Google, i found out soon that the book was "The Da Vinci Code". From here on it's trivial to find out the inverse encryption permutation of the alphabet and then apply it on the ciphertext. Then just look up for "timctf" and you'll get the flag. (I actually solved this problem on my phone :) ). <br> <br>
Tools used: Google <br>

<br>
<br>
<br>

## **Forensics**
### **(50p) Picassor:**
#### Solver(s): JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357

After many tries of finding hidden files in the given file, we gave up and went back to the drawing board to find a new idea. We noticed that the first part of the file seemed oddly regular and arranged, so we supposed it might be a codified regular file. After checking the JPEG file structure, we noticed that it was pretty similar to our file, so we started noting down the changes between our file and a normal JPEG file. Thus, we made a small tabel with Regular JPEG Characters vs. our file's JPEG Characters. (Regular JPEG Characters meaning file headers and other chars that are obligatory present at various positions in every JPEG). It couldn't be a direct conversion between characters, because FF becomes 54, for example. So we'd have to find the more complex codification that the file was using. After various tries, we noticed that there are indeed direct transformations for hex digits, but the transformation table depends on the position of the digit. For example, the F always becomes 5 if it's the first digit in a byte represented in hex, and 4 if it's the second digit. So, we made two tables, one for transformations made for first digits, and another one for transformations made for the second digits. After some deductions we started to complete the tables. For example, if we saw that A is 0, and 0 is A, and that 7 is E and E is 7, we can presume that the table is reversible, effectively reducing the amount of guesses that need to be made by half. After other deductions like filling in a bit obvious holes like 4 _ 6, we finished the tables. We were not 100% certain that they'd be correct, but they were the most plausible ones. Then, we switched to our trusty CodeBlocks IDE and started writing a small C++ program that'd open the file byte by byte, extracting each unsigned character as it parsed it. We passed the characters through a function that'd return the equivalent of the given character judging by the values of our tables, and we'd print the result out, byte by byte. After some bugfixing and finally figuring out how to properly read byte-by-byte in C++, we were able to generate a decoded JPEG file, that had the key written on the picture! <br> <br>
Tools used: HxD Hex Editor, CodeBlocks <br>
<br>
<br>

### **(50p) Secret Data:**
#### Solver(s): TavisIT#4504

Another simple problem, that we kind of skipped right to the end. Open the file that you are provided with in Notepad++ and look up timctf. There's the flag. Probably it should've been solved using Wireshark as the flag suggests :). <br> <br>
Tools used: Notepad++ <br>
<br>
<br>

### **(100p) Strange Behaviour:**
#### Solver(s): JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357, PinkiePie1189#7418, Gabies#3036

We ran binwalk on the file, and noticed a zipped archive inside it. We copied the bytes at that location and saved them into a new file. We then unzipped the new file that contained some .xml files, one of them containing our flag. <br> <br>
Tools used: Binwalk, WinRAR, Google Chrome <br>
<br>
<br>

### **(120p) Invitation:**
#### Solver(s): Gabies#3036

We were given a PDF document of an invitation, nothing to see at start. I opened the file using ghex and found a link on GitHub. The link showed up a panda_gif.txt file which was looking like a base64 encoding, but it started with "==" so it was reversed, so I just re-reversed and decoded it to get a photo where the flag can be read. <br> <br>
Tools used: Notepad++, www.base64decode.org <br>
<br>
<br>
<br>

## **Pwnable**
### **(50p) Attendance:**
#### Solver(s): JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357, PinkiePie1189#7418

This problem features a simple Buffer Overflow exploit. We saw that the port for the netcat connection was 31337, so we tried to call student #31337. Coincidentally, this was the input that let us send a message to the principal. We found by disassembling the program that the principal message input method was unprotected, so a buffer overflow on the EIP would be possible. We studied the objdump of the program and we saw that there was an unused function called *bring_students_to_school*. After some trial and error, we crafted an input string that writes directly the address of the function into the EIP register. The function opened a bash shell, so after we piped the overflow input string into netcat on the given IP, by also using the command cat- to interact with the shell, we were able to execute commands directly on the server. Thus, we did an ls, then cd'd into /home/attendance, ran *cat flag* and got the flag. <br> <br>

Tools used: gdb+gef, objdump, https://retdec.com, netcat <br>
<br>
<br>

### **(70p) C Party:**
#### Solver(s): JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357, PinkiePie1189#7418

This problem features another kind of Buffer Overflow. In Attendance, we had to override the EIP Register, but in CParty we had to override a value in memory (at $ebp - 0x14) that was compared to 0xc0defefe. We saw this by studying the disassembled code, and seeing that at one point the program would call "cat /home/party/flag" after running a cmp between the value at ($ebp - 0x14) and *0xc0defefe*. We studied our input and saw that it was allocated at an address smaller than $ebp-0x14, so overflowing $ebp-0x14 with our input should be easy. We then ran some tests and played with various input lengths until we saw the exact position of the bytes that would override $ebp-0x14. After writing *0xc0defefe* into the $ebp-0x14 address with the right bytes in our input string, the code would then proceed to run *cat /home/party/flag*. After running the program on the server with the overflowing input, we got our flag. <br> <br>

Tools used: gdb+gef, objdump, https://retdec.com, netcat <br>
<br>
<br>
<br>

## **Reverse**
### **(30p) History:**
#### Solver(s): PinkiePie1189#7418

This problem was trivial. You were given a Linux binary file which you could execute.The solution was actually inside the file itself, looking through it with a text editor as Notepad++ would reveal the flag but seperated with spaces. <br> <br>

Tools used: Notepad++ <br>
<br>
<br>

### **(150p) Math Exam:**
#### Solver(s): PinkiePie1189#7418, JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357, Gabies#3036

We decompiled the code using https://retdec.com/. After a few edits we were able to compile it on our local C++ IDE. We noticed that the "Master Key" was checked in 5 stages, and that it has to have >= 29 characters. We then saw that each check part was checking 6 characters each, so we could bruteforce each part, thus building our Master Key. When we saw that the first 6 characters were "timctf", we were convinced that the Master Key was indeed the flag. So after bruteforcing the rest of the characters (and bypassing some unpassable if statements), we obtained our flag. <br> <br>

Tools used: CodeBlocks <br>
<br>
<br>
<br>

## **Web**
### **(20p) Deery:**
#### Solver(s): Gabies#3036

In this problem we were given a link: deery.woodlandhighschool.xyz. Going through the web page source and looking through all of the files we get to another link: http://deery.woodlandhighschool.xyz/components/transition.js. Here just look up "timctf" and you find the flag. <br> <br>
Tools used: Google Chrome <br>
<br>
<br>

### **(50p) Porcupiney:**
#### Solver(s): JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357, PinkiePie1189#7418

We actually solved this problem by accident while trying to solve the easier problem Deery. We just changed the protocol from http to https on the deery link and Firefox came up with a warning, as shown in the following screenshot:
![Imgur Image](https://i.imgur.com/yUAVoKU.png)
Then we looked through nonononono.woodlandhighschool.xyz and at the bottom of the page we found the flag. <br> <br>
Tools used: Mozilla Firefox <br>
<br>
<br>

### **(50p) Watch Your Head:**
#### Solver(s): JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357

By using the Repeater from Burp Suite, we can send and re-send requests to carefully analize the response from the site. We can then notice that there are two interesting items sent, X-Data and Data-X. Upon further inspection, they seem to repeat. We list out the repetitions linearly and the flag should be formed. <br> <br>
Tools used: Burp Suite, Google Chrome <br>
<br>
<br>

### **(100p) Squirrels:**
#### Solver(s): PinkiePie1189#7418, JunkWub ✓ᵛᵉʳᶦᶠᶦᵉᵈ#7357

By using the Dirsearch utility we can see that the site has a .git folder, and plenty of files inside the .git folder that can be accessed and read. By using the Git Dumper utility, we downloaded the site's git repository, but the flag was not there and it looked there was a single commit and a single branch. Upon closer inspection, we noticed that the config file inside the .git folder contained the line [remote "fork"],which meant there was another remote called "fork" added to that git repository. By simply fetching that remote,and checking out into it,we quickly found the flag in the index.html file. <br> <br>
Tools used: DirSearch, Git, Git Dumper, Notepad++ <br>

<br>
<br>
<br>

