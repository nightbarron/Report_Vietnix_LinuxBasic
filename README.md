# Report_Vietnix_LinuxBasic

## BASE COMMAND
`man <name_of_tool>` to see explain for tool and using Google Search to get more detail.

## 1. Check diskspaces
Code:
```
df -a
```
Result:
![Picture 01](src/01.png)


## 2. Check partitions
Code:
```
fdisk -l
```
Result:
![Picture 02](src/02.png)

## 3. Check cpu, ram, network
### 3.1 Check system realtime
Code:
```
top
```
Result:
![Picture 03](src/03.png)
Explain:

\- We can see system report at realtime monitoring with:
* `load average` as CPU GHz
*  `%Cpu(s) 3.4 us, 0.8 sy` as % CPU used for user and system
* `MidB Mem: ` as Memory used

### 3.2 Check network
Code:
```
netstat && netstat -s
```
Result 01:
![Picture 04](src/05.png)

Result 02:
![Picture 05](src/04.png)

# 4. Process Monitor
Code:
```
ps -aux
```
Result:
![Picture 06](src/06.png)

# OR

Code:
```
htop # as a full monitor tool.
```
Result:
![Picture 07](src/07.png)

Explain:
- We can use `htop` to see CPU stat, Mem stat and many process which is running in system. `htop` is a realtime tool.

# 5. List files/ directories
Code:
```
ls && ls -la
```
Result:
![Picture 08](src/08.png)
Explain: `ls` is command to show files/directories which have in dir, `ls -la` can also see `chmod` status of files/ folders inside.

# 6. Find, Copy, Move, Rename
## 6.1 Find
Code:
```
locate <str_to_find> # or using whereis for find src of tool
```
Result:

![Picture 09](src/09.png)

## 6.2 Copy, Move, Rename

Code:
```
cp <src file> <des file>
mv <src file> <des locate> # For move
mv <old name> <new name> # For rename
```
Result:

![Picture 10](src/10.png)

# 7. System Decentralization 

Code:
```
chmod a+x <file name>
chown <new user> <file to change owner>
chgrp <new gr> <file to change group owner>
```
Result:

![Picture 11](src/11.png)

Explain: 
* There are 3 types of rule with `r-read`, `w-write`, `x-excute` match with 4 types of urgent `u-user`, `g-group`, `o-other`, `a-all`.
* We can also using `chmod 777 hello.sh` for example to grant role with `1-excute`, `2-write`, `4-read`. The order of number is presented as `user_group_other`.

# 8. Editors

Code:
```
vi || gedit || nano
```
Explain:
* For `gedit`, we using as notepad
* For `nano`, when we editted, we can use `ctrl + s` to save and `ctrl + x` to exit
* For `vi`, press `i` to using insert mode. `ESC` to exit insert, `:wq` to save and exit, `:q!` to ignore change and exit.

# 9. Mount/ Unmount

Code:
```
mount <device name> <directory>
umount <dev name>

```
Result:
![Picture 12](src/12.png)

# Config: If we want the mount isn't umount after restart, we can edit `/etc/fstab` like below:

![Picture 13](src/13.png)

# 10. Symbolic Links

Code:
```
ln -s <target file> <sym link>
unlink <sym link> # or rm to remove link

```

Result:

![Picture 14](src/14.png)
