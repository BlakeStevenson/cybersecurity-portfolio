# **File Permissions in Linux**

## **Project description**
In this project, I acted as a security professional reviewing file and directory permissions for a research team. My goal was to ensure that users were authorized appropriately and that no unauthorized write or execute permissions were present. Using Linux commands, I inspected existing permissions, analyzed the permission strings, and updated them to meet the organization's security requirements. This ensured that only the correct users and groups had access to sensitive project files.

---

## **Check file and directory details**

To check file and directory permissions, I used the `ls` command with the `-l` and `-a` options.  
This displays details such as the permission string, owner, group, file size, and includes hidden files.

**Command used**:
```
ls -la /home/researcher2/projects
```


**Current permissions represented as 10-character strings**:

| File / Directory      | Permissions |
|----------------------|-------------|
| project_k.txt        | `-rw-rw-rw-` |
| project_m.txt        | `-rw-r--r--` |
| project_r.txt        | `-rw-rw-r--` |
| project_t.txt        | `-rw-rw-r--` |
| .project_x.txt       | `-rw-w----` |
| drafts/              | `drwx--x---` |

---

## **Describe the permissions string**

**Example:** `-rw-rw-r--`

The 10-character permission string represents the file type and the permissions for the user, group, and others.

- **Character 1**: File type  
  - `-` = regular file  
  - `d` = directory  
- **Characters 2–4**: User permissions  
  - `rw-` = user can read and write  
- **Characters 5–7**: Group permissions  
  - `rw-` = group can read and write  
- **Characters 8–10**: Other permissions  
  - `r--` = others can only read  

So `-rw-rw-r--` means:  
A regular file where the user and group can read/write, and others can only read.

---

## **Change file permissions**

The organization does **not allow "others" to have write permissions**.  
The file **project_k.txt** currently has: `-rw-rw-rw-`


The last two characters (`rw-`) show "others" can write, which is not allowed.

### **Command used**

To remove write permission for others:
```
chmod o-w project_k.txt
```


### **Resulting permissions**
```
-rw-rw-r--
```
Others now only have read, not write, access.

---

## **Change file permissions on a hidden file**

The hidden file `.project_x.txt` currently has: `-rw-w----`

The requirement:  
- User: read + write  
- Group: read  
- Others: none  
- No one should have write permissions except user

### **Command used**
```
chmod u=rw,g=r,o= .project_x.txt
```
### **Resulting permissions**
```
-rw-r-----
```

The file is now read-only for the group, not writable.

---

## **Change directory permissions**

Only **researcher2** should access the `drafts` directory.  
Current permissions: `drwx--x---`


The group currently has execute (`x`) access, meaning they can enter the directory.  
We must remove that so only the user can read/write/execute.

### **Command used**
```
chmod 700 drafts
```

### **Resulting permissions**
```
drwx------
```


Only the user now has full access.

---

## **Summary**
In this activity, I inspected file and directory permissions in a research team’s project directory and verified whether the access levels matched organizational security requirements. I used `ls -la` to view permission details, explained how Linux permission strings work, and identified files that allowed unauthorized write access. I then applied `chmod` to correct file permissions, secure a hidden file, and restrict directory access. These changes ensure the system remains secure and only authorized users can access sensitive research materials.


