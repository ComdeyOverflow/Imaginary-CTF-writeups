# File Formats

In this round 16, i made two challenges. THis is one of the challenges of it.
Really easy and also funky

# Solution
From the flag.zip will output the secret.rar and in secret.rar (need to bruteforce the rar password) 

password is `12345`

In the rar file, there is a png file called extension.png that hide the flag.txt inside of it. 

but you can't solve with steghide or something because it is not a real png file. 

Actually it is a zip file so the player need to unzip or change the file extension to `.zip` from `.png` and got flag. Simple and not easy.

# My intended solution
unzip flag.zip
unrar e secret.rar (need password)
use this online rar bruteforcer [Online Rar password bruteforcer](https://www.lostmypass.com/file-types/rar/)
unrar e secret.rar (12345)
unzip extension.png
cat flag.txt

# flag
ictf{n0_1dea_h0w_t0_ge1_g1rL_fr1end!!} 

# Quick Note
If you are girl that reading this writeup, can you be my girlfriend?

# Connect me
Comdeyoverflowa#1279

