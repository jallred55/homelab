steps to follow to create a new user in linux:

to create the user (-m creates the home folder for the user)
$ sudo useradd -m [username]

to see the user id number
$ sudo id [username]

to change the password for the user
$ sudo passwd [username]

to add user to group:
$ usermod -aG sudo [username]

