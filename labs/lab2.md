## Lab 2 (1/30/26)

## Start this lab once you have access to RON through VScode
First, well will change a couple settings in VScode to make your life easier in the long run.
Tasks:
1. Set 'ctrl+enter' key to send a line of code down to the terminal
2. Test the keybinding
3. Make a new lab notebook repository on github. 
4. Clone that repository to RON

### To set the ctrl+enter run code shortcut:
1. Open the keybindings file of VScode
- Windows: File ==> preferences ==> Keyboard shortcuts 
- Mac: Code ==> Settings ==> Keyboard shortcuts
2. Search for ```workbench.action.terminal.runSelectedText``` in the keybindings search bar
3. Press the icon on the left to open a window with this message "Press desired key combination..." and make your choice. (I suggest Ctrl+Enter)
4. Press enter to store your binding. 

### Next, test the new keybinding: 
1. hit ctrl+n to open a new document. 
2. In the new document, write ```echo "Hello! I'm coding"```
3. With your cursor next to ```echo "Hello! I'm coding"```, press 'ctrl' and then 'enter' together
Did it send ```echo "Hello! I'm coding"``` to your terminal? What did it return?

### Make repository on GitHub for your lab notebook on RON and your local computer
Now that you are connected to RON, lets make a lab notebook in your repo to be graded each week. The easiest way to do this is to first create a new repository on GitHub.com, and then clone that to your home directory on RON and your laptop.
1. Login to GitHub with the credentials you made for Lab 1
2. On your GitHub page, click 'Repositories' 
3. Click the green 'New' button
4. In 'Repository Name', type 'Bioinformatics-Notes'  **No spaces. Lets all keep the same simple name**
5. Flip the switch to 'on' for the 'Add README'
6. Click 'Create repository'

### Next, we will clone the repo on RON, and open up the folder with VScode (using the Remote SSH extension)
1. Open up vscode
2. Control + shift + 'p' to open command prompt (command + shift + p on apple)
3. Start typing 'Connect to...' and the 'Connect current window to host' menu item will pop up. Select it
4. If asked, connect to ron.sr.edu host
5. Enter your RON username if prompted
6. Enter your RON password when prompted
7. Once you are successfully connected to RON and in your home directory, clone with the 'git clone' command:
```
cd $HOME
git clone https://github.com/<YOURGITHUBUSERNAME>/Bioinformatics-Notes.git
```
You should see an indication that it downloaded to your home directory 

### Next, we will open the directory you cloned in VScode to save the workspace, then make a lab notebook document that will synchronize on RON and your machine.
1. In the VScode window that you have connected to RON, go to 'File --> Open folder'
2. The command pallet in VScode should show your 'home directories' including the 'Bioinformatics-Notes' directory. Select it.  
3. If you did this correctly, you should now see the README file pop up on the left in the list of files. Click on it to open it. 
4. While we are at it, lets save your VScode workspace in the repo directory. Click 'File --> Save Workspace As...' and click on the 'Bioinformatics-Notes' directory to save the workspace there. The workspace file just lists your VScode preferences.This way, you can load this workspace each week to pick up where you left off.   
5. In vscode terminal, go to 'file' --> 'new text file'. Save this empty file as 'yourlastname_yourfirstname.md'. Keep notes in this file as demonstrated by your instructor to get full attendance points. Add some short random text to this document to make sure that it is picked up. 


Note: Text files saved with the '.md' after it will be interpreted at 'markdown' format. We will get into this soon. 


### Use SSH keys on RON so that you dont need passwords to push your lab notebook
1. Generate an SSH key pair (if you don't have one) in your host's terminal using the command:
ssh-keygen -t ed25519 -C "jeffrey.miller@unh.edu"
- You might see:
```
Enter file in which to save the key (/home/users/YOURUSERNAME/.ssh/id_ed25519):
```
Hit enter to proceed
- If you've done this already and re-runnig it, you might see
```
/home/users/YOURUSERNAME/.ssh/id_ed25519 already exists.
Overwrite (y/n)?
```
Enter 'y' and hit return
Next, you might see
```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
Hit return for both. No passphrase is required. 
You should see:
```
Your public key has been saved in /home/users/YOURUSERNAME/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:gS9dqsZ2WtlQhQWDWKC81aoPG3OwkFp0e5kAKwzbhLA YOUREMAIL@unh.edu
The key's randomart image is:
+--[ED25519 256]--+
|+.o   .+..o+o    |
|+= + ..o. .o     |
|E.+ = o o o      |
| o o = * =       |
|  + + * S        |
| o . * o +       |
|.   * * + .      |
|     X +         |
|    . o          |
+----[SHA256]-----+
```

2. Add your public key to your GitHub account:
- Copy the content of your public key file. Print it to the screen using ```cat ~/.ssh/id_ed25519.pub```
- This should print the key to the terminal screen and look like this
```
SHA256:gS9dqsZ2WtlQhQWDWKC81aoPG3OwkFp0e5kAKwzbhLA YOUREMAIL@unh.edu
```
- Go to your GitHub account's Settings (gear top right icon of your home GitHub page) > SSH and GPG keys.
- Click New SSH key, give it a title (use Laptop to RON), paste the copied public key, and click Add SSH key.

3. Change your repository's remote URL:
- Change into your Gen711-811 repository with ```cd ~/gen711-811```
- In your repository's directory, check the current remote URL with ```git remote -v``` You should see the name of your fetch (download) and push (upload) access method. Set it to use ssh with:
```
git remote set-url origin git@github.com:YOURUSERNAME/REPOSITORY.git
```
Note: replace 'YOURUSERNAME' with your ***github username***, and 'REPOSITORY' with the name of the repository. In this case, it is 'gen711-811'. This is what my command for me would look like:
```
git remote set-url origin git@github.com:jthmiller/gen711-811.git
```
- my github username is jthmiller
- the repo name is gen711-811

4. Test the connection at RON with: ```ssh -T git@github.com```
You should see a message confirming a successful connection like this:
```
Hi jthmiller! You've successfully authenticated, but GitHub does not provide shell access.
```
Now, subsequent push and pull operations from within VS Code will use SSH authentication without prompting for credentials. 

### Do the same for your lab notebook repository. 
1. Change your current directory to the lab notebook directory with ```cd ~/YOURLABNOTEBOOKREPONAME```
2. In your repository's directory, check the current remote URL with ```git remote -v``` You should see the name of your fetch (download) and push (upload) access method. It should also show your username and repo name.
3. Set it to use ssh authentication with:
```
git remote set-url origin git@github.com:YOURUSERNAME/REPOSITORY.git
```
Note: replace 'YOURUSERNAME' with your ***github username***, and 'REPOSITORY' with the name of the repository. In this case, it is whatever you nammed your notebook repo. 

If you've done everything above correctly, new documents and changes should be tracked VScode and Git. To get your changes incorporated into your repository at GitHub, click on the github bubble fork (usually the third icon down on the left of VScode). Enter any random text you want into the 'Message' box, and then hit the commit button. This should upload your new files/changes to your GitHub repo. 

Best practice is to use different authentication keys for different machines (e.g., work laptop vs. personal laptop). If one machine is compromised, you can revoke access for that specific key without affecting others. Go through this process again if you have another computer to work from.

### Updating your copy of 'gen711-811' each week. (Will do as a class prior to lab 3)
If you forked gen711-811, the easiest method to get the updates each week is to log in to your GitHub in a browser, navigate to your copy of the 'gen711-811' repo. If there are updates to be had, you should see 'update fork' button.  This will bring the new files/changes to your GitHub repo, but not to your 'remote repo' of gen711-811 on RON. To pull the updates to your RON remote repo, open VScode, connect to RON (as above). Once you've connected to RON, go to 'File --> Open Folder'. Scroll down to and click 'gen711-811'. Click the bubble fork on the left. Near the 'Changes' meun, you should see '...'. If you click on it, you should see a 'fetch' option. Let me know if you see an error as a result. 


### Generate ssh-keys to log into RON from VScode without usernames and passwords (Will do as a class prior to lab 3)
### Do this if you'd preffer not to type your username and password each time you log into RON. 
The process is much like the process for generating ssh keys for the connection between RON and GitHub
First, open 'terminal' on your mac. We are going to use the terminal to generate the keys and restrict the permissions on the private key file. 


 <details><summary>For Mac and Linux</summary> 
Run the following shell command, replacing the path to your private key if necessary: 

```
cd ~/.ssh
ssh-keygen -t ed25519 -b 4096
chmod 400 ~/.ssh/id_ed25519
```

- Next, share the public key with the Ron server

```
ssh-copy-id USERNAME@ron.sr.unh.edu
```

If that doesn't work, we can try:

```
cat ~/.ssh/id_rsa.pub | ssh user@12.34.56.78 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys
```
<br>
</details> <!-- end for mac-->
<br>
<details><summary>For Windows</summary> 
**For Windows**, run the following command in PowerShell to grant explicit read access to your username:
```
icacls "privateKeyPath" /grant :R
```
Then navigate to the private key file in Windows Explorer, right-click and select Properties. Select the Security tab → Advanced → Disable inheritance → Remove all inherited permissions from this object.
</details> <!-- end for Windows-->

Test the connection by connecting to RON

