# Cheatsheet

https://www.commandlinefu.com/commands/browse

## Bash


#### 0. Shortcuts.


CTRL+A  # move to beginning of line
CTRL+B  # moves backward one character
CTRL+C  # halts the current command
CTRL+D  # deletes one character backward or logs out of current session, similar to exit
CTRL+E  # moves to end of line
CTRL+F  # moves forward one character
CTRL+G  # aborts the current editing command and ring the terminal bell
CTRL+J  # same as RETURN
CTRL+K  # deletes (kill) forward to end of line
CTRL+L  # clears screen and redisplay the line
CTRL+M  # same as RETURN
CTRL+N  # next line in command history
CTRL+O  # same as RETURN, then displays next line in history file
CTRL+P  # previous line in command history
CTRL+R  # searches backward
CTRL+S  # searches forward
CTRL+T  # transposes two characters
CTRL+U  # kills backward from point to the beginning of line
CTRL+V  # makes the next character typed verbatim
CTRL+W  # kills the word behind the cursor
CTRL+X  # lists the possible filename completefions of the current word
CTRL+Y  # retrieves (yank) last item killed
CTRL+Z  # stops the current command, resume with fg in the foreground or bg in the background

DELETE  # deletes one character backward
!!      # repeats the last command
exit    # logs out of current session


#### 1. Bash Basics.


export              # displays all environment variables

echo $SHELL         # displays the shell you're using
echo $BASH_VERSION  # displays bash version

bash                # if you want to use bash (type exit to go back to your normal shell)
whereis bash        # finds out where bash is on your system

clear               # clears content on window (hide displayed lines)


#### 1.1. File Commands.


ls                            # lists your files
ls -l                         # lists your files in 'long format', which contains the exact size of the file, who owns the file and who has the right to look at it, and when it was last modified
ls -a                         # lists all files, including hidden files
ln -s <filename> <link>       # creates symbolic link to file
touch <filename>              # creates or updates your file
cat > <filename>              # places standard input into file
more <filename>               # shows the first part of a file (move with space and type q to quit)
head <filename>               # outputs the first 10 lines of file
tail <filename>               # outputs the last 10 lines of file (useful with -f option)
emacs <filename>              # lets you create and edit a file
mv <filename1> <filename2>    # moves a file
cp <filename1> <filename2>    # copies a file
rm <filename>                 # removes a file
diff <filename1> <filename2>  # compares files, and shows where they differ
wc <filename>                 # tells you how many lines, words and characters there are in a file
chmod -options <filename>     # lets you change the read, write, and execute permissions on your files
gzip <filename>               # compresses files
gunzip <filename>             # uncompresses files compressed by gzip
gzcat <filename>              # lets you look at gzipped file without actually having to gunzip it
lpr <filename>                # print the file
lpq                           # check out the printer queue
lprm <jobnumber>              # remove something from the printer queue
genscript                     # converts plain text files into postscript for printing and gives you some options for formatting
dvips <filename>              # print .dvi files (i.e. files produced by LaTeX)
grep <pattern> <filenames>    # looks for the string in the files
grep -r <pattern> <dir>       # search recursively for pattern in directory


#### Directory Commands.


mkdir <dirname>  # makes a new directory
cd               # changes to home
cd <dirname>     # changes directory
pwd              # tells you where you currently are


#### SSH, System Info

ssh user@host            # connects to host as user
ssh -p <port> user@host  # connects to host on specified port as user
ssh-copy-id user@host    # adds your ssh key to host for user to enable a keyed or passwordless login

#### System INFO

whoami                   # returns your username
passwd                   # lets you change your password
quota -v                 # shows what your disk quota is
date                     # shows the current date and time
cal                      # shows the month's calendar
uptime                   # shows current uptime
w                        # displays whois online
finger <user>            # displays information about user
uname -a                 # shows kernel information
man <command>            # shows the manual for specified command
df                       # shows disk usage
du <filename>            # shows the disk usage of the files and directories in filename (du -s give only a total)
last <yourUsername>      # lists your last logins


#### Networks
ping <host>              # pings host and outputs results
whois <domain>           # gets whois information for domain
dig <domain>             # gets DNS information for domain
dig -x <host>            # reverses lookup host

##### 1.6 Téléchargements
wget <file>              # downloads file


#### Variables.


varname=value                # defines a variable
varname=value command        # defines a variable to be in the environment of a particular subprocess
echo $varname                # checks a variable's value
echo $$                      # prints process ID of the current shell
echo $!                      # prints process ID of the most recently invoked background job
echo $?                      # displays the exit status of the last command
export VARNAME=value         # defines an environment variable (will be available in subprocesses)

#### Input/Output Redirectors.


cmd1|cmd2  # pipe; takes standard output of cmd1 as standard input to cmd2
> file     # directs standard output to file
< file     # takes standard input from file
>> file    # directs standard output to file; append to file if it already exists
>|file     # forces standard output to file even if noclobber is set
n>|file    # forces output to file from file descriptor n even if noclobber is set
<> file    # uses file as both standard input and standard output
n<>file    # uses file as both input and output for file descriptor n
<<label    # here-document
n>file     # directs file descriptor n to file
n<file     # takes file descriptor n from file
n>>file    # directs file description n to file; append to file if it already exists
n>&        # duplicates standard output to file descriptor n
n<&        # duplicates standard input from file descriptor n
n>&m       # file descriptor n is made to be a copy of the output file descriptor
n<&m       # file descriptor n is made to be a copy of the input file descriptor
&>file     # directs standard output and standard error to file
<&-        # closes the standard input
>&-        # closes the standard output
n>&-       # closes the ouput from file descriptor n
n<&-       # closes the input from file descripor n


#### Processes

myCommand &  # runs job in the background and prompts back the shell

jobs         # lists all jobs (use with -l to see associated PID)

fg           # brings a background job into the foreground
fg %+        # brings most recently invoked background job
fg %-        # brings second most recently invoked background job
fg %N        # brings job number N
fg %string   # brings job whose command begins with string
fg %?string  # brings job whose command contains string

kill -l      # returns a list of all signals on the system, by name and number
kill <PID>               # kills (ends) the processes with the ID you gave
killall <processname>    # kill all processes with the name

ps           # prints a line of information about the current running login shell and any processes running under it
ps -a        # selects all processes with a tty except session leaders

trap cmd sig1 sig2  # executes a command when a signal is received by the script
trap "" sig1 sig2   # ignores that signals
trap - sig1 sig2    # resets the action taken when the signal is received to the default

disown <PID|JID>    # removes the process from the list of jobs

wait                # waits until all background jobs have finished

ps -u yourusername       # lists your processes
top                      # displays your currently active processes


#### HTOP
htop # Ouvre le progrmme htop

### date
date

#### Debugging


bash -n scriptname  # don't run commands; check for syntax errors only
set -o noexec       # alternative (set option in script)

bash -v scriptname  # echo commands before running them
set -o verbose      # alternative (set option in script)

bash -x scriptname  # echo commands after command-line processing
set -o xtrace       # alternative (set option in script)

trap 'echo $varname' EXIT  # useful when you want to print out the values of variables at the point that your script exits

#### Folders
##### List the size (in human readable form) of all sub folders from the current location
du -h --max-depth=1


#### FILES

### type recherche sur le type (d=répertoire, c=caractère, f=fichier normal)
### -name recherche sur le nom du fichier

##### Search recursively to find a word or phrase in certain file types, such as C code

find . -name "*.[ch]" -exec grep -i -H "search pharse" {} \; 

#### MOVE A file

### ls list absolute path of files in directory
ls -d "$PWD/"*

##### quickly rename a file
mv filename.{old,new}

#### REMOVE
##### Recursively remove all empty directories
find . -type d -empty -delete 

##### List only empty directories and delete safely (=ask for each)

find . -type d -empty -exec rm -i -R {} \;

### fzf
#### fzf cd 
"fzf shortuct cd" - > ALT + C
#### fzf history
"fzf shortuct history" - > CTRL + R

#### grep

pygmentize -g "/home/sulgi/scripts/cheatsheet/cheatsheet.md" | grep "text"

grep . filename > newfilename #Remove blank lines from a file using grep and save output to new file

pdftotext [file] - | grep 'YourPattern' #GREP a PDF file.

grep -lir "some text" * #find files containing text


### regex to find files
find . -type d -regextype posix-egrep -regex '^./([0-9]+[.]){3}[0-9]+[-][0-9]+'<--regex-->
find /usr/hdp -regextype sed -regex "\/usr\/hdp\/[0-9]*\.[0-9]*\.[0-9]*\.[0-9]*-[0-9]*" <!--regex-->

#### regex using egrep
ls /usr/hdp | egrep '[0-9]+.[0-9]+.[0-9]+.[0-9]+-[0-9]+' <!--regex-->

#### regex with globs
shopt -s extglob
touch /some/path/{2.6.0.3-8,22.66.0.333-8,foobar}
printf "%s\n" /some/path/+([0-9]).+([0-9]).+([0-9]).+([0-9])-+([0-9])

### history most often used commands

history | awk '{a[$2]++}END{for(i in a){print a[i] " " i}}' | sort -rn | head #List of commands you use most often

### history open firefox with website with fzf and awk
history | grep "firefox" | fzf | awk '{print $3, $4}' | xargs firefox


### amass
#### amass enum
amass enum -help #voir l'aide

##### amass verification passive dans un fichier texte
amass enum -passive -d site.com -o amass_enum_passive_d_nomsite_com.txt

##### amass enum ipv4
amass enum -src -ipv4 -d owasp.org

#### amass intel
##### amass ennumération à partir d'un nom d'entité
amass intel -org "Nom Entité"

##### amass recupération d'information à partir d'un ASN (IP pool données à des entités)
amass intel -asn 26608

##### amass récupération des whois de l'asn
amass intel -asn 26608 -whois

##### amass Classless Inter-Domain Routing
stratégie d'attribution des adresses de l'espace d'adressage IPv4 32 bits existant en vue de conserver l'espace d'adressage et de limiter le taux de croissance de l'état de routage mondial
amass intel -cdir 72.237.4.0/24

#### amass visualisation
amass viz -help
amass viz -dir ~/amass -d3 -o ./
firefox outputd3_amass.html

#### amass track
amass track -d owasp -history

#### amass db
amass db -list

amass db -enum 1 -show

### see my distribution
cat /etc/*release <!-- distro  distribution -->

### ffplay

#### ffplay open cam
ffplay /dev/video0

#### ffplay open cam good res no lag
ffplay -f v4l2 -input_format mjpeg -video_size 1920x1080 -framerate 60 -i /dev/video0 

### git
#### git remote add remote origin to prefill passwords 
git remote add origin https://user:password@bitbucket.org/user/repository.git

### Image magick
##### modifier le format d'une image

convert img.jpg -resize 100x100\! test1b.jpg 

### massdns

#### massdns help (in folder)
./bin/massdns -h

#### massdns AAAA verification from domains to results
./bin/massdns -r lists/resolvers.txt -t AAAA domains.txt > results.txt
./bin/massdns -r lists/resolvers.txt -t AAAA -w results.txt domains.txt

#### madns bruteforce
./scripts/subbrute.py lists/names.txt example.com | ./bin/massdns -r lists/resolvers.txt -t A -o S -w results.txt

### NETRPC

net rpc shutdown -I ipAddressOfWindowsPC -U username%password # Shutdown a Windows machine from Linux This will issue a shutdown command to the Windows machine. username must be an administrator on the Windows machine. Requires samba-common package installed

### PDF

#### croppdffile
pdfcrop --margins '0 -20 0 0' input.pdf output.pdf 

#### Mergepdffiles
pdftk file1.pdf file2.pdf cat output mergedfile.pdf 


### XDTOOL
xdotool click --repeat 300 --delay 1000 1

## Often used

##### Recupérer les ligne intéréssantes corespondantes à Keyword
history | grep "keyword"

##### expressvpn Connection vpn
expressvpn connect esma

#####  expressvpn Deconnection vpn
expressvpn disconnect

#### Bluetooth 

sudo systemctl restart bluetooth

cat /etc/*release 

### install deb files
sudo dpkg -i deb_file_name.deb


### vlc
#### vlc launch video
vlc westworld.mkv

#### vlc launch video fullscreen
vlc westworld.mkv --fullscreen

### OS
https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/
#### see os version linux
cat /etc/os-release

#### see os version linux with lsb_realease
lsb_release -a <!--os-->

#### see os with hostnamectl
hostnamectl  <!--os-->

### wifi
#### see save wifi passwords
sudo grep psk= /etc/NetworkManager/system-connections/* <!--wifi-->


### sed rename file
rename -n -v 's/^(\d+)._(.+)_S2\.mp4/$2_s02e$1.mp4/' *.mp4

### nmcli
#### activité wifi
nmcli radio
#### activité carte reseau
nmcli device
#### scan des wifi alentours nmcli
nmcli device wifi rescan
#### nmcli listing des wifi alentours
nmcli device wifi list
#### choix du wifi nmcli fzf
nmcli device wifi list | fzf

#### connection au réseau
nmcli device wifi connect SSID-Name password wireless-password

### word count with wc
wc honeypot.md

### word count of all folder
ls | xargs wc

## line count all folder
ls | xargs wc -l

## pygments
### add color terminal
pygmentize -O full,style=monokai hello.go
pygmentize -O full,style=native hello.go
pygmentize -O full,style=vim hello.go

pygmentize -O full,style=monokai hello.go | while read i; do echo $i; sleep 1 ; done

##Code qui défile en couleur
clear && pygmentize -O full,style=monokai hello.go | while read i; do echo $i; sleep 1 ; done


