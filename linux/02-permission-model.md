# Linux Users, Groups & Permissions

## Linux Permission Model

```text
Linux primarily controls access using:

User / Owner
Group
Others

For example:
ls -l file.txt

Output:
-rwxr-xr--

Breakdown:
- | rwx | r-x | r--
  |     |     |
  |     |     └── Others
  |     └──────── Group
  └────────────── Owner

Permission meanings:
r = Read
w = Write
x = Execute
- = Permission not granted

```

## Check User Information

Shows the current username.

```bash
whoami
```

Example:

```text
ubuntu
```

Shows UID, GID and group membership.

```bash
id
```

Example:

```text
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),27(sudo)
```

Check another user's information.

```bash
id deploy
```

Show the groups of the current user.

```bash
groups
```

Shows currently logged-in users

```bash
who
```

Shows logged-in users plus what they are doing.

```bash
w
```

Shows login history.

```bash
last
```

## User Management

Create a User

```bash
sudo useradd -m username
-m creates the user's home directory.
```

Set Password

```bash
sudo passwd deploy
```

Add User to a Group

```bash
sudo usermod -aG group username
```

Important:

```text
-a → append
-G → supplementary groups
```

Remove User from a Group

```bash
sudo gpasswd -d username groupname
```

Delete user and home directory:

```bash
sudo userdel -r deploy
```

## Group Management

Create Group

```bash
sudo groupadd developers
```

Delete Group

```bash
sudo groupdel developers
```

Check Group

```bash
getent group developers
```

Add User to Group

```bash
sudo usermod -aG developers ismail
```

Remove User to Group

```bash
sudo gpasswd -d ismail developers
```

## Understanding ls -l

Run:

```bash
ls -l
```

Example:

```text
-rwxr-xr-- 1 ismail developers 1234 Sep 13 script.sh
```

Breakdown:

```bash
-rwxr-xr--
│  │ │ │
│  │ │ └── Others permissions
│  │ └──── Group permissions
│  └────── Owner permissions
└───────── File type
```

## Numeric / Octal Permissions

This is extremely important.

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
rwx = 4 + 2 + 1 = 7
rw- = 4 + 2     = 6
r-x = 4     + 1 = 5
r-- = 4         = 4
-wx =     2 + 1 = 3
-w- =     2     = 2
--x =         1 = 1
--- =           = 0
```

Permission Table

```text
| Numeric | Symbolic | Meaning                |
| ------  | -------- | -----------------------|
|       7 |   rwx    | Read + Write + Execute |
|       6 |   rw-    | Read + Write           |
|       5 |   r-x    | Read + Execute         |
|       4 |   r--    | Read                   |
|       3 |   -wx    | Write + Execute        |
|       2 |   -w-    | Write                  |
|       1 |   --x    | Execute                |
|       0 |   ---    | No permission          |

```

The Most Important Concept

```text
| Binary | Permission | Calculation | Decimal |
| ------ | ---------- | ----------- | ------  |
|   111  |   rwx      | 4 + 2 + 1   |     7   |
|   110  |   rw-      | 4 + 2 + 0   |     6   |
|   101  |   r-x      | 4 + 0 + 1   |     5   |
|   100  |   r--      | 4 + 0 + 0   |     4   |
|   011  |   -wx      | 0 + 2 + 1   |     3   |
|   010  |   -w-      | 0 + 2 + 0   |     2   |
|   001  |   --x      | 0 + 0 + 1   |     1   |
|   000  |   ---      | 0 + 0 + 0   |     0   |
```

## Three-Digit Numeric Permissions

Example:

```bash
chmod 755 script.sh
```

Breakdown:

```text
7 → Owner
5 → Group
5 → Others
```

Therefore:

```bash
755
│││
││└── Others = r-x
│└─── Group  = r-x
└──── Owner  = rwx
```

### Numeric Method

```bash
chmod 644 file.txt
```

### Symbolic Method

```bash
chmod u+x script.sh
```

Where:

```text
u = user/owner
g = group
o = others
a = all
```

### Add Group Write Permission

```bash
chmod g+w file.txt
```

### Remove Others Write Permission

```bash
chmod o-w file.txt
```

### Give Everyone Read Permission

```bash
chmod a+r file.txt
```

### Remove Everyone Execute Permission

```bash
chmod a-x file.sh
```

## Recursive Permissions

This changes permissions for the entire directory tree.

```bash
chmod -R 755 /var/www/myapp
Note: -R means recursive.
```

## Changes ownership

```bash
sudo chown ismail file.txt
```

## Change User and Group

```bash
sudo chown ismail:developers file.txt
```

## Recursive Ownership

```bash
sudo chown -R ismail:developers /var/www/myapp
```

## Changes only the group ownership.

```bash
sudo chgrp -R developers /var/www/myapp
```

## ACL (Access Controll List)

### Set ACL for a User

Give user read permission:

```bash
setfacl -m u:rahim:r file.txt
```

Give user read + write permission:

```bash
setfacl -m u:rahim:rw file.txt
```

Give user full permission:

```bash
setfacl -m u:rahim:rwx file.txt
```

### Set ACL for a Group

This gives the developers group:

```bash
setfacl -m g:developers:rwx project/
```

### Remove ACL

Remove a specific user's ACL:

```bash
setfacl -x u:rahim file.txt
```

Remove group ACL:

```bash
setfacl -x g:developers file.txt
```

### Remove All ACL Entries

```bash
setfacl -b file.txt
Note: -b removes extended ACL entries.
```

### Recursive ACL

```bash
setfacl -R -m u:rahim:rwx project/
```

### Default ACL

Set default ACL: You want newly created files/directories to inherit permissions.

```bash
setfacl -d -m g:developers:rwx /var/www/project
```

Check:

```bash
getfacl /var/www/project
```

## Permission Troubleshooting

It shows permissions for each directory in the path.

```bash
namei -l /var/www/myapp/storage/logs
```
