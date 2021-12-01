# Overview of application

1. there is two endpoints called `/docker` and `/curl`. and The `/docker` endpoints will show the scripts of dockerfile and `/curl` endpints is just a curl service.
2. In line `35` of main.py, you can see the following command for curl with python. `return run(["curl", "-L", "--max-time", "1", "--max-filesize", "1000",  url], capture_output=True).stdout.decode()`
3. So, From this line, we can know that he is using the actually curl with python. If you familar with curl, you will know that we can read files from our local machine with curl service too. (read this: [Curl-file-service](https://security.stackexchange.com/questions/196842/is-it-possible-to-execute-a-local-file-or-code-from-curl)) (Example: curl **file:///etc/passwd**, curl **"file:///etc/shadow**")
4. So, we can read files from service now. (Example: **file:///etc/passwd**) **Note: We don't need to add curl because in main.py it is already excuting the curl**
5. But this challenge is not just that. There is a `/docker`  endpoints that show the scripts of dockerfile. 
6. Let me show you the important line of this dockerfile. ```RUN useradd -ms /bin/bash newuser
COPY flag.txt .
RUN echo "newuser:$(cat flag.txt | sed 's/ictf{//; s/}//')" | chpasswd && rm flag.txt```
7. As you can see the serval of commands are running in just one line.
8. So let me explain about it, let start from first line. `useradd -ms /bin/bash newuser`. THis line is not have any tricks. It is just add newuser called `newuser` with the `/bin/bash`. (Read this: [about-useradd](https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/))
9. The second line have many tricks. There are `5` commands in one line. 
10. (1.`cat flag.txt`, 2.`sed 's/ictf{//; s/}//')"`, 3. `chpasswd`, 4. `&&` 5.`rm flag.txt`)
11. But the real important in this line is using `echo`. Example explain of puzzler7: `the syntax $(some_command_here) executes the command and puts the output of it inside the outer command`, `for instance, cat $(echo "flag.txt")` is the same as `cat flag.txt`
12. and `chpasswd` is a linux command to change the password for `newuser`
13. and `rm flag.txt` is simple. But you might thinking like you remove the flag.txt and how can we read now the flag? Well, let me explain
14. Before the remove the flag.txt and he change the password of `newuser` to `flag.txt`.
15. Actually the changed password is not `flag.txt`, the content from `flag.txt`. For exmaple: in the flag.txt file have string called `test_flag`. the changed password will be `test_flag`. Just that. linux tricks. Right?
16. So we know that our flag is the `password` of `newuser`. So the password of users in linux is stored in `/etc/shadow`. And got the hashes of password and crack it and got flag.

# Solution
`file:///etc/shadow` and crack the hashes of newuser with hascat `hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt -O`. and got flag. 
`ripcurlgurl` and `ictf{ripcurlgurl}`

# flag
ictf{ripcurlgurl}

Thanks!
