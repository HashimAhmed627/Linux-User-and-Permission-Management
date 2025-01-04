<p align="center">
  <img src="https://github.com/user-attachments/assets/b10f0f0b-8c11-448c-874c-b87b934270f4" alt="Description" width="300">
</p>

# Linux User and Permission Management

## Overview
This project demonstrates essential tasks for managing users, groups, and file permissions in a Linux environment. It includes practical examples and explanations for each command to help understand their functionality.

## Objective
~

## Tasks Covered
1. Add and Remove Users and Groups
2. Change Ownership of Files
3. Modify File Permissions Using Symbolic and Numeric Mode

# 

### Adding & Removing Users 

![Adding User in Linux1](https://github.com/user-attachments/assets/c91b7536-6193-4d5d-aeb9-05c6c675a3ef)

To add a user in Linux, you simply run the command `sudo useradd 'username'`

- `sudo` allows a user to temporarily perform tasks as the root, and since adding a user requires administrative privileges, this command is necessary 
- `useradd` adds new user account
- `'username'` this would be the desired name of the new user (e.g. USER1, GUEST1, etc)
  
** *To add multiple users simultaneously, we can use the logical operator `&&` (e.g. `sudo useradd USER10 && sudo useradd USER11`)* **

After we've added our new user, we can use the command `cat /etc/passwd` to view a list of all user accounts and verify the user has been added successfully 

- `cat` is used to display contents of a file
- `/etc/passwd` is a Linux system file that has key information about all user accounts on the system
    
![Setting a Password for User1](https://github.com/user-attachments/assets/879b30da-19ff-4aca-ac20-80cd1c788d3f)

- To create a password for the new user, we can use the command `sudo passwd 'username'`

![Deleting User1](https://github.com/user-attachments/assets/3cf0fe3c-c817-4ff7-902a-afc8250bed66)

To remove a user, you can use the command `sudo userdel 'username'`

- again `sudo` is necessary to perform this task because it requires root permissions
- `userdel` removes/deletes the user account
- `'username'` is the name of the user account that is going to be removed (*in the screenshot above 'USER1' is being removed*)

`cut -d: -f1 /etc/passwd` can be used to print a simple list of users without displaying all the other information associated with the user accounts 



### Adding and Removing Groups

![Adding Group1](https://github.com/user-attachments/assets/a3007f35-d683-484c-9923-d9685aa9c59c)

To add a group, you can use the command `sudo groupadd 'groupname'`
- `groupadd` creates a new user group
- `'groupname'` would be the desired name of the new user group
- After adding the new group, we can use the command `cat /etc/group` to display a list of all user groups on the system



![Deleting a Group1](https://github.com/user-attachments/assets/b4e639b8-7ca5-4892-b2fe-0a642f6379e3)

To remove a group, we can simply use the command `sudo groupdel 'groupname'`
- `groupdel` removes a user group

`cat /etc/group | tail -n 10` I used this command to display the last 10 lines of the groups list 
- `|` This is a pipe operator. It takes the output of the command on the left side of the pipe and passes it as input for the command on the right.
- `tail` is used to display the last few lines of a file or output
- `-n 10` is an option that tells the `tail` command to display only the last 10 lines


### Assigning Users to a Group

![Adding Users to Group1](https://github.com/user-attachments/assets/1fbee3ed-3f27-4db9-9a43-4b22015a397e)

To add users to a specific group we can use this command `sudo usermod -aG 'groupname' 'username' && sudo usermod -aG 'groupname' 'username'`
- `usermod` is used to modify a user account's settings
- `-aG` is used to add users to one or more groups without removing them from any other groups they may already be apart of

I used `grep GROUP1 /etc/group` to search for the string *GROUP1* in the `/etc/group` file
- `grep` is used to search for specific patterns or key words in a file

In the screenshot above, we can see that users *USER4* and *USER5* have been successfully added to *GROUP1*
