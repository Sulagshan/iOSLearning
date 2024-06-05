##### In order to use setup multiple github accounts on one CLI

Use PAT from github account and HTTPs

Set credential.helper to cache 
> git config --global credential.helper 'cache --timeout=3600'

set user email and name. then store in credential helper
> git config user.email "user2@gmail.com"
> git config user.name "User Two"
> git config credential.helper store

Set remote 
> git remote set-url origin https://username2@github.com/username2/repository.git
