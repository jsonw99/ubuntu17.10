### ubuntu17.10 setup

#### 1. chinese input
https://askubuntu.com/questions/59356/how-do-i-get-chinese-input-to-work <br />
First install ibus-libpinyin
```bash
sudo apt-get install ibus-libpinyin
```
Then, run the following command:
```bash
gsettings set org.gnome.desktop.input-sources sources "$(gsettings get org.gnome.desktop.input-sources sources | sed "s/]/, ('ibus', 'libpinyin')]/")" 
```
The command above takes output of gsettings get org.gnome.desktop.input-sources sources, gives it to sed, which removes the last square bracket and appends , ('ibus', 'libpinyin')] to its output. That particular schema has entries in format [(INPUTMETHOD1, LANGUAGE1), (INPUTMETHOD1,LANGUAGE2)], so this is the reason why sed has to be used to insert text in that fassion. Finally we use output of that as input for gsettings set command, through parameter substitution with $( . . . )

#### 2. Quick Fix to mount Windows partition immediately
```bash
sudo ntfsfix /dev/sdXY
```
where XY is the troublesome partition shown in the error. For example sda2 or sdb1 or sda5. ntfsfix is already installed in Ubuntu systems.

#### 3. Find number of files in folder and sub folders?
```bash
find . -type f | wc -l
find . -type f -name '*.png' | wc -l
```

#### 4. Convert all *.png to *.jpg
```bash
sudo apt-get install parallel imagemagick
find -type f -name '*.png' | parallel --eta convert '{}' '{.}.jpg'
find -type f -name '*.png' -delete
```

#### 5. Check which process is running on port 5000
```bash
lsof -i:5000
```

#### 6. Check memory usage
```bash
watch -n 1 free -m
```

#### 7. Check storage usage
```bash
df -h
```

#### 8. Extending a Linux File System after Resizing the Volume
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html
```bash
df -h
lsblk
sudo growpart /dev/xvdf 1
lsblk
sudo resize2fs /dev/xvdf1
```

#### 9. Copy large file or directory
```bash
rsync --info=progress2 sourceFile destinationFile
rsync -r --info=progress2 sourceFolder/ destinationFolder/

```

#### 10. Check directory size
```bash
du -hs targetFolder
```
