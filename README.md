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
