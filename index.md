
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

> ### How to Crack a Zip File Password in Linux?

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

### How to Open Encrypted Zip Files Without Password in windows ?
* Using the command prompt is a method you can try to make your password-protected ZIP files accessible without entering any passcode. 
* When trying this method, you have to use a pre-coded tool, John the Ripper.
* Let's see how this tool helps you get over the line.

Step 1. Download and install John the Ripper from this link. It will be in the ZIP format. Extract it to your desired location and install it so that you can use it in CMD.

Step 2. You can change the folder name you have downloaded. Place the folder on the Desktop.

Step 3. Now, open the folder you just placed on the Desktop and double-click on the “Run” folder. Inside the Run folder, create another folder and name it “Crack”.

Step 4. It is time to copy and paste the encrypted ZIP file you want to access into the Crack folder.

Step 5. Go to the search bar of your Windows or any other operating system, type cmd, and open the Command Prompt

Step 6. Type the “cd/Desktop/john/run” command on the cmd interface and press the “Enter” key from your computer. This command calls Windows to find the Run folder.

Step 7. Now, write the “Zip2john.exe/crack/ZipFileName.zip>crack/keys.txt” command on the interface and execute it. It will create hashes. These hashes help you crack the lost password when they are matched with it. You will find password hashes in the “keys.txt” file.

Step 8. Execute the “john -format=zip crack/keys.txt” command. Within a few minutes, you may see your password appear on the screen. Otherwise, you may have to wait for multiple hours, depending on how complicated or difficult your password is. Below, you can see that the cracked password is “ABC123”.


## References ~

> _[Official Documentation](https://www.openwall.com/john/doc/)_

> Follow the link to install _[John The Ripper](https://web.archive.org/web/20190315141023/https:/www.openwall.com/john/)_ in any operating system

> _[Openwall Examples](https://www.openwall.com/john/doc/EXAMPLES.shtml)_

> _[Ubuntu Man Page](https://manpages.ubuntu.com/manpages/focal/en/man8/john.8.html)_

> For any issues, _[Refer Here](https://superuser.com/questions/1457837/command-zip2john-is-not-working)_ and _[here](https://www.freecodecamp.org/news/crack-passwords-using-john-the-ripper-pentesting-tutorial/)_

![keanu_Reeves](imgs/johnwick.jpg)
