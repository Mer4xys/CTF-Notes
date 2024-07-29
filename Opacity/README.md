
Open Ports

22 OpenSSH 8.2p1

80 Apache httpd 2.4.41

139 Samba smbd 4.6.2

445 Samba smbd 4.6.2

Enumeration

When we access the webserver we are provided with a login screen

Feroxbuster finds a cloud directory

It's an image upload website that of course accepts only image files

But it's possible to bypass this restriction by adding a space after the extension of the file that you want to upload

If you want to upload a shell.php just put shell.php .jpg and the file will upload successfully

Privilege escalation

In the opt directory there is a dataset.kdbx file

It's a Keepass password database

We can extract the hash:

keepass2john dataset.kdbx > forjohn.txt

And crack it with John:

john --wordlist=/usr/share/wordlists/rockyou.txt forjohn.txt 
Created directory: /home/kali/.john
Using default input encoding: UTF-8
Loaded 1 password hash (KeePass [SHA256 AES 32/64])
Cost 1 (iteration count) is 100000 for all loaded hashes
Cost 2 (version) is 2 for all loaded hashes
Cost 3 (algorithm [0=AES 1=TwoFish 2=ChaCha]) is 0 for all loaded hashes
Will run 8 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
REDACTED        (dataset)     
1g 0:00:00:06 DONE (2023-04-07 22:41) 0.1485g/s 133.1p/s 133.1c/s 133.1C/s chichi..ilovegod
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

Now we can open the database and we will find the password for the user sysadmin

We now have access to the scripts directory

This is the script.php file:
