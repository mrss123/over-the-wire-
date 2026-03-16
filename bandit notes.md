level 0 basic ls and seeing and reading files 
level 1 used a password form readme on level 0 and get access 
	it have - filed (dashed file) and opened by `./-`
	it have password for bandit2
level 2 used password from level 1
	it shows as space in the file name 
	opened it with \/ 
	have multiple file 
	i get back to the main repo
	cat "./--spaces in this filename--"
	showed the password for the next level 
level 3 used password from level 2
	found a password in inhere folder and continued 
level 4 used form level 3 found passoword in inhere folder
level 5 used form level 4 simply seeing every directory 
	
	file ./* to 
to see the file type manually 
	but the intended command was 
	`find . -type f -size 1033c ! -executable`
	and then  `cat .file2 `
level 6 used from level 5 password 
	same logic but differen finding method used from the clue given
	`find -user bandit7 -group bandit6 -size 33c 2>/dev/null`
level 7 used form level 6 
	under this level it was actually a bunch of names and strings infront of them 
	so i used grep to the hint name given on the web 
level 8 used from level 7 
	finding a char that occurs only once 
	`sort filename | uniq -u`
level 9 used from level 8
	finding a chr that is followed by = 
	`string filename | grep "="`
level 10 used from level 9
	the password was located in a encrypted base64 data
	`cat filename `
	copied the string 
	`echo "the string" | base64 -d `
level 11  used form level 10
	i actually didn't understand the command to execute this 
	`tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt`
	- `tr` = translate characters
	- `'A-Za-z'` = all letters
	- `'N-ZA-Mn-za-m'` = rotated letters
	- `< data.txt` = read input from the file
    This will **print the decoded password** directly to your terminal.
level 12 used from level 11
	this is by far the most complex decode routine i have saw from the challenge 
	the password was locked and encrypted with hexdump on multiple layer so i have to dcrypt it with different method again and again 
level 13 used from level 12 
	this is trickey it have private key that lets you to connect over ssh to get for the next level 
	i downloaded the file first to my local machine using same password i used to login bandit13 
	edited the file `chmod 600 sshkey.private`
	then i used same file to login directly to level 14 so i can login and use the password for the next level
		`ssh -i sshkey.private bandit14@bandit.labs.org -p 2220`
level 15 used from level 14 
	this one was easy 
	the discription says to submit the password i used to login on port 30000
		`telnet -a localhost 30000`
		i submitted the password and it provided the password 
		