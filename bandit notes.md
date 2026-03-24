## level 0 basic ls and seeing and reading files 

## level 1 used a password form readme on level 0 and get access 
	it have - filed (dashed file) and opened by `./-`
	it have password for bandit2

## level 2 used password from level 1
	it shows as space in the file name 
	opened it with \/ 
	have multiple file 
	i get back to the main repo
	
	cat "./--spaces in this filename--"
	
	showed the password for the next level 

## level 3 used password from level 2
	found a password in inhere folder and continued 

## level 4 used form level 3 found passoword in inhere folder

## level 5 used form level 4 simply seeing every directory 
	
	file ./* to 

to see the file type manually 
	but the intended command was 
	
	`find . -type f -size 1033c ! -executable`
	
and then  `cat .file2 `

## level 6 used from level 5 password 
same logic but differen finding method used from the clue given

	`find -user bandit7 -group bandit6 -size 33c 2>/dev/null`

## level 7 used form level 6 
	under this level it was actually a bunch of names and strings infront of them 
	so i used grep to the hint name given on the web 

## level 8 used from level 7 
	finding a char that occurs only once 

	`sort filename | uniq -u`

## level 9 used from level 8
	finding a chr that is followed by = 

	`string filename | grep "="`

## level 10 used from level 9

the password was located in a encrypted base64 data

	`cat filename `
	
copied the string 

	`echo "the string" | base64 -d `

## level 11  used form level 10

	i actually didn't understand the command to execute this 
	`tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt`
	
- `tr` = translate characters
	- `'A-Za-z'` = all letters
	- `'N-ZA-Mn-za-m'` = rotated letters
	- `< data.txt` = read input from the file
    This will **print the decoded password** directly to your terminal.

## level 12 used from level 11

this is by far the most complex decode routine i have saw from the challenge 
	the password was locked and encrypted with hexdump on multiple layer so i have to dcrypt it with different method again and again 

## level 13 used from level 12 

this is trickey it have private key that lets you to connect over ssh to get for the next level 
	i downloaded the file first to my local machine using same password i used to login bandit13 
	edited the file
	
		`chmod 600 sshkey.private`
	
then i used same file to login directly to level 14 so i can login and use the password for the next level
		
		`ssh -i sshkey.private bandit14@bandit.labs.org -p 2220`

## level 14 used a password form the previous session 

this one was easy 
the discription says to submit the password i used to login on port 30000
	
		`telnet -a localhost 30000`
i submitted the password and it provided the password 
## level 15 same used password from the past one 
 this one needs to undersanding of how ssl/tls handshake works 
 - the discription states i need to connect over port 30001
 - i read the manual
 - 
   		`openssl s_client localhost:30001`
   
   hen submitted the password i used to login to level 15 and it was correct
## level 16 used password form level 15
- this one was a bit trickey but have multiple very good concepts on network and it way of connections
- as the previous level this one needs ssl/tls connection to get the next level password
- but first you need to i dentify which port is litening for `31000-32000`
- first i tried to see what ports are active on the local machine

  		`netstat -tuln`
  
- i found some ports on the specified port range but none of them were open for ssl/tls
- so i did nmap scan

   		`nmap -sV localhost -p 31000-32000`
  
-  this gave me some port that didin't show up before
-  so i use the openssl command to communicate and get what there is

  		 `openssl s_client -connect localhost:31790 `
   
-  this was the only one who responded with a private key
-  but this private key didn't work

    	`openssl s_client -connect localhost:31790 -quiet `
   
-  	used the queit flag to reduce the jargon and it worked i submitted the password and gave me new private key for level 17
-  	i used this key
  and on my local machine

		`nano mykey.pem`

		`chmod 600 mykey.pem`
 		
		`ssh -i mykey.pem bandit17@bandit.labs.overthewire.org -p 2220`

- and it worked i used so i directly started to search the folders
- and found it under etc file

		 `cat etc/bandot_pass/bandit17`
 ## level 17 used password form the previous level 
 - this one interesting it requuires to use the command diff
 - the clue was there are 2 files and the diffrence is the password for level 18
so i read the manual 

   		`diff --normal password.old password.new`
   
i got the password for level 18
## level 18 used the previous level password 
-  the problem was it immedietly closes the machine

		`ssh bandit18@bandit.labs.org -p 2220 "cat readme"`
## level 19 used form the previous level 
- this level was more of technical
- i found there is executable file that is only set for a user so i run it as is

  		./bandit20-do cat /etc/bandit_pass/bandit20
- like level 17 -18
## level 20 used from previous level 
- on this level there was a setuid file that connects to a localhost on a specified port given

	  echo "the password from previous level" | netcat -lp <port>
      ./suconnect <port>
## level 21 used form previous levle
- this level have new concept
- it have a cron command
- cron is a demon that execute automically on background with on schedule time
- so first i found the cron.d file and read

		man crontab
  		cd \/
  		cd etc/cron.d
  		cat cronjob_bandit22
   		cat /usr/bin/cronjob_bandit22.sh
  		cat /tmp/jargon 
