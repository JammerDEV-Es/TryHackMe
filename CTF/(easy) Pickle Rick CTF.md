# TryHackMe - **Pickle Rick** CTF Walkthrough

This is a detailed walkthrough of the **Pickle Rick** CTF challenge from TryHackMe. The goal of this challenge is to help Rick turn back into a human by finding three secret ingredients. This challenge is beginner-friendly and covers basic web exploitation, Linux commands, and privilege escalation.

---

# Steps to Complete the Challenge

## **Step 1: Initial Reconnaissance**

1. **Access the Machine:**
   - SSH into the machine or use the access method provided by TryHackMe.

2. **Port Scanning:**
   - The first task is to perform a **port scan** to discover open ports and services on the machine. We can use **nmap** for this:

   ```bash
   nmap -sC -sV -o PickleRickCTF -A MACHINE_IP
### Check Available Services

After running the scan, you should see a web service running on ports like 80 or 8080. Open your browser and visit the IP address of the machine:

  ```bash
  http://MACHINE_IP
  ```
You should see a page with some initial clues about the secret ingredients.

## Step 2: Explore the Web Service

### Inspect the Web Service

Inspect the page by viewing the source code. You can do this by pressing Ctrl+U or right-clicking and selecting "View Page Source". Look for comments or hidden clues that may point to the location of the ingredients.

### Directory Bruteforce (Using Gobuster)

We will right-click on the blank space of the page and select 'View Page Source.' Once we've done that, a comment will appear in green at the bottom that says
```bash
 <!--

    Note to self, remember username!

    Username: R1ckRul3s

  -->
```
![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recorteusername.png)
If you don’t find more relevant information directly on the page, you can use Gobuster, its a little bit slow to scan but it helps to find hidden directories and files. 

you will put this on the console:
```bash
gobuster dir -u http://MACHINE-IP -w /usr/share/wordlists/dirb/common.txt
```
-u its to specify the directory and -w its to put the wordlist

common.txt has 4615 words, this are the page directories: 
/.hta                 
/.htaccess            
/.htpasswd            
/assets              
/index.html           
/robots.txt           
/server-status        

![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recortegobusteer.png)

After that we're gonna put the robots.txt like this http://MACHINE-IP/robots.txt and we're gonna see a simple text on the screen that it says: Wubbalubbadubdub

This will be the password. Then put this https://MACHINE-IP/login.php and you will put the username **R1ckRul3s** and the Password **Wubbalubbadubdub**

### Step 4 (Locate First Ingredient) - First Question: What is the first ingredient that Rick needs?

After putting the username and the password, you should find the first ingredient on the in a file called `Sup3rS3cretPickl3Ingred.txt`. You can't `cat` the txt file because you're not able to do this
then you're gonna put `less` it's basically the same function.
![](https://github.com/JammerDEV-Es/TryHackMe/blob/main/CTF/Images/recortelogin.png)

### AND THE FIRST INGREDIENT WILL BE:  `mr. meeseek hair`

## Step 4: Privilege Escalation for the Second Ingredient

### Access a Protected Directory

The second ingredient is located in the directory `/home/rick/second_ingredient/`. However, this directory is protected, and you'll need privileged access to view its contents.

### Escalate Privileges

To escalate privileges, you can attempt to use `sudo` if it's allowed. Run the following command to check what commands you can run as a privileged user:



























