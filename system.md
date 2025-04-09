# System Control

&nbsp;

### 1. Check Internet Speed
```console
user@machine:~$ speedtest-cli    # Install: pip install speedtest-cli
```

&nbsp;

### 2. How to reduce terminal text? / Customizing BASH Prompt Text
```console
user@machine:~$ PS1='[\u@\h \W]\$ '                       # Small
user@machine:~$ PS1='[@ \W]\$ '                           # Extra Small
```

&nbsp;

### 3. Find the MAC Address
```console
user@machine:~$ ifconfig | grep 'HWaddr' 

# Go to router icon --> Connection Information --> General
```

&nbsp;

### 4. Fixed the Compiz Configure Issue
```console
user@machine:~$ dconf reset -f /org/compiz
user@machine:~$ setsid unity  # (If doesn't work: sudo apt install unity.)
user@machine:~$ unity --reset-icons
```

&nbsp;

### 5. TTY Mode:
###### We can use shortcut key: control → alter → F7    # Try F2, F3, ..., F6 (i.e., F2 through F6).
This shoud bring up a text-based login prompt (F2 through F6). Afterward, log in with your username (`whoami`) and password. Keep in mind, F1 is reserved for GUI.

###### We could use terminal or console, if we access via GUI mode.
```console
user@machine:~$ sudo chvt 7                            # Try 1, 2, 3, ... 7
```

&nbsp;

### 6. Create a New User and Remove the Root Privilege
```console
user@machine:~$ sudo adduser anyName           ### Add a New User
user@machine:~$ sudo usermod -aG sudo anyName  ### Add the Root Privilege
user@machine:~$ sudo gpasswd -d anyName sudo   ### Remove the Root Privilege
```

- #### References:
  > 1. Create a SUDO User ([web](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart))
  > 2. Remove the Root Privilege-1 ([web](https://askubuntu.com/questions/335987/remove-sudo-privileges-from-a-user-without-deleting-the-user))
  > 3. Remove the Root Privilege-2 ([web](https://www.liquidweb.com/kb/remove-delete-user-ubuntu-16-04/))
  > 4. Create User and Remove the Root Privilege ([web](https://www.ostechnix.com/how-to-grant-and-remove-sudo-privileges-to-users-on-ubuntu/))
  > 5. Restore the Root Privilege ([web](https://www.ostechnix.com/how-to-restore-sudo-privileges-to-a-user/))

&nbsp;

### 8. Program Killing Procedure:
- #### Step 1: Show the all running program
  ```console
  user@machine:~$ top                     # dynamic
  user@machine:~$ ps aux                  # static
  user@machine:~$ ps aux | grep '<PID>'   # Find a particular process with details
  ```

- #### Step 2: Kill program(s)
  ```console
  user@machine:~$ kill 3288             # Kill a particular program
  # Example: Here, 3288 is the process identity (PID), Then the program (3288) will halt.

  user@machine:~$ kill -9 3288          # Kill a particular program forcefully. It is especially helpful for the GPU system.
  user@machine:~$ kill -9 -1            # Kill all the program
  ```
  
&nbsp;

### 9. Boot a Pendrive for the Linux-based OS:
- #### Step 1: Findout the Pendrive
  ```console
  user@machine:~$ ls /dev/sd    # Press the Tab (NOT the Enter)
  ```
  | No Pendrive | Pendrive Exist |
  |---|----| 
  | <img src="https://github.com/mrzResearchArena/Linux/blob/master/sdx-1.png" width="450" height="150"/> |  <img src="https://github.com/mrzResearchArena/Linux/blob/master/sdx-2.png" width="450" height="150"/> | 

  
- #### Step 2: Boot the Pendrive
  ```console
  user@machine:~$ sudo dd if=anyName.iso of=/dev/sdx bs=4M status=progress && sync   # x = {b, c, d, ...}
  ```

&nbsp;

### 10. Wi-Fi Reboot for Linux
```console
nmcli radio wifi off
echo 'Wi-Fi is turned off. Internet will appear within 15 seconds if everything goes smoothly.'
sleep 10 # Pause for 10 seconds
nmcli radio wifi on
echo 'Wi-Fi will turn on after a few seconds.'
```

### 11. Battery Timing
https://askubuntu.com/questions/69556/how-do-i-check-the-batterys-status-via-the-terminal
