
# Chapter 010 - Guided Exercise 01 - Creating Tar Files

## Objective
Learn how to create a `.tar` archive, extract it, and transfer it between systems using `scp`.

---

## Steps

### 1. Login  
Login as the `student` user on **Node1**.

### 2. Create 5 `.mp3` Files
```bash
cd ~
touch song{1..5}.mp3
```

### 3. Create a Tar Archive from the 5 Files
```bash
tar -cvf all_songs.tar song1.mp3 song2.mp3 song3.mp3 song4.mp3 song5.mp3
```

### 4. Create a Folder `~/extracted-data` and Copy the Tar File into it.
```bash
mkdir ~/extracted-data
cp ~/all_songs.tar ~/extracted-data/
cd ~/extracted-data
```

### 5. Extract the `all_songs.tar` Tar File in the Directory and verify the extracted files.
```bash
tar -xvf all_songs.tar
ls -l
```

### 6. Prepare the Destination Directory on Node2
```bash
ssh student@node2
mkdir -p /home/student/extracted-node1
ls /home/student/extracted-node1
exit
```

### 7. Copy the Tar File to Node2
```bash
scp ~/all_songs.tar student@node2:/home/student/extracted-node1/
```

---

## Notes
- Replace `node2` with the actual hostname or IP address of Node2.
- Ensure SSH access is configured between the nodes.
