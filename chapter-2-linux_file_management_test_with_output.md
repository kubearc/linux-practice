==============================

🧪 LINUX FILE MANAGEMENT PRACTICE TEST WITH OUTPUT

==============================

📌 INSTRUCTIONS:
This version includes the commands and their expected output (simulated where necessary). Run each command and compare your output.

🔹 TASK 1: BASIC FILE OPERATIONS
------------------------------
1. Create an empty file:
``` bash
   # touch testfile.txt
```
2. Write to the file:
``` bash
  $ echo "Hello Linux" > testfile.txt
```
3. Display contents:
```Bash
   $ cat testfile.txt
   Output: Hello Linux
   ```
4. Copy file:
``` bash
   $ cp testfile.txt copyfile.txt
```
5. Rename file:
``` bash
   $ mv copyfile.txt renamedfile.txt
```
🔹 TASK 2: DIRECTORY OPERATIONS
------------------------------
6. Create a directory:
``` bash
   $ mkdir myfolder
```
7. Move file into directory:
``` bash
   $ mv testfile.txt myfolder/
```
8. Change into directory and list:
``` bash
   $ cd myfolder
   $ ls
   Output: testfile.txt
```
9. Create a new file:
``` bash
   $ touch notes.txt
```
10. Go back:
``` bash
    $ cd ..
```

🔹 TASK 3: ADVANCED FILE MANAGEMENT
------------------------------
11. Copy directory with contents:
``` bash
    $ cp -r myfolder backupfolder
```
12. Delete a file:
   ``` bash
    $ rm myfolder/notes.txt
```

13. Delete a folder:
``` bash
    $ rm -r backupfolder
```
14. List files by time:
```bash   
$ ls -lt
```
15. Show hidden files:
``` bash   
$ ls -a
    Output includes: . .. .bashrc .profile etc.
```
🔹 TASK 4: BONUS (CHALLENGE)
------------------------------
16. Create nested structure and file:
``` bash   
$ mkdir -p nested/inside/deep && touch nested/inside/deep/depth.txt
```

17. View first 5 lines:
``` bash   
$ head -n 5 myfolder/testfile.txt
```
✅ Clean up when finished:
``` bash
$ rm -rf myfolder backupfolder nested renamedfile.txt testlink
```
==============================
