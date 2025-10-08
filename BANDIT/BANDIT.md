# LEVEL 0

- I was given credential to log in along with the link
- Initally , what i did was used ssh -p 2220 link , and yes it did login but as root itself and not bandit.
- Then i added username -->  ` ssh -p 2220 user@link  --> Passed level 0 `

# LEVEL 0 -> LEVEL 1

- This one was easy as well 
- first log out from bandit 0
- Login to bandit 1 --> ` ssh -p 2220 bandit1@bandit.labs.overthewire.org ` 
- Then i used ` cat readme ` to get the password -> ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

# LEVEL 1 -> LEVEL2 

- Now for this i moved to home directory --> Bandit1 

- In this we have a file called -->  -  

- From this , when i used cat , it did not return anything , so i tried --> ` cat .\ - `

- Hence , the password is --> 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

# LEVEL 2 -> LEVEL 3

- Next we have aa file called ==> --spaces in this filename-- 

- We cannot dirctly use the file name as it is because there are spaces and if we write it as it is ie ` cat --spaces in this filename-- ` , then cat will consider this to be four different files , so to resolve this  , we use the command as --> ` cat .\--spaces in this filename-- `.

- Password --> MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

# LEVEL 3 -> LEVEL 4

- Here we can see that the file with password is hidden 

- ls gives us only files which are non-hidden

- now in order to open the file , which are hidden , we use --> ` ls -a ` 

- And then we use ` cat ...Hiding-From-You `

- Finally , we are done ,we get the password --> 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

# LEVEL 4 -> LEVEL 5

- The ` file ./file_name `command will give us what kind of format is the file in ,like ascii or unicode or elf etc 
- In this , we are given human readable files
- The most common data encodings that are human-readable are ASCII and Unicode.
- Here what we did was , just first find the formal of the file usng command ` file .\* `, we used `*` so that we dont have to write the command individually for each file
- Then , what we can do is , we get the firat and then direcclt do ` cat ./file07 ` we get the password --> 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

# LEVEL 5 -> LEVEL 6

- Here we had numerous dir and files , we can use file ./* command in each dir and do it manually , but this can be tedious
- So better option is using the command ` find `
- command is as follows ` find . i -type f -size 1033c ! -executable `
    - Here `find` ia the command used 
    - .  means, start from current directory
    - -type f , means search/consider only files 
    - -size 1033c , is 1033 is the size and c is used for bytes where for blocks we use b
    - ! this is not symbol ,so ! -executable means --> not executable
    - So this command means --> give me all the files , with size 1033 bytes and which are not executable .
- I did go to maybehere07 ,but shockingly file2 wasnt there and then  i did ` ls -a ` and i found the file , lol
- Password is --> HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

# LEVEL 6 -> LEVEL 7

- Here we learnt about 2 types of ownership in linux , they are one as group and other as user
- So her =e we had to find a password, where user was bandit7 and group was bandit6
- this ones easy , just use ` find / -type f -size 33c -user bandit7 -group bandit6 `
- we get it --> morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

# LEVEL 7 -> LEVEL 8

- The password was in data.txt , besgdes millionth
- Just used ` cat data.txt | grep millionth ` , this fetched me password --> dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

# LEVEL 8 -> LEVEL 9

- Here we were having data.txt file with so , sooo many repeating lines , so i did cat.txt to see if it if i can find the password manually , but quite tough
- so the best command i found for this is -> ` sort data.txt | uniq -u `\
- sort , first sorts all the similar  liines next to each other and then uniq -u removes the repeating lines.
- password -> 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

# LEVEL 9 -> LEVEL 10

- The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

- i iinitally tried doing cat data.txt , but ah i coulndt understand whats going on in that , and then i did find out to get the human readable strings from txt or file , we can use the following command 
` strings data.txt ` , yes  strings command gave me human readble strings, but as question said  password is having ' = ' before it so my final command was -> ` strings data.txt | grep = `

- password -> FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

# LEVEL 10 ->LEVEL 11

- Here we have data.txt , but its in base64
- so i did cat data.txt and i got a code, but since in question it was gives that it is base64 , then we have to conver it to normal one which can be done easilty using -> ` base64 -d data.txt`
- where -d is decoding .

- password -> dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr


# LEVEL 11 -> LEVEL 12

- The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions !!

- As we know , we will have to rotate it here by 13 translations , in order to get the proper solution.

- So what we do is , use ` tr ` 

- command is as follows -> ` cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m' `

- Here `tr` is translate , and as we know we have to convert it to 13 characters, as we know A->N,soo from A , N is the 13th position and then , so after `tr`, we can see `A-Za-z` this means we want to translate the letter both upper and lowercasse , from A to Z and from a to z.

- Now , besides that we can see `N-ZA-Mn-za-m` , now the reason for this is , as we know 13 rotations , so A -> N , so we wrote 'N' in the beginning and then , we write N-ZA-M, because , for A , N is the 13 rotation and then , ZA is written because , For `tr` -> tr understands character ranges like A-Z, a-z, 0-9.But these ranges must go forward in ASCII order [ ascending order]. 

- Yes , so we Write N-ZA,means N to Z ,A to M, i cant directky write M , or some other way as it will loose its meaning , ie alphabetical order . simillary we did for lowecase.