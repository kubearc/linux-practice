
# ==============================
# 🧪 VIM COMMAND PRACTICE TASKS WITH ANSWERS
# ==============================

# 📌 INSTRUCTIONS:
# Each task includes the correct Vim command to help you learn.
# copy the /etc/passwd file to a new file named /passwdbackup      
#  open the /passwdbackup file and perform all the task 
 
  🔹 TASK 1: MOVEMENT
 ------------------------------
 1. Move to the top of the file
``` bash
    #     gg
```
    
 2. Move to the bottom of the file
``` bash
   # G
```
 3. Move to the end of the line
``` bash
    # $
```
 4. Move to the beginning of the line
```
   # ^
```
 5. Jump to line 20
``` bash
  # :20
```
 🔹 TASK 2: INSERTING TEXT
   ------------------------------
 6. Insert your name at the top
``` bash
in command Mode press gg then O
```
 7. Add a new line after line 10
``` bash
  # :10 then o
```
 8. Append " - Practice Complete"
```  bash
   # A then type the text
```
🔹 TASK 3: DELETING TEXT
 ------------------------------
 9. Delete a line
```bash
   # dd
```
 10. Delete first word on next line
``` bash
# dw
```

 🔹 TASK 4: COPYING & PASTING
 ------------------------------
 11. Yank line 15
``` bash
 # :15 then yy
```
 12. Paste it below
``` bash
    p
```
 13. Paste it above
``` bash
 #  P
```

 🔹 TASK 5: SEARCH & REPLACE
 ------------------------------
 14. Search for "TASK"
``` bash
 #  /TASK
```
 15. Replace "TASK" with "CHALLENGE"
``` bash
 # :%s/TASK/CHALLENGE/g
```
 🔹 TASK 6: UNDO, REDO, SAVE & EXIT
 ------------------------------
 16. Undo last change
``` bash
 # u
```
 17. Redo change
 ``` bash
Ctrl + r
```
 18. Save the file
``` bash
 # :w
 ```
 19. Quit Vim
``` bash
 # :q
```
 20. Save and quit
``` bash
 # :wq
```


# 🎉 Great job! Keep practicing until it's muscle memory!
# ==============================
