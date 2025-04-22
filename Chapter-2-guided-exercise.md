- Login to the system with the `student` user.
- Open the command line terminal by clicking on `Activities >> Terminal` 
- Check the file system hierarchy by navigaeting to /
```bash
cd /
ls -l
```
- Check present working directory
```bash
pwd
```
- Create following files in the `Home Directory` of student.
```bash
cd /home/student
pwd
touch song1.mp3 song2.mp3 song3.mp3 song4.mp3 song5.mp3 song6.mp3
touch snap1.jpg snap2.jpg snap3.jpg snap4.jpg snap5.jpg snap6.jpg
touch filml.avi film2.avi film3.avi film4.avi film5.avi film6.avi
```
- Move all songs files to `Music` directory.
```bash
mv song1.mp3 song2.mp3 song3.mp3 song4.mp3 song5.mp3 song6.mp3 Music
```
- Move all the snap files to `Pictures` directory
```bash
mv snap1.jpg snap2.jpg snap3.jpg snap4.jpg snap5.jpg snap6.jpg Pictures
```
- Move all the film files to `Videos` directory
```bash
mv filml.avi film2.avi film3.avi film4.avi film5.avi film6.avi Videos
```
- Check the content of `Music` directory
```bash
ls -l Music
```
- Check the content of `Pictures` directory
```bash
ls -l Pictures
```
Check the content of `Videos` directory
```bash
ls -l Videos
```
- Make following directories and check that directories are created.
```bash
mkdir friends family work
ls -l friends
ls -l family
ls -l work
```
- Copy the song1 and song2, snap1 and snap2, file1 and filme2 to `friends` directory.
```bash
cd friends
cp ~/Music/song1.mp3 ~/Music/song2.mp3 ~/Pictures/snap1.jpg ~/Pictures/snap2.jpg ~/Videos/film1.avi ~/Videos/film2.avi .
```
- Copy the song3 and song4, snap3 and snap4, file3 and filme4 to `family` directory.
```bash
cd family
cp ~/Music/song3.mp3 ~/Music/song4.mp3 ~/Pictures/snap3.jpg ~/Pictures/snap4.jpg ~/Videos/film3.avi ~/Videos/film4.avi .
```
- Copy the song5 and song6, snap5 and snap6, file5 and filme6 to `work` directory.
```bash
cd work
cp ~/Music/song5.mp3 ~/Music/song6.mp3 ~/Pictures/snap5.jpg ~/Pictures/snap6.jpg ~/Videos/film5.avi ~/Videos/film6.avi .
```
- Now check the copied content in respective directories.
```bash
ls -l ~/friends
ls -l ~/family
ls -l ~/work
```
- Now try to remove the friends, family directory.

Note:- Below command will fail as these directories are not empty

```bash
rmdir ~/friends
rmdir ~/family
```
- Now remove these directories with rm command and with -r parameter to remove recursively.
```bash
rm -r ~/friends
rm -r ~/family
ls -l ~/friends ~/family
```
- Navigate to work directory and remove each file manually.
```bash
cd ~/work
rm song5.mp3 song6.mp3 snap5.jpg snap6.jpg film5.avi film6.avi
ls -l
```
