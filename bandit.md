# Bandit Over The Wire Write-Ups

## Level 0

Here we are asked to connect to a server located at port 2220

` ssh bandit0@bandit.labs.overthewire.org -p 2220`

now read the readme file

`cat readme`

password obtained: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

---

## Level 1

` ssh bandit1@bandit.labs.overthewire.org -p 2220`

we have to access a file named - located in the home directory

`cat./-`

password obtained:rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

---

## Level 2

` ssh bandit2@bandit.labs.overthewire.org -p 2220`

we will put the filename in quotes as it contains spaces

`cat "spaces in this filename"`

password obtained: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

---

## Level 3

` ssh bandit3@bandit.labs.overthewire.org -p 2220`

a hidden file starts with '.'. first enter the inhere directory and then access the hidden file

`cd inhere`
`ls -a` this will show the list of files in that directory (the hidden ones too)

`cat .hidden` read the hidden file

password obtained: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

---

## Level 4

` ssh bandit4@bandit.labs.overthewire.org -p 2220`

`cd inhere` - enter the inhere directory

`ls` - display all the files

`file ./-file0*` - display the type of all the files of the type file0X

the file which is human readable will be of the type ASCII text. Read the desired file

`cat ./-file07`

password obtained: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

---

## Level 5

` ssh bandit5@bandit.labs.overthewire.org -p 2220`

`cd inhere`

now find the files which are 1033 bytes in size and non-executable. The file with the ASCII text type is the desired file.

`find . -size 1033c ! -executable`

`cd maybehere07`

`cat .file2`

password obtained: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

---

## Level 6

` ssh bandit6@bandit.labs.overthewire.org -p 2220`

`cd /` - enter the home directory as the desired file is located 'somewhere on the server'

`find -user bandit7 -group bandit6 -size 33c`

`cat bandit7.password`

password obtined: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

---

## Level 7

` ssh bandit7@bandit.labs.overthewire.org -p 2220`

`ls`

`strings data.txt | grep millionth`
strings function outputs the printable lines from the file and gives it as an input to the next command viz grep through the pipe operator. grep xyz outputs the string next to xyz.

password obtained: TESKZC0XvTetK0S9xNwm25STk5iWrBvP

---

## Level 8

` ssh bandit8@bandit.labs.overthewire.org -p 2220`

`sort data.txt | uniq -u`
sorts command sorts the data in alphabetical order, hence duplicate strings will be together. uniq -u prints only unique lines on the sorted data.

password obtained: EN632PlfYiZbn3PhVK3XOGSlNInNE00t

---

## Level 9

` ssh bandit9@bandit.labs.overthewire.org -p 2220`

`strings data.txt | grep "==="`

this will output the lines which contain 3 '===' or more. the next word is your password.

password obtained: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

---

## Level 10

` ssh bandit10@bandit.labs.overthewire.org -p 2220`

`strings data.txt | base64 -d`

base64 -d decodes the base 64 encoded data piped in.

password obtained: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

---

## Level 11

` ssh bandit11@bandit.labs.overthewire.org -p 2220`

`cat data.txt | tr [a-mA-Mn-zN-Z] [n-zN-Za-mA-M]`

the tr command rotates each character by a given number of positions

password obtained: JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

---

## Level 12

` ssh bandit12@bandit.labs.overthewire.org -p 2220`

`ls`
~ data.txt

make a new directory, copy data.txt over there and rename it. then decompress that file containing hexdump data.

```
mkdir /tmp/suhani123
cd /tmp/suhani13
cp ~/data.txt /tmp/suhani123

mv data.txt hexdump_data

xxd -r hexdump_data compressed
```

`
file compressed` -gzip compressed data

` gzip -d compressed.gz` - decompressing

`file compressed` -bzip2 compressed data

` bzip2 -d compressed.bz2` - decompressing

this process of decompressing continues for 2 more times.

`file compressed` - POSIX tar archive (still compressed)

`tar -xvf compressed.tar` - outputs a file named data5.bin decompressed to some extent

now,
data5.bin (tar) --> outputs data6.bin (bzip2)

`mv data6.bin compressed2.bzip2` - move and rename

...this process continues for 4 more times

(bzip2--> tar --> gzip --> tar)
finally,

`file compressed.tar`
~ ASCII text

`cat compressed.tar`

password obtained: wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

---

## Level 13

` ssh bandit13@bandit.labs.overthewire.org -p 2220`

the password for the next level can only be accessed if we login to the next level through the sshkey

`ls` ~sshkey.private

login to the next level now, through the key obtained above using ssh -i command (as an identification proof for the key)

` ssh bandit14@bandit.labs.overthewire.org -p 2220 -i sshkey.private`

` cd /etc/bandit_pass`

`cat bandit14`

password obtained: fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

---

## Level 14

` ssh bandit14@bandit.labs.overthewire.org -p 2220`

the password obtained in the previous level is to be submitted to port 30000 on localhost

`echo "fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq" | nc localhost 30000`

echo command reads the password and outputs it to nc which in turn esatblishes a connection between the mentioned host and port

password obtained: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

---

## Level 15

` ssh bandit15@bandit.labs.overthewire.org -p 2220`

` openssl s_client -connect localhost:30001`

this command allows us to establish a SECURE connection between the said host and port (by ssl encryption)

now, paste the password obtained previously

password obtained: JQttfApK4SeyHwDlI9SXGR50qclOAil1

---

## Level 16

` ssh bandit16@bandit.labs.overthewire.org -p 2220`

`nmap localhost -p 31000-32000`

nmap scans all the ports in the given range and shows their status (outputs those which are open)

5 ports will be shown. check each port if they have a server listening on them or not. if they do, a secure ssl connection can be established.

`openssl s_client -connect localhost: 31790`

_connection established_

paste the password ontained previously.

An RSA private key will be obtained. exit this level, open another file using nano command and paste this key so as to be able to use it in the next level.

` nano rsakey.private`

---

## Level 17

` ssh bandit17@bandit.labs.overthewire.org -p 2220 -i rsakey.private`

`ls` ~ passwords.new passwords.old

`diff passwords.old passwords.new`

2 passwords are shown, indicating this is the only difference in the 2 files.

Since passwords.new contains our password, the latter becomes our desired password.

password obtained: hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg

---

## Level 18

` ssh bandit18@bandit.labs.overthewire.org -p 2220 -T`

if we use the above command without the -T flag, it will log you out.
since .bashrc has been modified, we use the -T flag to run commands through ssh without any terminal interaction.
After that, simply read the file in it

`ls`

`cat readme`

password obtained: awhqfNnAbc1naukrpqDYcF95h7HoMTrC

---

## Level 19

`ssh bandit19@bandit.labs.overthewire.org -p 2220`

`./bandit20-do cat /etc/bandit_pass/bandit20`

the setuid file bandit20-do will let me run commands as user 'bandit20'. thus, using this we can read the password from the given directory

password obtained: VxCazJaVykI6W36BkBU0mJTCM8rR95XT

---

## Level 20

`ssh bandit20@bandit.labs.overthewire.org -p 2220`

here we will open 2 terminal windows, to establish connection between server and client.

server-

`ls` ~ suconnect

`./suconnect 8000`

client-

`nc localhost 8000`

_enter previous password _

~ password matches, sending next password

LEVEL CLEARED

## Done :)
