<p align="center">
  <img src="https://github.com/user-attachments/assets/b10f0f0b-8c11-448c-874c-b87b934270f4" alt="Description" width="300">
</p>

# Linux User and Permission Management

## Overview
This project focuses on core Linux system administration tasks, including user and group management, file permissions, and file ownership. It provides a step-by-step guide to adding and removing users, assigning users to groups, modifying file permissions in both symbolic and numeric modes, and changing file ownership. Each command is accompanied by a detailed explanation to clarify its function and purpose, making it a valuable resource for beginners and a practical reference for experienced users.

## Tasks Covered
1. Add and Remove Users and Groups
2. Change Ownership of Files
3. Modify File Permissions Using Symbolic and Numeric Mode

#

### Adding a User 

![Adding User in Linux1](https://github.com/user-attachments/assets/c91b7536-6193-4d5d-aeb9-05c6c675a3ef)

`sudo useradd 'username'`: This command allows you to add a user account in Linux

- `sudo`: This command allows you to temporarily perform tasks as the root, and since adding a user requires administrative privileges, this command is necessary 
- `useradd`: adds a new user account
- `'username'`: This would be the desired name of the new user (e.g. USER1, GUEST1, etc)
  
** *To add multiple users simultaneously, we can use the logical operator `&&` (e.g. `sudo useradd USER10 && sudo useradd USER11`)* **

After we've added our new user, we can use the command `cat /etc/passwd` to view a list of all user accounts and verify the user has been added successfully 

- `cat`: used to display contents of a file
- `/etc/passwd`: a Linux system file that has key information about all user accounts on the system

_____________________________________________________________________________________________________________________________________________________________________________________
### Creating a Password for a User
![Setting a Password for User1](https://github.com/user-attachments/assets/879b30da-19ff-4aca-ac20-80cd1c788d3f)

`sudo passwd 'username'`: This command is used to create a password for a new user

_________________________________________________________________________________________________________________________
### Removing a User
![Deleting User1](https://github.com/user-attachments/assets/3cf0fe3c-c817-4ff7-902a-afc8250bed66)

To remove a user, you can use the command `sudo userdel 'username'`

- `sudo`: necessary again becuase this task requires root permissions
- `userdel`: removes/deletes the user account
- `'username'`: the name of the user account that is going to be removed (*in the screenshot above 'USER1' is being removed*)

`cut -d: -f1 /etc/passwd` can be used to print a simple list of users without displaying all the other information associated with the user accounts 


_____________________________________________________________________________________________________________________________
### Adding a Group
![Adding Group1](https://github.com/user-attachments/assets/a3007f35-d683-484c-9923-d9685aa9c59c)

`sudo groupadd 'groupname'`: This command adds a new group 
- `groupadd`: creates a new user group
- `'groupname'`: would be the desired name of the new user group
- `cat /etc/group`: This command is used to display a list of all user groups on the system, which helps verify that the new group has been added successfully

__________________________________________________________________________________________________________________
### Removing a Group
![Deleting a Group1](https://github.com/user-attachments/assets/b4e639b8-7ca5-4892-b2fe-0a642f6379e3)

`sudo groupdel 'groupname'`: This command removes a group from the system
- `groupdel`: removes a user group
- `cat /etc/group | tail -n 10` I used this command to display the last 10 lines of the groups list 
- `|` This is a pipe operator. It takes the output of the command on the left side of the pipe and passes it as input for the command on the right.
- `tail`: used to display the last few lines of a file or output
- `-n 10`: an option that tells the `tail` command to display only the last 10 lines

__________________________________________________________________________________________________________________
### Assigning Users to a Group

![Adding Users to Group1](https://github.com/user-attachments/assets/1fbee3ed-3f27-4db9-9a43-4b22015a397e)

`sudo usermod -aG 'groupname' 'username' && sudo usermod -aG 'groupname' 'username'`: This coommand assigns users to a specific group
- `usermod`: used to modify a user account's settings
- `-aG`: used to add users to one or more groups without removing them from any other groups they may already be apart of

`grep GROUP1 /etc/group`: I used this command to search for the string *GROUP1* in the `/etc/group` file
- `grep` is used to search for specific patterns or key words in a file

In the screenshot above, we can see that users *USER4* and *USER5* have been successfully added to *GROUP1*

_______________________________________________________________________________________________________________________
### File Permissions (Symbolic Mode)
![File Permissions Symbolic Mode1](https://github.com/user-attachments/assets/22869c28-b5cb-4730-b7c6-3b6323775881)

Before changing any file permissions, I used the `ls -l` command to display a detailed list of all the files in the *sample_dir* directory 
- `ls`: lists the files and directories in a directory
- `-l`: an option that stands for "long format" and provides detailed information about each file or directory

After listing all files in the directory, we can see that all files have the same permissions which is the read permissions for the user, group, and others

`sudo chmod u+rwx,g+x,o+x,o-r file1`: I used this command to change the file permissions for *file1* in symbolic mode
- `chmod`: used to change the permissions of a file or directory
- `u+rwx`: This adds read(`r`), write(`w`), and execute(`x`) permissions for the **user** (*the owner of the file*)
- `g+x`: adds execute(`x`) permissions for the group associated with the file
- `o+x`: adds execute(`x`) permissions for others (*everyone else*)
- `o-r`: removes read(`r`) permissions for others
- `file1`: This is the file I'm changing permissions for

After running the command, the user now has read, write, and execute permissions. The associated group and everyone else only have execute permissions

________________________________________________________________________________________________________________________
### File Permissions (Numeric Mode)
![File Permissions Numeric Mode1](https://github.com/user-attachments/assets/5d22867e-5769-4982-b292-4eea62878000)

`sudo chmod 751 file3`: I used this command to change the file permissions of *file3* in numeric (octal) mode

Understanding the Octal Permissions (`751`)

Octal permissions are represented by three digits. Each digit corresponds to a set of permissions for the user, group, and others.

** *(4) = read permissions,     (2) = write permissions,     (1) = execute permissions* **
- First digit (7): User permissions
    - 7 = 4(read) + 2(write) + 1(execute) = rwx
    - The user has read, write, and execute permissions
- Second digit (5): Group permissions
    - 5 = 4(read) + 1(execute) = r-x
    - The group has read and execute permissions (but not write)
- Third digit (1): Others' permissions
    - 1 = 1(execute) = --x
    - Others have only execute permissions (no read or write)

After running the command, the permissions for *file3* are as follows: read, write, and execute permissions for the user, read and execute permissions for the group, and only execute permissions for others
_________________________________________________________________________________________________________________________
### Changing File Ownership
![Changing File Ownership to Diff User1](https://github.com/user-attachments/assets/79b5d23d-c859-45ad-97c3-7669586d0d82)

`sudo chown USER2:GROUP1 file2`: I used this command to change the ownership of *file2* from *cyberhashim* to *USER2* in *GROUP1*
- `chown`: stands for "change owner" and is used to change the owner and/or group of a file or directory
- `USER2:GROUP1`: This specifies the new owner and group

After running the command, the ownership of *file2* was successfully changed from *cyberhashim* to *USER2*

###

## Important Lessons
- **User and Group Management:** Commands like useradd, groupadd, and usermod allow efficient creation and modification of users and groups, ensuring proper access control.

- **File Permissions:** Linux offers symbolic and numeric modes for file permissions, allowing precise control over who can read, write, or execute files.

- **File Ownership:** The chown command is used to change ownership of files, crucial for controlling access and maintaining system security.

- **Use of sudo:** sudo enables users to perform administrative tasks with root privileges, ensuring secure system management.

- **File System Insights:** Commands like cat /etc/passwd and cat /etc/group help you review user and group information, essential for system administration tasks.
