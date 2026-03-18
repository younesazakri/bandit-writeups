# OverTheWire Bandit Writeups
## **Introduction**

This repository contains my writeups for the OverTheWire Bandit wargame.
The goal of this project was to build a strong foundation in Linux, networking, and basic cybersecurity concepts.

Throughout these levels, I focused on understanding the underlying concepts rather than just solving the challenges.
Each level includes the goal, commands used, solution, and what I learned.

## Writeups
## Level 0
**Goal:**  
Log into the Bandit wargame server via SSH.  
**Commands:**  
ssh bandit0@bandit.labs.overthewire.org -p 2220  
**Solution:**  
I used the SSH command to establish a secure connection to the Bandit server and logged in using the password for level 0.  
**What I learned:**  
I learned how to connect to a remote Linux server using SSH.  
  
## Level 0 -> level 1
**Goal:**  
The password was stored in a file named readme. Find the file and read the password.  
**Commands:**  
ls  
cat readme  
**Solution:**  
I used the ls command to check if the file was in the directory. Then, I used the cat command to read the file and retrieve the password.  
**What I learned:**  
I learned how to view the contents of a directory and read the contents of a file.  
   
## Level 1 -> level 2
**Goal:**  
The password was hidden in a file named -.  
**Commands:**  
cat ./-  
**Solution:**  
I could not open the file using cat -, because - is interpreted differently. Instead, I specified the path by using cat ./- to read the file and retrieve the password.  
**What I learned:**  
I learned that files with special names like - cannot always be accessed in the usual way and may require specifying the file path.  
  
## Level 2 -> level 3
**Goal:**  
The password was hidden in a file with spaces in its name.  
**Commands:**  
cat "./--spaces in this filename--"  
**Solution:**  
I used quotes around the file name to handle the spaces. By writing the file name between quotes (e.g. cat "./--spaces in this filename--"), I was able to open the file and retrieve the password.  
**What I learned:**  
I learned that file names with spaces need to be handled carefully, and using quotes ensures that the full file name is interpreted correctly as a single argument.  
  
## Level 3 -> level 4
**Goal:**  
The password was stored in a hidden file inside the inhere directory.  
**Commands:**  
Cd inhere  
ls -a  
cat ...Hiding-From-You  
**Solution:**  
I navigated to the inhere directory using cd. Then, I used ls -a to list all files, including hidden ones. Finally, I used the cat command to read the file and retrieve the password.  
**What I learned:**  
I learned how to navigate between directories and how to display hidden files using ls -a.  
  
## Level 4 -> level 5
**Goal:**  
The password was stored in the only human-readable file in the inhere directory.  
**Commands:**  
cd inhere  
ls  
file ./-file0*  
cat ./file07  
**Solution:**  
I navigated to the directory and listed its contents. Then, I used the file command on each file to determine its type. Files labeled as “data” were not human-readable, while the file labeled as “ASCII text” contained readable content. I opened that file to retrieve the password.  
**What I learned:**  
I learned how to use the file command to identify the type of a file and distinguish between binary and human-readable files.  
  
## Level 5 -> level 6
**Goal:**  
The password was stored in a file with the following properties: human-readable, 1033 bytes in size, and not executable.  
**Commands:**  
find -type f -size 1033c \! -executable  
**Solution:**  
I used the find command to locate the file based on its properties. I specified -type f to search for regular files, -size 1033c to match the exact file size and \! -executable to exclude executable files. This allowed me to narrow down the search and find the correct file. I then opened the file to retrieve the password.  
**What I learned:**  
I learned how to use the find command to search for files based on specific properties such as type, size, and permissions.  
  
## Level 6 -> level 7
**Goal:**  
The password was located somewhere on the server and had the following properties: owned by user bandit7, owned by group bandit6, and 33 bytes in size.  
**Commands:**  
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null  
**Solution:**  
I used the find command to search the entire system for the file based on its properties. I specified -user bandit7 for the owner, -group bandit6 for the group, and -size 33c for the file size. I also used 2>/dev/null to suppress error messages, so only relevant results were shown. This allowed me to locate the correct file and retrieve the password.  
**What I learned:**  
I learned how to redirect error output to /dev/null, allowing me to ignore permission errors and focus only on useful results.  
  
## Level 7 -> level 8
**Goal:**  
The password was located in the file data.txt next to the word “millionth”.  
**Commands:**  
cat data.txt | grep "millionth"  
**Solution:**  
I searched for the word “millionth” in the file using the grep command. This allowed me to locate the correct line and retrieve the password.  
**What I learned:**  
I learned how to search for specific text within a file using the grep command.  
  
## Level 8 -> level 9
**Goal:**  
The password was stored in the file data.txt and was the only line that appeared once.  
**Commands:**  
sort data.txt | uniq -u  
**Solution:**  
I used the sort command to sort the contents of the file alphabetically. Then, I used uniq -u to display only the line that appeared once. This allowed me to identify the password.  
**What I learned:**  
I learned how to sort file contents and how to extract unique lines using the uniq command.  
  
## Level 9 -> level 10
**Goal:**  
The password was stored in the file data.txt, hidden among readable strings and preceded by multiple = characters.  
**Commands:**  
strings data.txt | grep "="  
**Solution:**  
I used the strings command to extract human-readable text from the file. Then, I searched for lines containing multiple = characters using grep. This allowed me to locate the correct string and retrieve the password.  
**What I learned:**  
I learned how to extract readable text from binary files using the strings command and how to filter the output using grep.  
  
## Level 10 -> level 11
**Goal:**  
The password was stored in the file data.txt, which contained base64-encoded data.  
**Commands:**  
base64 -d data.txt  
**Solution:**  
I used the base64 command with the -d flag to decode the contents of the file. This revealed the original text, allowing me to retrieve the password.  
**What I learned:**  
I learned how to decode base64-encoded data using the base64 command.  
  
## Level 11 -> level 12
**Goal:**  
The password was stored in the file data.txt, where all lowercase (a–z) and uppercase (A–Z) letters were rotated by 13 positions.  
**Commands:**  
cat bestand.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'  
**Solution:**  
I used the tr command to reverse the ROT13 encoding. I specified the input range A-Za-z and mapped it to N-ZA-Mn-za-m, which shifts each letter by 13 positions back to its original form. This allowed me to decode the text and retrieve the password.  
**What I learned:**  
I learned how to reverse ROT13 encoding using the tr command.  

## Level 12 -> level 13
**Goal:**  
The password was stored in the file data.txt, which contained a hexdump of a repeatedly compressed file.  
**Commands:**  
xxd -r data.txt > hex  
file hex  
zcat hex | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat | file –  
zcat hex | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat  
**Solution:**  
I first reversed the hexdump using xxd -r to restore the original binary file. Then, I used the file command to identify the file type. Based on the detected compression method (e.g. gzip, bzip2, tar), I used the appropriate command to decompress the file. I repeated this process—checking the file type and decompressing—until the file was no longer compressed and I could retrieve the password.  
**What I learned:**  
I learned how to reverse a hexdump using xxd -r and how to identify and decompress different file formats step by step.  

## Level 13 -> level 14
**Goal:**  
The password was stored in /etc/bandit_pass/bandit14 and could only be read by user bandit14. Instead of a password, I was given a private SSH key to log in to the next level.  
**Commands:**  
cat sshkey.private  
nano bandit14.key  
chmod 600 bandit14.key  
ssh -i bandit14.key bandit14@bandit.labs.overthewire.org -p 2220  
**Solution:**  
I opened the private key file and copied its contents. Then, I went back to my Kali machine and created a new file to store the key. I pasted the key into the file and changed its permissions using chmod to make it secure. Finally, I used the key to log in to bandit14 via SSH.  
**What I learned:**  
I learned how to use a private SSH key to authenticate and log in to a remote server.  

## Level 14 -> level 15
**Goal:**  
The password could be retrieved by sending the password of the current level to port 30000 on localhost.  
**Commands:**  
cat /etc/bandit_pass/bandit14  
nc localhost 30000  
**Solution:**  
I first retrieved the password of the current level from /etc/bandit_pass/bandit14. Then, I used the nc (netcat) command to connect to localhost on port 30000. After establishing the connection, I sent the password as input and received the password for the next level.  
**What I learned:**  
I learned how to connect to a specific port using nc (netcat) and how to send input over a network connection.  

## Level 15 -> level 16
**Goal:**  
The password could be retrieved by sending the password of the current level to port 30001 on localhost using SSL/TLS encryption.  
**Commands:**  
openssl s_client -connect localhost:30001  
**Solution:**  
I used the openssl s_client command to establish a secure connection to localhost on port 30001. This allowed me to communicate over an SSL/TLS-encrypted channel. After connecting, I sent the current password as input and received the password for the next level.  
**What I learned:**  
I learned that some services use SSL/TLS encryption, and that I need to use the appropriate tools to interact with them. As a pentester, it is important to understand the difference between testing plain TCP services and encrypted TLS services.  

## Level 16 -> level 17
**Goal:**  
The credentials could be obtained by sending the password of the current level to a port on localhost within the range 31000–32000. I first had to identify which ports were open and which ones supported SSL/TLS. Only one server would return the correct credentials.  
**Commands:**  
nmap -sV -p31000-32000 localhost  
openssl s_client -connect localhost:31790 -quiet  
**Solution:**  
I used nmap to scan the port range 31000–32000 on localhost to identify open ports and detect which services were running. Based on the scan results, I determined which port supported SSL/TLS. I then connected to that port using the appropriate tool and sent the current password as input. This returned the credentials for the next level.  
**What I learned:**  
I learned how to scan a range of ports using nmap and how to identify services and encryption protocols running on those ports.  

## Level 17 -> level 18
**Goal:**  
There were two files in the home directory: passwords.old and passwords.new. The password was in passwords.new and was the only line that had changed between the two files.  
**Commands:**  
diff passwords.old passwords.new  
**Solution:**  
I used the diff command to compare both files and identify the difference. This allowed me to locate the modified line in passwords.new, which contained the password.  
**What I learned:**  
I learned how to compare files and identify differences using the diff command.  

## Level 18 -> level 19
**Goal:**  
The password was stored in a file named readme in the home directory. However, the .bashrc file had been modified, causing an automatic logout whenever I logged in via SSH.  
**Command:**  
scp -P 2220 bandit18@bandit.labs.overthewire.org:/home/bandit18/readme /home/kali  
cat /home/kali/readme  
**Solution:**  
Since I was immediately logged out after connecting via SSH, I needed an alternative way to access the file. I used the scp command to securely copy the file from the remote server to my local machine without opening an interactive SSH session. I specified the port using -P, provided the username and host, and included the path to the file. Finally, I defined the destination on my local machine to download the file and retrieve the password.  
**What I learned:**  
I learned how to use scp to securely transfer files from a remote server without needing to interact with the system through an SSH session.  

## Level 19 -> level 20
**Goal:**  
To access the next level, I had to use the setuid binary bandit20-do in the home directory. The password was stored in the usual location (/etc/bandit_pass) and could be accessed after using the binary.  
**Commands:**  
./bandit20-do  
./bandit20-do cat /etc/bandit_pass/bandit20  
**Solution:**  
I executed the bandit20-do binary without arguments to understand how it worked. It returned the message: “Run a command as another user. Example: ./bandit20-do whoami”. This indicated that I could execute commands as the user bandit20. I then used this binary to run a command that read the password file, allowing me to retrieve the password with elevated privileges.  
**What I learned:**  
I learned how to use a setuid binary to execute commands with the privileges of another user, which can be used for privilege escalation.  

## Level 20 -> level 21
**Goal:**  
In the home directory, there was a setuid binary that connected to localhost on a port I specified as a command-line argument. It would read a line from the connection and compare it to the password of the previous level (bandit20). If the password was correct, it would return the password for the next level (bandit21).  
**Commands:**  
nc -l 40000  
./suconnect 40000  
**Solution:**  
I used two terminals for this level. In the first terminal, I started a listener using the nc (netcat) command with the -l flag on a chosen port. In the second terminal, I executed the ./suconnect binary and provided the same port number. Once the connection was established, I sent the current password through the listener in the first terminal. The binary verified the password and returned the password for the next level.  
**What I learned:**  
I learned how programs can communicate with each other over network ports, where one program listens on a port and another connects to it, allowing data to be exchanged.  

## Level 21 -> level 22
**Goal:**  
A program was automatically executed at regular intervals by cron, a time-based job scheduler. I had to inspect /etc/cron.d/ to identify which command was being executed.  
**Commands:**  
ls /etc/cron.d  
cat /etc/cron.d/cronjob_bandit22  
cat /usr/bin/cronjob_bandit22.sh  
cat / tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv  
**Solution:**  
I first listed the files in the /etc/cron.d/ directory and found a file named cronjob_bandit22. I opened this file to see which command was being executed. It pointed to a script located at /usr/bin/cronjob_bandit22.sh. I then read the contents of this script and discovered that it generated the password and stored it in a temporary file at /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv. Finally, I read this file to retrieve the password.  
**What I learned:**  
I learned that cron jobs can expose sensitive information by writing data to temporary files. If these files have weak permissions, other users may be able to read them. This is a common misconfiguration that pentesters can exploit.  

## Level 22 -> level 23
**Goal:**  
A program was automatically executed at regular intervals by cron. I had to inspect /etc/cron.d/ to determine which command was being executed.  
**Commands:**  
ls /etc/cron.d  
cat /etc/cron.d/cronjob_bandit23  
cat /usr/bin/cronjob_bandit23.sh  
myname=bandit23  
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)  
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"  
cat /tmp/8ca319486bfbbc3663ea0fbe81326349  
**Solution:**  
I checked the cron jobs in /etc/cron.d/ and found the file cronjob_bandit23. This file pointed to a script located at /usr/bin/cronjob_bandit23.sh. After reading the script, I saw that it generated a filename based on a username using a hash function and then wrote the password to a file in /tmp.
Since I was logged in as bandit22, the script generated a file for that user. I analyzed how the filename was created and manually reproduced the same process for the user bandit23. This allowed me to determine the correct filename in /tmp and retrieve the password from that file.  
**What I learned:**  
I learned how to analyze scripts to understand how data is generated and stored, and how to replicate that logic to retrieve sensitive information.  

## Level 23 -> level 24
**Goal:**  
A program was automatically executed at regular intervals by cron. I had to inspect /etc/cron.d/ to determine which command was being executed. For this level, I needed to create my own shell script.  
**Commands:**  
ls /etc/cron.d  
cat /etc/cron.d/cronjob_bandit24  
cat /usr/bin/cronjob_bandit24.sh  
mkdir /tmp/tijdelijk  
cd /tmp/tijdelijk  
nano getpass.sh  
#!/bin/bash  
cat /etc/bandit_pass/bandit24 > /tmp/pass_bandit24  
chmod +x getpass.sh  
cp getpass.sh /var/spool/bandit24/foo  
**Solution:**  
I checked the cron jobs in /etc/cron.d/ and found cronjob_bandit24, which pointed to the script /usr/bin/cronjob_bandit24.sh. After reading the script, I understood that it executed all files in /var/spool/bandit24/foo that were owned by bandit23, and then deleted them.
This meant I could create my own script as bandit23 and place it in that directory to have it executed with the privileges of bandit24.
Since I did not have write permissions in that directory directly, I created a script in /tmp, where I had write access. The script contained a command to read the password of the next level and write it to a file in /tmp.
I made the script executable using chmod, then copied it to /var/spool/bandit24/foo. After the cron job executed the script, I read the output file in /tmp to retrieve the password.  
**What I learned:**  
I learned how to analyze more complex scripts and understand their behavior. I also learned how cron jobs can be abused to execute my own code with higher privileges. Additionally, I learned the importance of write permissions and how temporary directories like /tmp can be used to store and execute scripts.  

## Level 24 -> level 25
**Goal:**  
A daemon was listening on port 30002 and would return the password for bandit25 if I sent the password for bandit24 along with a secret 4-digit PIN. The only way to find the PIN was by brute-forcing all 10,000 possible combinations.  
**Commands:**  
mkdir /tmp/tijdelijk  
nano script.sh  
#!/bin/bash  
for i in {0000..9999};  
do echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i";  
done | nc localhost 30002  
chmod +x script.sh  
./script.sh  
**Solution:**  
I created a script to generate all possible 4-digit PIN combinations (from 0000 to 9999). For each combination, I sent the current password together with the PIN to the daemon using nc (netcat).
I used a loop to iterate through all possible PINs and formatted the input correctly so it matched what the daemon expected. The output of the loop was then piped into nc localhost 30002. Once the correct PIN was sent, the daemon returned the password for the next level.  
**What I learned:**  
I learned how to use loops in Bash to automate repetitive tasks and how to perform a brute-force attack by sending multiple inputs to a service.  

## Level 25 -> level 26
**Goal:**  
Logging into bandit26 from bandit25 was not straightforward because the shell for user bandit26 was not /bin/bash. I needed to identify which shell was being used, understand how it worked, and find a way to escape it.  
**Commands:**  
cat /etc/passwd | grep “bandit26”  
cat /usr/bin/showtext  
cat bandit26.sshkey  
nano bandit26.key  
chmod 700 bandit26.key  
:set shell?  
:set shell=/bin/bash  
:!/bin/bash  
**Solution:**  
In the home directory of bandit25, I found a private key for bandit26. I copied it to my local machine and used it to log in. However, I was immediately logged out.
To understand why, I checked /etc/passwd and saw that bandit26 used /usr/bin/showtext as its shell. I then examined this file and found the following script:  
#!/bin/sh  
Export TERM-Linux  
Exec more ~/tekst.txt  
Exit 0  
This showed that the more command was executed automatically upon login.  
To prevent immediate logout, I resized my terminal window so that more would not exit instantly. While inside more, I pressed v to open the file in vi.
From within vi, I was able to spawn a shell by executing a command (e.g. :!/bin/bash). This gave me access to a shell as bandit26.  
**What I learned:**  
I learned how to identify which shell a user is using and how to analyze custom shell scripts. I also learned how to escape restricted environments (like more) and use tools like vi to spawn a shell.  

## Level 26 -> level 27
**Goal:**  
After gaining access to a shell as bandit26, I needed to retrieve the password for bandit27.  
**Commands:**  
./bandit27-do  
./bandit27-do cat /etc/bandit_pass/bandit27  
**Solution:**  
I used the available setuid binary to execute a command with elevated privileges. This allowed me to read the password file for bandit27 from /etc/bandit_pass and retrieve the password.  

## Level 27 -> level 28
**Goal:**  
A Git repository was available at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo on port 2220. The password for user bandit27-git was the same as for bandit27. I needed to clone the repository on my local machine and find the password for the next level.  
**Commands:**  
mkdir bandit27  
cd bandit27  
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo  
cat /repo/README  
**Solution:**  
I created a directory on my local Kali machine to store the cloned repository. Then, I used the git clone command with the SSH URL and specified the correct port. After cloning the repository, I explored its contents and found a file named README. I opened this file and retrieved the password for the next level.  
**What I learned:**  
I learned how to clone a remote Git repository using SSH and how to inspect its contents locally.  

## Level 28 -> level 29
**Goal:**  
A Git repository was available at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo on port 2220. The password for user bandit28-git was the same as for bandit28. I needed to clone the repository and find the password for the next level.  
**Commands:**  
mkdir bandit28  
cd bandit28  
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo  
git log README.md  
git show README.md  
**Solution:**  
I cloned the repository to my local machine and explored its contents. When I opened the README.md file, I noticed that the password was hidden.
To investigate further, I checked the commit history of the repository. I found a commit message that indicated a “fix info leak”, which suggested that the password had previously been exposed.
I then compared the current version of the file with earlier versions using Git history. By reviewing the previous commit, I was able to see the original content and retrieve the password.  
**What I learned:**  
I learned how to inspect the history of a Git repository and how sensitive information can still be accessible even after it has been removed from the latest version.  

## Level 29 -> level 30
**Goal:**  
A Git repository was available at ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo on port 2220. The password for user bandit29-git was the same as for bandit29. I needed to clone the repository and find the password for the next level.  
**Commands:**  
mkdir bandit29  
cd bandit29  
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo  
git log README.md  
git show README.md  
git branch -a  
git checkout remotes/origin/dev  
**Solution:**  
I cloned the repository to my local machine and inspected its contents. After opening the README.md file, I found no useful information. I then checked the commit history, but it did not reveal the password.
Next, I enumerated the available branches and discovered a branch named developer. I switched to this branch and inspected its contents. In this branch, the README.md file contained the password for the next level.  
**What I learned:**  
I learned that Git repositories can have multiple branches with different content, and that sensitive information may be exposed in branches other than the main branch.  

## Level 30 -> level 31
**Goal:**  
A Git repository was available at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo on port 2220. The password for user bandit30-git was the same as for bandit30. I needed to clone the repository and find the password for the next level.  
**Commands:**  
mkdir bandit30  
cd bandit30  
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo  
git log README.md  
git show README.md  
git branch -a  
git checkout remotes/origin/master  
git checkout remotes/origin/HEAD  
git tag -l  
git show secret  
**Solution:**  
I cloned the repository to my local machine and began exploring its contents. I first checked the commit history, but there were no previous versions containing useful information. Then, I inspected the available branches, but did not find anything relevant.
Next, I examined the Git tags and discovered a tag named secret. I inspected this tag and found that it contained the password for the next level.  
**What I learned:**  
I learned that Git repositories contain more than just commits and branches. Tags can also store important information, and sensitive data may be exposed through them.  

## Level 31 -> level 32
**Goal:**  
A Git repository was available at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo on port 2220. The password for user bandit31-git was the same as for bandit31. I needed to clone the repository and find the password for the next level.  
**Commands:**  
mkdir bandit31  
cd bandit31  
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo  
cat README.md  
nano key.txt  
git add -f key.txt  
git config --global user.email "bandit31@localhost"  
git config --global user.name "bandit31"  
git commit key.txt  
git remote -v  
git push origin master  
**Solution:**  
I cloned the repository to my local machine and inspected its contents. The README.md file instructed me to create a specific file and push it to the remote repository.
I created the required file and attempted to commit it. Before committing, I configured my Git username and email, as Git requires this information. After that, I added the file, created a commit, and checked the name of the remote repository.
Finally, I pushed the commit to the remote repository. After pushing, I received the password for the next level.  
**What I learned:**  
I learned how to configure Git, create commits, and push changes to a remote repository.  

## Level 32 -> level 33
**Goal:**  
After the Git levels, I was placed in a restricted uppercase shell. I needed to escape this environment to access the next level.  
**Commands:**  
$0  
cat /etc/bandit_pass/bandit33  
**Solution:**  
I identified that I was in a restricted uppercase shell that prevented normal command execution. After researching how this shell worked, I found a way to escape it and spawn a usable shell. Once I had access to a normal shell, I retrieved the password for the next level from /etc/bandit_pass.  
**What I learned:**  
I learned how to escape a restricted shell environment and regain access to normal command execution.  

## Overall What I Learned
•	Gained strong fundamentals in Linux commands and navigation  
•	Learned how to enumerate systems and identify useful files and services  
•	Developed a mindset for solving problems step-by-step  
•	Understood how privilege escalation works in different scenarios  
•	Gained experience with networking tools like netcat and openssl  
•	Learned how to analyze Git repositories for sensitive information  
•	Practiced basic exploitation techniques such as brute-forcing and script analysis  
