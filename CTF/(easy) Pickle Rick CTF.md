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
   nmap -sC -sV -o PickleRickCTF -A <MACHINE_IP>
### Check Available Services

After running the scan, you should see a web service running on ports like 80 or 8080. Open your browser and visit the IP address of the machine:

  ```bash
  http://<MACHINE_IP>
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
If you don’t find any relevant information directly on the page, you can use Gobuster to scan for hidden directories and files. This will help you discover paths that might lead to important files.




