---
title: "OverTheWire: Bandit, Level 0-10 Write-up"
date: 2024-10-24 00:00:00 +212
categories: [CTF challenges]
tags : [CTF , Challenges , OverTheWire , overthewire-bandit ]
image:
  path: assets/headers/bandit.webp
  alt: OverTheWire-Bandit 
---



## Introduction

 OverTheWire is a community that can help you learn and practice security concepts in the form of fun games. They offer many war games to practice your skills.

![image](https://user-images.githubusercontent.com/84661482/132092828-c917b13e-0df0-4052-b7a7-a7a9d7162d8f.png)

 The first set of challenges is called "Bandit", which is a Linux CLI tutorial, where the goal of each level is to discover the password to move on to the next level.

![image](https://user-images.githubusercontent.com/84661482/132092898-322b815b-674e-4dd7-a457-e824d910ae43.png)

##  Level 0
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is ``` bandit.labs.overthewire.org ``` , on port ``` 2220 ```. The username is ``` bandit0 ``` and the password is  ```bandit0 ```:

```
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
bandit0@bandit:~$
```
##  Level 0 → 1

 The password for the next level is stored in a file called  ```readme``` located in the ``` home ``` directory. Use this password to log into ``` bandit1 ``` using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

```
$ ssh bandit0@bandit.labs.overthewire.org -p 2220

bandit0@bandit:~$ ls
readme

bandit0@bandit:~$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```
##  Level 1 → 2
 The password for the next level is stored in a file called ``` - ``` located in the home directory.
```
$ ssh bandit1@bandit.labs.overthewire.org -p 2220

# use absolute path
bandit1@bandit:~$ cat /home/bandit1/-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

# OR, "hide" the dash from the command
bandit1@bandit:~$ cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```
##  Level 2 → 3
 The password for the next level is stored in a file called ``` spaces in this filename ``` located in the home directory.
```
$ ssh bandit2@bandit.labs.overthewire.org -p 2220

bandit2@bandit:~$ cat "spaces in this filename"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

# or use backslashes
bandit2@bandit:~$ cat spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```
##  Level 3 → 4
 The password for the next level is stored in a hidden file in the ``` inhere ``` directory.
```
$ ssh bandit3@bandit.labs.overthewire.org -p 2220

bandit3@bandit:~$ ls -la inhere/
total 12
drwxr-xr-x 2 root    root    4096 Oct  5 06:19 .
drwxr-xr-x 3 root    root    4096 Oct  5 06:19 ..
-rw-r----- 1 bandit4 bandit3   33 Oct  5 06:19 .hidden

bandit3@bandit:~$ cat inhere/.hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```
##  Level 4 → 5
 The password for the next level is stored in the only human-readable file in the ``` inhere ``` directory. Tip: if your terminal is messed up, try the ``` reset ``` command.
```
$ ssh bandit4@bandit.labs.overthewire.org -p 2220

bandit4@bandit:~$ ls -la inhere/
total 48
drwxr-xr-x 2 root    root    4096 Oct  5 06:19 .
drwxr-xr-x 3 root    root    4096 Oct  5 06:19 ..
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file00
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file01
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file02
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file03
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file04
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file05
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file06
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file07
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file08
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file09

# check content first
bandit4@bandit:~$ file inhere/*
inhere/-file00: data
inhere/-file01: data
inhere/-file02: data
inhere/-file03: data
inhere/-file04: data
inhere/-file05: data
inhere/-file06: data
inhere/-file07: ASCII text
inhere/-file08: data
inhere/-file09: data

bandit4@bandit:~$ cat inhere/-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```
##  Level 5 → 6
 The password for the next level is stored in a file somewhere under the ``` inhere ``` directory and has all of the following properties: human-readable, 1033 bytes in size, not executable.
```
$ ssh bandit5@bandit.labs.overthewire.org -p 2220

bandit5@bandit:~/inhere$ find . -type f -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```
##  Level 6 → 7
 The password for the next level is stored somewhere on the server and has all of the following properties: owned by user ``` bandit7 ```, owned by group ``` bandit6 ```, ``` 33 ```bytes in size.
```
$ ssh bandit6@bandit.labs.overthewire.org -p 2220

bandit6@bandit:/$ find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
/var/lib/dpkg/info/bandit7.password

bandit6@bandit:/$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```
##  Level 7 → 8
 The password for the next level is stored in the file ``` data.txt ``` next to the word ``` millionth ``` .
```
$ ssh bandit7@bandit.labs.overthewire.org -p 2220

bandit7@bandit:~$ ls
data.txt

bandit7@bandit:~$ cat data.txt | grep millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP

# or in a one-liner
bandit7@bandit:~$ ls | xargs cat | grep millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```
##  Level 8 → 9
 The password for the next level is stored in the file ``` data.txt ``` and is the only line of text that occurs only once.
```
$ ssh bandit8@bandit.labs.overthewire.org -p 2220

bandit8@bandit:~$ sort data.txt | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```
##  Level 9 → 10
 The password for the next level is stored in the file ``` data.txt ``` in one of the few human-readable strings, preceded by several ``` = ``` characters.
```
bandit9@bandit:~$ strings data.txt | grep "="
========== the*2i"4
=:G e
========== password
<I=zsGi
Z)========== is
A=|t&E
Zdb=
c^ LAh=3G
*SF=s
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
S=A.H&^
bandit9@bandit:~$
```