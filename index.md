
## Applying John in our daily life
----------------------------------

> ### Installing John...

* First of all, we need to install 'john-the-ripper' using snap
```
sudo snap install john-the-ripper -y
```

_NOTE: john is included in snap version of john-the-ripper, & tested in Ubuntu 20.04_

* Alternatively, we can install it via _[github](https://github.com/openwall/john.git)_ and then follow the instructions explained in _[Openwall](https://www.openwall.com/john/doc/INSTALL.shtml)_

> ### How to Crack a Linux Password ?

* In Linux, there are two important files saved in the /etc directory: passwd and shadow
```bash
/etc/passwd -> stores information like username, user id, login shell, etc.
/etc/shadow -> contains password hash, password expiry, etc.
```

* In addition to the 'john' command, John comes with a few other utilities. One of them is called 'unshadow'

* The unshadow command combines the passwd and shadow files together into a single file. This can then be used by John to crack passwords

* Here's how we can use the unshadow command
```
unshadow /etc/passwd /etc/shadow > output.db
```

This command will combine the files together and create an output.db file. We can now crack the output.db file using John
```
john output.db
```

* John tries to find the password for all the users in the passwd file and generates the output with the list of cracked passwords
* Again, you can use custom wordlists via the --wordlist flag

> ### How to Crack a Windows Password ?

* In Windows, the password hashes are stored in the SAM database. SAM uses the LM/NTLM hash format for passwords, so we will be using John to crack one

* Getting passwords from the SAM database is out of scope for this article, but let's assume you have acquired a password hash for a Windows user

* Here's the command to crack it:
```
john --format=lm crack.txt
```

* The crack.txt will contain the password hash
* If John is unable to crack the password using its default wordlist, you can use the RockYou wordlist using the --wordlist flag

> ### How to Crack a Zip File Password in Linux ?

* Let's try to crack a zip file password. To do that, we need to get the hash of the zip file's password

* Like unshadow, John has another utility called 'zip2john' 
* zip2john helps us to get the hash from zip file. If you are cracking a .rar file, you can use the rar2john utility

* Here's the syntax to get the password hash of a zip file
```
john-the-ripper.zip2john test.zip > zip.hash
```

* The above command will get the hash from the zip file and store it in the 'zip.hash' file. You can then use John to crack the hash
```
john-the-ripper.zip2john zip.hash
```

* To decrypt the hash
```
john-the-ripper zip.hash
```

* John also has several other functionalities that will help you crack a variety of passwords

> ### How to Open Encrypted Zip Files Without Password in windows ?

* By Using command prompt, you can access all the files available in password-protected ZIP file without entering any passcode 

* When trying this method, you have to use a pre-coded tool, John the Ripper

* Let's see how this tool helps you get over the line

1. Download and install John the Ripper from this _[link](https://web.archive.org/web/20190315141023/https:/www.openwall.com/john/)_ 

2. It'll be in the ZIP format. Extract it to your desired location and install it so that you can use it in cmd

3. Change the folder name to 'john' you have downloaded & Place it on the Desktop

4. Create a new folder 'crack' inside run folder of john which you just placed on Desktop

5. Copy and paste the encrypted ZIP file you want to access into the crack folder

6. Search for cmd and open the Command Prompt

7. Enter the following command in cmd
```
cd Desktop/john/run
```

8. Now, execute the following command
```
zip2john.exe crack/ZipFileName.zip>crack/key.txt
```
* This command creates hashes which helps you crack the lost password and when they are matched, You'll find password hashes in the 'key.txt' file

9. Next, execute the following command 
```
john --format=zip crack/key.txt
```
* Within few minutes, you may see your password appear on the screen. Otherwise, you may have to wait for few hours, depending on how complicated/difficult your password is


## References ~

> _[Official Documentation](https://www.openwall.com/john/)_

> _[Openwall Examples](https://www.openwall.com/john/doc/EXAMPLES.shtml)_

> _[Ubuntu Man Pages](https://manpages.ubuntu.com/manpages/focal/en/man8/john.8.html)_

> For any issues, _[Refer Here](https://superuser.com/questions/1457837/command-zip2john-is-not-working)_ or _[here](https://www.freecodecamp.org/news/crack-passwords-using-john-the-ripper-pentesting-tutorial/)_

![keanu_Reeves](imgs/johnwick.jpg)
