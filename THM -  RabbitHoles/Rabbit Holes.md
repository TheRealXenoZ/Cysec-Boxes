# Rabbit Holes

### [TryHackMe Box](https://tryhackme.com/room/rabbitholes) by CYSEC CLUB, GITAM 

This box is geared towards *beginners* who are interested in getting into the beautiful world of cybersecurity and pentesting.

The theme of this box revolves around the fundamentals of Linux and bash.

Make sure you use this write-up only when you are really stuck at a point and don't understand how to move forward, because usually ==the answer is right infront of you.==

> "Try harder!" - The official motto of Offensive-Security 

---

#### Resources used:

* [CyberChef (gchq.github.io)](https://gchq.github.io/CyberChef/)
* [dCode](https://www.dcode.fr/)
* [CrackStation](https://crackstation.net/)

------

## Flags :

This writeup consists of the way I went about with the given tasks, be mindful that there might be several other ways to do the same task. 

#### Flag 1:

- You are given the first flag when you SSH into the client
- You can log into the user<number on the flag> with the flag as password.
- user1 : user1{dd7536794b63bf90eccfd37f9b######}

---

#### Flag 2:

* This flag requires you to use the "ls" command
* This command displays ("**l**ist**s**") all the files in the current directory.
* syntax : ls {location of the directory}
* The 2nd flag is the name of the folder you see after you type "ls".
* user2 : user2{8c728e685ddde9f7fbbc452155######}

---

#### Flag 3:

* This flag requires you to use the "cat" command.
* "cat" command is used to read **any** file.
* using "ls" reveals flag.txt file. use "cat" to read the contents, which reveal the flag
* user3 : user3{639bae9ac6b3e1a84cebb7b403######}

---

#### Flag 4:

* When you first get into the box, you can see a random string of characters which look like they represent the flag in reverse

* Copy that and paste into the console

* I reversed the flag using rev command of bash, but this can be done in multiple different ways :

  ```bash
  echo }aea67de3611db4c03d32d862a565f9c5{4resu | rev
  ```

* user4 : user4{5c9f565a268d23d30c4bd1163e######}

---

#### Flag 5:

* uses -la option of ls to "list all"

* ```bash
  ls -la
  cat .flag.txt
  ```

* user5 : user5{9e925e9341b490bfd3b4c4ca3b######}

---

#### Flag 6:

* Further uses -la option but with decoy flags and folders to throw us off.

* ```bash
  ls -la
  cd .flag
  ls -la
  cat .flag.txt
  ```

* user6 : user6{a8db1d82db78ed452ba0882fb9######} 

---

#### Flag 7:

* Multiple decoy folders are present. using recursive finding to make it easy to find the flag

* ```bash
  find . * | grep flag
  cat 'f/i/n/d/ /c/m/d/ /m/a/k/e/ /w/o/r/k/ /e/a/s/i/e/r/ /i_am_flag.txt'
  ```

* user7 : user7{b04ec0ade3d49b4a079f0e207d######}

---

#### Flag 8:

* Presented with multiple dictionaries

* use grep to find a given string in the given dictionaries

* ```bash
  ls -la
  cat .rockyou.txt | grep "user8{"
  ```

* user8 : user8{ffcf70e892b8ac3facbac0f886######}

---

#### Flag 9:

* I solved it by using the "-r" flag of grep to find a given string in the files/folders

* ```bash
  grep -r "user9{"
  ```

* user9 : user9{0a7d55be9d12a369a6a8da0fb5######}

---

#### Flag 10:

* uses -la option of "ls"

* checking through files using "cat" command

* Flag present in .bashrc

* ```bash
  cat .bashrc
  ```

* user10 : user10{ff1ccf57e98c817df1efcd9fe4######}

---

#### Flag 11:

* same as the previous flag, I solved it used grep command

* ```bash
  cat .bash_history | grep "user11"
  ```

* user11 : user11{8e13ffc9fd9d6a6761231a764b######}

---

#### Flag 12:

* same as the previous flag. the provided flag.txt gives clues onto which file to check for.

* ```bash
  cat .viminfo | grep "user12"
  ```

* user12 : user12{13b5bfe96f3e2fe411c9f66f4a######}

---

#### Flag 13:

* Given flag.txt has encrypted data, which on a closer inspection turns out to be base64
* I used Cyberchef to decode the base64 data
* user13 : user13{ee20fd29e100990f661f3f1479######}

---

#### Flag 14:

* Given flag.txt is encrypted, which on closer inspection turns out to be base32
* After the initial decoding, it is still in base32 format, so decode again to reveal the flag
* This flag acts as a precursory reminder to expect multiple layers of encryption ahead
* user14 : user14{bd4c4ea1b44a8ff2afa18dfd26######}

---

#### Flag 15:

* The given flag is a double hex encoded flag.
* Auto decoding in cyberchef doesn't work efficiently in these situations.
* user15 : user15{6b393b6b209b981e9c552d3d38######}

---

#### Flag 16:

* The given flag is a double decimal encoded flag. 
* As was with case of Flag 15, Auto-decoding (Magic) doesn't work efficiently.
* user16 : user16{a77b3598941cb803eac0fcdafe######}

---

#### Flag 17:

* This flag is a double octal encoded flag. 

  * > Awful lot of doubles eh? Trust me it's gonna become much more difficult.

* As was the case with previous flags, Auto-decoding is sketchy

* user17 : user17{0cc175b9c0f1b6a831c399e269######}

---

####  Flag 18:

* This flag is a simple binary decode
* Cyberchef might require some digging around to get your required result

* user18 : user18{b04ec0ade3d49b4a079f0e207d######}

---

#### Flag 19:

* This flag is a simple ROT47 Decode

  * > Went from doubles to simple single encryptions hasn't it? Wait for it...

* The difficulty with one is identifying the Cipher, The initial flag.txt gives a good idea it is a rotating cipher.

* user19 : user19{13b5bfe96f3e2fe411c9f66f4a######}

---

#### Flag 20:

* This box requires you to be good at most of the things you have done up until now

* Even I was stumped for a few minutes on what to do due to the chain of commands required  ( _and also because I only had a few hours of sleep_ 😓).

* This flag requires you to recurse through multiple folders placed in a layout of trees. I solved it by finding all the files in the folders and grepping them for flag.

* Be careful when copying the paths to get the flag, as the spaces also come under the  name of the path

* Once you find the flag (and avoid the fake ones) , you'll notice that you are unable to do anything with it. Checking with ls -la shows that it has no permissions given to it.

* This needs to give you the hint to use chmod and give permissions to it as the file is owned by you.

  ###### Entire shell command to search for flags and read it:

  ```bash
  find . * | grep flag
  chmod +rw './   -----   /t/r/e/e/ /flag.txt'
  cat './   -----   /t/r/e/e/ /flag.txt'

* You will notice that the text is still encrypted.
* This requires you to run the text through multiple chains of encryption to decode.
* It is also helpful to ==notice the patter you are decoding in==, Trust me when I say this.

* Also, dcode.fr 's cipher detection feature will help you alot here.

* user20 : user20{53d8f4d1e2b5be0d0abfde443f######}

---

#### Flag 21:

* The given flag states that there is stored variable with the flag value
* I used printenv to print the environment variables and grepped for user21

* ```bash
  printenv | grep user21
  ```

* user21 : user21{8fc42c6ddf9966db3b09e84365######}

---

#### Flag 22: 

* Here we are given a flag.txt and a python executable.
* The challenge originally intended us to find a number which follows the given logic in the program and get the flag, but....
* Being the lazy pentester I am, I just copied the required hex bytes and decoded it manually to reveal the path of the location of flag.

* This kind of thought process helps alot in the world of cysec.

* I encourage you to check the executable yourself and solve it in a way you'd like to.
  * Also I didn't paste the location of flag to help you guys explore and understand.

* user22 : user22{5f4dcc3b5aa765d61d8327deb8######}

---

#### Flag 23:

* Just like the previous one, we are presented with a dummy flag and an executable but this time, It is a C executable.

* Just like before, I just wanted to get the flag as soon as possible, So I copied the source code onto my local machine and skimmed through the code.
* I found a breakpoint and bypassed the entire logic to get me my flag path.
* And just like previous flag, I am not putting the path here to help you guys learn and understand by exploring.
* user23 : user23{d55669822f1a8cf72ec1911e46######}

---

#### Flag 24:

* Like the previous one but with a Java file.
* Reading the file gives you the path of the flag in plain sight, so should be an easy flag.

* ```bash
  cat flag.java
  cat <location of flag from the java file>
  ```

* user24 : user24{8fc42c6ddf9966db3b09e84365######}

---

#### Flag 25:

* Since the previous java one was really simple, I decided to just execute the ruby file (_and also because I'm a big dumb dumb with ruby_) and Boom! we just get the flag.

* user25 : user25{ee11cbb19052e40b07aac0ca06######}

---

#### Flag 26:

* When we enter the user, we are greeted with a hideous looking file with multiple extensions. This flag demonstrates a simple **matryoshka doll** concept 
* Uhh, just stop bruteforcing the moment you see known extensions. Recon in these kind  of cases is really helps to save you some time and a whole lot of stress.

* To keep my sanity, I renamed my original file to flag.orginal.

* using "file" command I get to know that it is a .tar archive

* Uncompressing it gives us a .zip file

* Uncompressing that gives us a .xz archive

* Uncompressing that gives us a gunzip archive

* We get our flag after uncompressing the final gunzip archive.

  * ###### Shell commands I used :

    ```bash
    mv flag.<random junk> flag.original
    file flag.original
    tar -xvf flag.original
    unzip flag.gz.xz.zip
    xz -d -v flag.gz.xz
    gunzip flag.gz
    cat flag
    ```

* user26 : user26{e6cc3fa15a672b3c6fc579b30c######}

---

#### Flag 27: 

* In this flag challenge, you are given a image file

* Just a friendly tip which I learned over the years of practice, wheneven you are faced with an image or a non-text file, just run "strings" on it.

* strings shows all the metadata stored with the file

* lucky for us, it was sufficient.

* ```bash
  strings "<name of image" | grep user27
  ```

* user27 : user27{a2a551a6458a8de22446cc76d6######}

---

#### Flag 28:

* Reading the initial dummy flag gives us the clue that the flag is hidden within the dummy flag
* I used "less" since it is a dumbed-down version VI, the invisible data was visible just infront of the dummy flag header.

* user28 : user28{6c1230bf15e7c89e1668de0157######}

---

#### Flag 29:

* The dummy flag gives an exact idea what to do. The explicit mention of passwd made me check /etc/passwd.

* ``` bash
  cat /etc/passwd | grep user29
  ```

* user29 : user29{56ab24c15b72a457069c5ea42f######}

---

#### Flag 30:

* Checking the dummy flag, The clue suggests something hidden in the plain sight.
* I checked the .bashrc file and found a suspicious command
* Running the command just gave me the flag :laughing:

* ```bash
  cat .bashrc
  echo "==QfhV2NzMDN3ITZidzN3QWZjljMjZGNkNjZ1YzN0YjYhR2ewMjclNXd" |rev|base64 -d
  ```

* user30 : user30{dab64765f3d4fc29ced777be27######}

---

#### Flag 31:

* This and the remaining flags ahead require you to be good at researching and finding out about your environment.

* In Flag 31, you are locked in a python environment. But since we have the whole environment, we can break out of it and spawn a **tty shell** pretty easily

* I just used a simple pty import and spawned a bash shell and found the flag in the home directory.

* ```python
  >>> import pty
  >>> pty.spawn("/bin/bash")
  $ cat flag.txt
  ```

* user31 : user31{df3f079de6961496f0460dcfdb######}

---

#### Flag 32:

* Similar to the previous one but this time we are locked in a ruby shell
* we can break out of ruby environment to spawn a **tty shell** pretty easily by just executing a binary using exec() command.
* after spawning the shell, we find a dummy flag a clue hinting towards ids. I just ran "id" and searched for all the files belonging to me and my groups by using "find" command

* after searching for a while I found an odd looking file in /apt/ directory with the same letters as in the clue flag.

* ```bash
  exec "/bin/bash"
  cat flag.txt
  cat /**r/**g/apt/i_4m_U53R32 #censored to help you explore and learn
  ```

* user32 : user32{f894427cc1c571f79da49605ef######}

---

#### Flag 33:

* Even though not as difficult as the previous flag, This flag still poses a challenge if you don't know what to do.

* In this challenge, we are locked in an environment with no essential binaries such a ls, cat, etc.

* This challenge encourages you to explore and find alternative ways to read files,  check what files are in a directory, etc.

* I solved this challenge by using the echo command.

* ```bash
  echo * #Lists all files in a directory (similar to ls)
  echo "$(<flag.txt)" #Prints the flag contents (similar to cat)
  ```

* user33 : user33{77498ff764fc0a34cafdad2c70######}

---

#### Web Flag:

* The name of the flag / challenge should give you an idea to check the IP you guys used to SSH to check for a web-frontend.
* Accessing the IP brings us to a blog with 4 subsections and you can already see the flag section.
* opening the flag section gives us the web-flag but also clue regarding the next flag.
* webflag : flag{2e781e46cd473612f108b29a62######}

---

#### Alienone password:

* From the above clue, I just copied and pasted the md5sum salts into a text file and ran those through CrackStation (_Free online database  to check hashes if they are already cracked, saving us a huge amount of time_).

* And within a few seconds, I got the password.

* Password : T#eL##t#### (_censored it to not spoil the fun of exploring_)

---

#### Root Flag:

* Here we are, The end of line. If you remember all the things which you have learned till now, This flag should be a breeze for you. I'm gonna write my shell command history so you guys get an Idea, If you are really stuck.

* ```bash
  sudo -s
  cd /root/
  grep -r "{"
  ```

* root : root{<censored>}

---

---

## Conclusion :

I really liked the way the box grew in difficulty where even the most difficult point felt simple after understanding the clue and the idea behind it. I hope **CYSEC GITAM, Hyderabad** hosts more of these THM / Hackthebox based challenges in the future to get more people into the beautiful world of cybersecurity.

​								

​																																Marked by :

​																																	 **XenoZ**

