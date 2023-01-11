## Base commands

---

- `ls`: Lists the files and directories in a directory.
  example: `ls -l`: Lists the files and directories in a directory in a long format showing permissions, ownership and timestamps
- `cd`: Changes the current working directory.
  example: `cd /home/`: Changes the current working directory to the home directory
- `pwd`: Prints the current working directory.
  example: `pwd`: Prints the current working directory, for example /home/username
- `mkdir`: Creates a new directory.
  example: `mkdir testfolder`: Creates a new directory named testfolder
- `touch`: Creates a new file or updates the timestamp of an existing file.
  example: `touch testfile.txt`: Creates a new file named testfile.txt or updates the timestamp of an existing file with the same name
- `rm`: Removes a file or directory.
  example: `rm testfile.txt`: Removes the file named testfile.txt
- `cp`: Copies a file or directory.
  example: `cp testfile.txt testfile_copy.txt`: Copies the file testfile.txt to a new file named testfile_copy.txt
- `mv`: Moves or renames a file or directory.
  example: `mv testfile.txt testfile_renamed.txt`: Renames the file testfile.txt to testfile_renamed.txt
- `cat`: Displays the contents of a file.
  example: `cat testfile.txt`: Displays the contents of the file testfile.txt on the terminal
- `less`: Displays the contents of a file, one page at a time.
  example: `less testfile.txt`: Displays the contents of the file testfile.txt one page at a time in the terminal
- `echo`: Displays a message on the screen.
  example: `echo "Hello World"`: Displays the message "Hello World" on the screen
- `man`: Shows the manual for a command.
  example: `man ls`: Shows the manual for the command ls

## Users and Groups

---

- `useradd`: Creates a new user.
  example: `useradd newuser`: Creates a new user with the specified username newuser
- `userdel`: Deletes a user.
  example: `userdel newuser`: Deletes the user newuser
- `usermod`: Modifies a user account.
  example: `usermod -a -G developers newuser` : Add the user newuser to the developers group
- `passwd`: Changes a user's password.
  example: `passwd newuser`: Changes the password for the user newuser
- `chage`: Changes a user's password expiry information.
  example: `chage -M 90 newuser` : set the maximum number of days a password for newuser may be used
- `groupadd`: Creates a new group.
  example: `groupadd projectX`: Creates a new group named projectX
- `groupdel`: Deletes a group.
  example: `groupdel projectX`: Deletes the group projectX
- `groupmod`: Modifies a group account.
  example: `groupmod -n projectY projectX` : Rename the group from projectX to projectY
- `adduser`: Add a user to a group.
  example: `adduser newuser projectX` : Add the newuser to the projectX group
- `deluser`: Remove a user from a group.
  example: `deluser newuser projectX` : Remove the newuser from the projectX group
- `id`: Shows user and group information for a given user.
  example: `id newuser`: Shows user and group information for the newuser
- `gpasswd`: Modifies group password
  example: `gpasswd -a newuser projectX` : Add the newuser to the projectX group and enable the user to administrate the group
