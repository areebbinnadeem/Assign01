# Assign01

## Steps

## 1
Downloaded Ubuntu Version 16.04.7
## 2
Downloaded Kernel Version 4.19.275
## 3
Installed some libraries to add a new System Call to kernel. These Include:
    <ul>
    <li>sudo apt-get install gcc</li>
    <li>sudo apt-get install libncurses5-dev</li>
    <li>sudo apt-get install bison</li>
    <li>sudo apt-get install flex</li>
    <li>sudo apt install make</li>
    <li>sudo apt-get install libssl-dev</li>
    <li>sudo apt-get install libelf-dev</li>
    <li>sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main
universe"</li>
    <li>sudo apt-get update</li>
    <li>sudo apt-get upgrade</li>
    </ul>
    
## 4
Extracted the kernel file and made a folder named "hello" inside a the kernel file
![1](https://user-images.githubusercontent.com/108046345/224017232-6b470ed8-99e9-4684-ae85-7c97abdeb563.PNG)
## 5
Inside the "hello" file opened the terminal and created a 'C' file named hello to add 'C' code for the system call
![2](https://user-images.githubusercontent.com/108046345/224017694-bf6ea125-6553-4c6a-845c-da67dc60a9d8.PNG)
In the 'c' file wrote the following code
![3](https://user-images.githubusercontent.com/108046345/224017923-0a1fa3d4-a785-42b6-954c-e58969d34428.PNG)

## 6
Created a Makefile for my new folder to ensure that the code in the folder is always compiled whenever the kernel is compiled. In order to do this, I typed in my
terminal “gedit Makefile” <br>
![4](https://user-images.githubusercontent.com/108046345/224018505-e586eb87-6670-4b5d-8870-40a18e94b5b8.PNG)<br>
and put the following code:<br>
![5](https://user-images.githubusercontent.com/108046345/224018547-a98288e2-5694-416a-8f69-ab3811694529.PNG)

## 7
Adding the new code into the system table file:
It is mandatory to add the system call entry to the syscall 64.tbl file, which stores the names of all the system calls in our system, in order to establish a 64-bit system call in accordance with our system.
![6](https://user-images.githubusercontent.com/108046345/224020020-0018c326-064d-4d7c-acf5-1ead0b864e17.PNG)
![7](https://user-images.githubusercontent.com/108046345/224020048-5e464208-a355-434b-95d8-22e870996885.PNG)
![8](https://user-images.githubusercontent.com/108046345/224020077-7326a8f8-fc8f-47ab-b8b9-9ab52970b068.PNG)

## 8
Adding the prototype of the new system call into the system calls header file:
The prototype is located in the kernel folder<br>
![9](https://user-images.githubusercontent.com/108046345/224020516-9de50c8a-e0cc-4d9c-a77c-1a75fe996dc2.PNG)<br>
Added the prototype of the system call in this file<br>
![10](https://user-images.githubusercontent.com/108046345/224020702-d9f448b5-b0d7-49a6-bca8-96ed733064e0.PNG)

## 9
Changing version and adding the hello folder in the kernel’s Makefile:<br>
Added my roll number in the extraversion of the kernel’s make file and added the new module that was created into the kernel’s make file. For this, I opened
the Makefile of the kernel and search for “core-y” and went to it’s second instance and add new module which is “hello” at the end of it.<br>
![11](https://user-images.githubusercontent.com/108046345/224021971-f30b120b-c66d-4105-963e-fa9b862e62c1.PNG)
![12](https://user-images.githubusercontent.com/108046345/224022620-549893fb-8d75-4316-be8b-0b300f6e0d82.PNG)


## 10
Created a config file for my kernel<br>
![13](https://user-images.githubusercontent.com/108046345/224022734-2737b320-08e0-4b64-9b7d-afe938f3a2c5.PNG)
![14](https://user-images.githubusercontent.com/108046345/224022779-f773abde-eed4-4012-aac2-2b44b6e29851.PNG)

## 11
Cleaned all existing object and executable file because compiler sometimes links or compile files incorrectly and to avoid this, deleted all old objects and
executable files by typing “make clean -j4" (forgot to take screenshot)<br>
Next, wrote the command “make -j4” to start building the kernel (forgot to take screenshot)<br>
Here is a screenshot after the kernel was built<br>
![17](https://user-images.githubusercontent.com/108046345/224023913-2cd105fa-2898-42a7-b6ed-12798372b9e7.PNG)

## 12
Installed the kernel that was built by typing “make modules_install install” which installed the kernel and updated the grub as well.<br>
![18](https://user-images.githubusercontent.com/108046345/224024439-2a81bfad-bdff-42c6-af33-ddff7dfdec20.PNG)<br>
Now restarted the laptop to switch to the new kernel<br>
![20](https://user-images.githubusercontent.com/108046345/224024771-49444e58-d96e-4773-8135-d54e9d60da98.PNG)

## 13
After logging into the newly compiled kernel, checked the system call by making a C code named “userspace.c” and putting the following code in it:<br>

#include <stdio.h><br>
#include <linux/kernel.h><br>
#include <sys/syscall.h><br>
#include <unistd.h><br>
int main()<br>
{<br>
long int i = syscall(335);<br>
printf("System call sys_hello returned %ld\n", i);<br>
return 0;<br>
}<br>

Compiled the code and executed it. It returned 0 which meant that the code compilation was successful.<br>
![21](https://user-images.githubusercontent.com/108046345/224025939-6134a69e-bea2-485c-a8cc-48dd9f022c26.PNG)<br>

Run the command "dmesg" and found "Hello World" written at the end of it.<br>
![22](https://user-images.githubusercontent.com/108046345/224025992-819ef1f0-384f-4a92-9ea1-02275e7ad415.PNG)<br>

