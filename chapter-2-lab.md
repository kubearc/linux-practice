# 🛠️ Lab Instructions – Node1 (User: `student`)

**Start in your home directory:** `/home/student`

---

## ✅ Tasks

### 1. Create Practice Files
Create empty files for practice. If a shortcut doesn’t work, explore or use tab-completion to help.

---

### 2. Create TV Episode Files
In `/home/student`, create 12 files named like:
```
tv_seasonX_episodeY
```
Where `X` = 1 or 2 (season) and `Y` = 1 to 6 (episode).

---

### 3. Create Book Chapter Files
Create 8 files in `/home/student`:
```
mystery_chapter1.odf` to `mystery_chapter8.odf
```

---

### 4. Organize TV Episodes into Folders
Create the following folders using one command:
```
/home/student/Videos/season1
/home/student/Videos/season2
```

---

### 5. Move TV Episodes into Season Folders
Move:
- Season 1 episodes → `/home/student/Videos/season1`
- Season 2 episodes → `/home/student/Videos/season2`

Use **two commands**, use **relative paths**.

---

### 6. Create Book Chapter Directory Structure
In one command, create:
```
/home/student/Documents/my_bestseller/chapters
```

---

### 7. Create More Directories
Inside `/home/student/Documents/my_bestseller`, create:
- `editor`
- `plot_change`
- `vacation`  
(Use one command)

---

### 8. Move Chapter Files to Chapters Folder
Move all 8 chapter files from `/home/student` to:
```
/home/student/Documents/my_bestseller/chapters
```

Use `.` as the destination if you're already in the `chapters` directory.

---

### 9. Send Chapters 1 & 2 to Editor
From inside `chapters`, move:
- `mystery_chapter1.odf`
- `mystery_chapter2.odf`  
To `../editor` using **relative paths**.

---

### 10. Send Chapters 7 & 8 on Vacation
Move `mystery_chapter7.odf` and `mystery_chapter8.odf` to `../vacation` in **one command**.

---

### 11. Copy Season 2, Episode 1 to Vacation
Go to `/home/student/Videos/season2` and copy:
```
tv_season2_episode1 → /home/student/Documents/my_bestseller/vacation
```

---

### 12. Add Episode 2 to Vacation Using Directory Shortcuts
From `vacation`:
- List files
- Go back to `season2`
- Copy `tv_season2_episode2` to `vacation`
---

### 13. Copy Chapters 5 & 6 for Plot Changes
From `my_bestseller`, copy:
```
mystery_chapter5.odf and mystery_chapter6.odf → plot_change
```

(Use **one command**)

---

### 14. Back Up Chapter 5 in 3 Ways
In `plot_change`:
- `mystery_chapter5-YYYY-MM-DD.odf`
- `mystery_chapter5-<timestamp>.odf`
- `mystery_chapter5-$USER.odf`

*Optional: Repeat for Chapter 6.*

---

### 15. Clean Up Plot Change Directory
- Delete files in `plot_change`
- Go up one level
- Try `rm plot_change` (expect failure)
- Then use `rmdir plot_change` (should succeed)

---

### 16. Remove Vacation Folder
Delete using:
```
rm -r /home/student/Documents/my_bestseller/vacation
```

---

### 17. Return to Home
Use:
```
cd ~
```

---

_Last updated: 2025-04-24_
