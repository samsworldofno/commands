# Definitive Snippets Library

## Linux

### Generate SSH key pair

    $ ssh-keygen -t rsa -C "your_email@youremail.com"

### Add user to group

    $ usermod -G [GROUP_NAME] username
    
### Batch rename a load of files

    $ rename 's/\.jpeg/\.jpg/' *

## OSX / macOS

### Set time to UTC

    $ sudo ln -sf /usr/share/zoneinfo/UTC /etc/localtime

### Find CPU speed etc information

    $ sysctl -n machdep.cpu.brand_string

### Find how much memory is installed

    $ /usr/sbin/system_profiler SPHardwareDataType | grep Memory

### View a sitemap's contents

    $ curl -s https://shutl.com/sitemap.xml.gz | gunzip | xmllint --format -

### Extract sitemap from robots.txt and view contents

    $ curl -s https://shutl.com/robots.txt | sed -n 's/Sitemap: \(.*\).*/\1/p' | xargs -n1 curl -s | gunzip | xmllint --format -

### Add SSH key to keychain

    $ ssh-add -k [path-to-keychain]
    
... remembering to have the ssh config specifying the [use of keychain](https://unix.stackexchange.com/questions/140075/ssh-add-is-not-persistent-between-reboots)

    Host *
      UseKeychain yes

## Git

### Default push current branch to origin

    $ git config remote.origin.push HEAD

### Always rebase when pulling

    [branch "master"]
      rebase = true

### Showing log as a graph

    $ git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset' --abbrev-commit --date=relative

### Rename a branch

    $ git branch -m old_name new_name

### Delete a remote branch

    $ git push origin :branch_name

### Set up automatic rebase

    $ git config --global branch.autosetuprebase always

### Move a file between branches

    $ git show [branch]:path/to/file.rb > path/to/file.rb

### Delete branches merged on origin

    $ git branch --merged | grep -v "\*" | xargs -n 1 git branch -d

## MySQL

### Output data to a CSV


    SELECT a,b,a+b
      INTO OUTFILE '/tmp/result.txt'
        FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
        LINES TERMINATED BY '\n'
    FROM test_table;

### Grant all privileges to anonymous user

    CREATE USER ""@"localhost";
    GRANT ALL ON *.* TO ""@"localhost";
    
    
## Docker

### Delete old docker containers

Anything created before today:

    docker ps -a | grep 'days ago' | awk '{print $1}' | xargs docker rm 

Anything created more than a week ago:

    docker ps -a | grep 'weeks ago' | awk '{print $1}' | xargs docker rm 


## PostgreSQL

### Output data to a CSV

    Copy (
      -- ... your SQL here
    ) To "FILENAME" With CSV HEADER;

## Ruby

### Installing libv8 on REE on OSX Mountain Lion

    $ RUBYOPT=-rrubygems gem install libv8 -v '3.3.10.4'

### Remove rake gem from RVM global gemset

    $ rvm use @global && gem uninstall rake -v 0.9.0  
    $ rvm use @ && gem uninstall rake -v 0.9.0  
