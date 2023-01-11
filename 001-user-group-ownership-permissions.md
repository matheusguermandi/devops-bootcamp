## Ownership and permissions

---

In Linux, every file and directory is owned by a specific user and group. The user and group ownership of a file or directory determines who has the ability to read, write, and execute the file or navigate the directory. In addition to the user and group ownership, there are also file permissions that can be set for the file or directory, which determine what actions can be taken by the owner, members of the group, and others.

In Linux, file permissions are represented by a series of letters and/or symbols that indicate the level of access that a user has to a file or directory. The permissions are divided into three categories: read (r), write (w), and execute (x).

```bash
- `r`: read permission allows a user to open and view the contents of the file
- `w`: write permission allows a user to make changes to the file or create new files in the directory
- `x`: execute permission allows a user to execute a file as a program or navigate the contents of a directory
```

These permissions can be set for three different classes of users: the owner of the file (user), members of the group that owns the file (group), and all other users (others). Each class of users has its own set of permissions for the file.

```bash
- `rwx`: read, write, and execute permissions are granted.
- `rw-`: read and write permissions are granted.
- `r-x`: read and execute permissions are granted.
- `r--`: read permission only is granted.
- `-wx`: write and execute permissions are granted.
- `-w-`: write permission only is granted.
- `--x`: execute permission only is granted.
- `---`: no permissions are granted.
```

You can check the permissions of a file using the ls -l command, it will show the permissions of the file on the left of the listing, for example:

```bash
-rwxr-xr-x 1 root root  789 Aug 12 18:00 testfile.txt
```

In this example, the first rwx indicates the owner of the file (root) has read, write and execute permissions. The next r-x indicates that members of the group (root) have read and execute permissions, and the final r-x indicates
