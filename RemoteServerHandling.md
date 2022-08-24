# Linux Server Handling

&nbsp;

### 1. How to check machine configuration?

- #### Step 1: Information about OS
  ```console
  user@machine:~$ uname -a              # All informatics about OS
  # Output: Linux rafsanjani 4.15.0-65-generic #74~16.04.1-Ubuntu SMP Wed Sep 18 09:51:44 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
  
  user@machine:~$ uname -r              # Kernel Release      --> 4.15.0-65-generic
  user@machine:~$ uname -v              # Kernel Version      --> #74~16.04.1-Ubuntu
  user@machine:~$ arch                  # Kernel Architecture --> x86_64 (64 bits)
  user@machine:~$ lsb_release -a        # Distributor ID: Ubuntu, Description: Ubuntu 18.04.3 LTS, Release: 18.04, Codename: bionic
  user@machine:~$ cat /etc/os-release   # Another way!
  ```

- #### Step 2: Processor Information:
  ```console
  user@machine:~$ lscpu | grep 'Model name'              # Output: Intel(R) Core(TM) i7-7700 CPU @ 3.60GHz
  user@machine:~$ cat /proc/cpuinfo | grep 'model name'  # Output: Intel(R) Core(TM) i7-7700 CPU @ 3.60GHz
  user@machine:~$ lscpu                                  # Output: Overall CPU information, including cores, threads, sockets, and so forth.
  ```

- #### Step 3: RAM Status
  ```console
  user@machine:~$ free -h                        # RAM capacity
  user@machine:~$ sudo dmidecode --type 17       # RAM information
  user@machine:~$ nproc                          # RAM Core
  ```

- #### Step 4: HDD (Hard Disk Drive) Status

  - ##### Step 4.1: Working Drive (Dual Boot Mode OS)
    ```console
    user@machine:~$ df -h                            # Show disk usage

    user@machine:~$ du -h --max-depth=1 /home/user   # Show the directory space usage for the particular location.
    user@machine:~$ du -h -s /home/user              # -s, is for the summarizing the given location size.
    ```

  - ##### Step 4.2: Whole HDD Information (Identifying the Partition Type)
    ```console
    user@machine:~$ sudo fdisk -l
    ```

&nbsp;

### 2. Ubuntu Installation for Deep Learning 
- #### Seep 1: GPU Setup [ [by clicking here!](https://github.com/mrzResearchArena/Linux-Documentation/blob/master/installGPU.md) ]
  - Reference: Lambda Lab [ [by clicking here!](https://lambdalabs.com/lambda-stack-deep-learning-software) ]

&nbsp;

### 3. How to check GPU configuration?

- #### Step 1: Ensure GPU Existence
  ```console
  user@machine:~$ nvidia-smi
  ```
  | GPU Utilization (No) | GPU Utilization (Full) |
  |---|----| 
  | <img src="https://github.com/mrzResearchArena/Linux-Documentation/blob/master/nvidia-smi.png" width="500" height="325"/> |  <img src="https://github.com/mrzResearchArena/Linux-Documentation/blob/master/nvidia-smi-FULL.png" width="500" height="325"/> | 

  ***Note:*** [What is the difference between Type-C and Type-G process?](https://stackoverflow.com/questions/54750627/what-do-g-and-c-types-mean-in-nvidia-smi)

- #### Step 2: Ensure CUDA Existence
  ```console
  user@mrz:~$ nvcc --version
  ```
- #### Step 3: Ensure by run a simple programme (PyTorch/Tensorflow):
  - [PyTorch](https://github.com/mrzResearchArena/Linux/blob/master/check-PyTorch-GPU-existance.py)
  - [Tensorflow-2.x](https://github.com/mrzResearchArena/Linux/blob/master/check-TF-GPU-existance.py)

- #### Step 4: GPU Memory Allocation:
  - [Allocate GPU Memory](https://github.com/mrzResearchArena/Linux/blob/master/allocateGPU.py)

&nbsp;

### 4. How does the screen work?

- #### Step 1: Current Status of the Running Socket(s)
  ```console
  user@machine:~$ screen -list   # screen -ls
  ```

- #### Step 2: Generate a Socket
  ```console
  user@machine:~$ screen -S anySocketName
  ```

- #### Step 3: Detach Screen without Killing the Socket
  ```console
  user@machine:~$ control + A + D        # The shortcut for the logout.
  ```

- #### Step 4: Resume/Re-attach the Socket after Detach
  ```console
  user@machine:~$ screen -r anySocketName
  ```

- #### Step 5: Kill a Socket
  ```console
  user@machine:~$ screen -S anySocketName -X quit
  ```

- #### Step 6: Remove Dead Screen
  ```console
  user@machine:~$ screen -wipe
  ```

- #### Step 7: Know the Current Socket Name
  ```console
  user@machine:~$ echo $STY
  ```

- #### Step 8: Kill All Screen
  ```console
  user@machine:~$ killall screen 
  user@machine:~$ pkill screen     # Alternative way
  ```


&nbsp;

### 5.1. How to copy a file/directory from local machine to remote machine? (Use Local Terminal)

```console
user@machine:~$ scp  <source>  <destination>
```
***Note:*** `150.78.20.89` and `learning` are the IP address and user name of remote machine respectively.

- #### Step 1: Copy a file 
  ```console
  user@machine:~$ scp /home/rafsanjani/anyFile.csv learning@150.78.20.89:/home/learning/mrzResearchArena
  ```

- #### Step 2: Copy a directory
  ```console
  user@machine:~$ scp -r /home/rafsanjani/anyDirectory learning@150.78.20.89:/home/learning/mrzResearchArena
  ```
- #### Step 3: How to copy all files to HDD?
  ```console
  user@machine:~$ cp -rf /home/user/ /media/user/BACKUP
  ```
  
&nbsp;

### 5.2. How to copy a file/directory from remote machine to local machine? (Use Local Terminal)

```console
user@machine:~$ scp  <source>  <destination>
```
***Note:*** `150.78.20.89` and `learning` are the IP address and user name of remote machine respectively.

- #### Step 1: Copy a file 
  ```console
  user@machine:~$ scp learning@150.78.20.89:/home/learning/ACP-SaveModel.zip /home/rafsanjani/Desktop
  ```
  
- #### Step 2: Copy a directory
  ```console
  user@machine:~$ scp -r learning@150.78.20.89:/home/learning/ACP-SaveModel /home/rafsanjani/Desktop
  ```
  
&nbsp;

### 6. How to access jupyter notebook remotely?

- #### Step 1: Run on a remote machine ####
  ```console
  learning@150.78.20.89:~$ jupyter-notebook --no-browser --port=8889 
  ```
  ***Note:*** By running, you will recieve a token from remote machine (or, server). 

  Exmaple: http://localhost:8889/?token=05f8832e3a103c9cab5f89b28e8c6e24b74ce61e2fc8ddbz

&nbsp;

- #### Step 2: Run on a local machine ####
  ```console
  user@machine:~$ ssh -N -f -L localhost:8888:localhost:8889 learning@150.78.20.89
  ```
  ***Note:*** `150.78.20.89` and `learning` are the IP address and user name of remote machine respectively.

&nbsp;

- #### Step 3: Go to the local machine's web browser and type the below URL! ####
  ```console
  localhost:8888/tree
  ```

- #### Step 4: Graphical Interface ####

&nbsp;

<!-- ![Jupyter Remotely](https://github.com/mrzResearchArena/Linux-Documentation/blob/master/jupyternotebook.png) -->

  <p align="center">
    <img src="https://github.com/mrzResearchArena/Linux-Documentation/blob/master/jupyternotebook.png" width="550" height="550"/>
  </p>



  ***Figure:*** A simple three-step process for running a remote Jupyter notebook.

  ##### Learning Resource-1 [ [by clicking here!](https://ljvmiranda921.github.io/notebook/2018/01/31/running-a-jupyter-notebook/) ]
  ##### Learning Resource-2 [ [by clicking here!](https://amber-md.github.io/pytraj/latest/tutorials/remote_jupyter_notebook/) ]

&nbsp;

### 7. Keep Remote SSH Alive / Increase SSH Connection Timeout / Prevent Remote SSH Disconnect:

- #### Step 1: Configure
  ```console
  user@machine:~$ sudo vi /etc/ssh/sshd_config
  ```

- #### Step 2: Set the Value
  ```
  ClientAliveInterval  21600   # 6h --> (3600 x 6) seconds.
  ```

- #### Step 3: Reload the SSH
  ```console
  user@machine:~$ sudo systemctl reload sshd
  ```

- **References:** https://www.tecmint.com/increase-ssh-connection-timeout/
