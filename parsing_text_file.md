# Updating an Allow List File with a Python Automation Script  

## Overview
My organization maintains a text file (`allow_list.txt`) that contains approved IP addresses for accessing restricted resources. A separate list (`remove_list`) identifies IP addresses that should no longer be allowed. To streamline updates, I created a Python algorithm that reads the file, removes outdated addresses, and rewrites the updated list back to the file.

---

## Step 1: Load the Allow List File
I began by storing the file name in a variable and opening it in read mode:

```python
import_file = "allow_list.txt"

with open(import_file, "r") as file:
    ip_addresses = file.read()
```

Opening the file using a `with` block ensures that Python manages the resource properly and closes the file automatically. Using the `"r"` mode indicates that the file will be accessed strictly for reading.

---

## Step 2: Read and Parse the File Contents
Once opened, I used `.read()` to load the file’s text:

```python
ip_addresses = ip_addresses.split()
```

The `.read()` method loads the entire file as a single string. Because IP addresses in the file were separated by whitespace, converting the string to a list using `.split()` allowed the program to treat each IP address as a separate element.

---

## Step 3: Loop Through the Removal List
Next, I iterated through every IP address contained in the `remove_list` variable:

```python
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)
```

A `for` loop allows the script to examine each address scheduled for removal. The `if` check prevents errors by ensuring `.remove()` only executes on items that actually exist in the list.

---

## Step 4: Convert the Updated List Back to a String
Before writing the revised content back to the text file, the list had to be turned into a properly formatted string. I used `"\n".join()` so each address appears on a separate line:

```python
updated_ips = "\n".join(ip_addresses)
```

`join()` combines list elements into a single string, using newline characters to preserve one-per-line formatting.

---

## Step 5: Rewrite the Allow List File
Finally, I opened the file again—this time in write mode—and replaced its previous contents:

```python
with open("allow_list.txt", "w") as file:
    file.write(updated_ips)
```

Using `"w"` mode clears the original file automatically. Calling `.write()` outputs the updated set of IP addresses so that only valid IPs remain authorized.

---

## Summary
The Python script automates the process of removing outdated IP addresses from the allow list. It:

1. Opens the `allow_list.txt` file in read mode  
2. Reads its contents into a string  
3. Converts that string into a list for easier manipulation  
4. Iterates over a separate `remove_list` and removes matching addresses  
5. Converts the cleaned list back into a newline-separated string  
6. Rewrites the file with the updated data  

This automation ensures that access control rules stay current without requiring manual editing.

---
