# Permissions

<img width="954" height="613" alt="image" src="https://github.com/user-attachments/assets/9faceb87-dedb-4d56-87e6-953fc88b1d98" />


## Objective
The objective of this challenge is to read a file located in the **root directory**, despite not having direct permission to access it.

## Description
The challenge asks whether it is possible to read files located in the root directory.  
After launching the instance, the user is placed in a restricted shell environment without direct read access to `/root`.

The key to solving the challenge lies in identifying available privileges that can be abused to bypass file permission restrictions.

## Methodology
First, the contents of the home directory are listed to understand the current environment and permissions:
This shows standard user files such as .bashrc, .profile, and .flag.txt, but no direct access to the root directory.

Next, the sudo -l command is executed to check which commands the current user is allowed to run with elevated privileges:


The output reveals that the user can run /usr/bin/vi as root without a password.

<img width="567" height="281" alt="image" src="https://github.com/user-attachments/assets/7b7a4321-1cf5-4a95-ad02-0797db1a3e36" />




Since vi is a powerful text editor capable of opening arbitrary files, it can be abused to read files owned by root.

Using this privilege, vi is executed with root permissions and pointed directly at the /root directory:
<img width="567" height="93" alt="image" src="https://github.com/user-attachments/assets/d59063a2-6fe0-44c5-b1cc-47d9e7992af5" />




This opens a directory listing inside vi, showing the contents of the /root directory.
Among the files present is the flag file.

<img width="567" height="294" alt="image" src="https://github.com/user-attachments/assets/22fcfc2f-a677-4319-bdb8-9cf3ea717a67" />


The flag file is then opened directly from within vi, revealing the flag contents.

<img width="567" height="149" alt="image" src="https://github.com/user-attachments/assets/bc3d2f25-0c96-451e-9b1b-a0287b3f7d18" />


## Flag 
picoCTF{using_vim_3dit0r_ad091ce1}

