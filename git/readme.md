In git there are two types of repos:
public
private

public repos anyone can clone

private repos you need ssh keys to clone



to create ssh keys for git repo you need terminal access; 
you can download mobaxterm or use azure cloud terminal or any other machine where linux is installed or mac os
in case you have created a ec2 instance then you will have a .pem key;
you need to download puttykeygen to convert the .pem key to .ppk key


ssh-keygen create



take the public key: id_rsa.pub file and paste contents in github -> settings -> deploy keys; you need to be git admin of that repo
these keys cannot be reused for any other repo with the github account

id_rsa private key is stored in the home directory of the user in .ssh folder


you can also create a alias file for which ssh private key to be used for which repo in .ssh folder with file called config
template of the file will be as below:

host
key
alias


git clone https

git clone ssh

once the repo is cloned then a folder named as <repo name> is available in the current directory
in case you want to clone the repo into a directoy with different name from repo then:
git clone .... <new folder name>

by default the master branch is cloned when git clone happens;
in case you want to clone a specific branch then
git clone .... -b <branch name>

if a specific branch is cloned then later you can checkout another branch as required

git branch


git checkout -b <branchname from git branches>


git status


git add <name appearing in git status>
git add .

git commit -m "added | updated | deleted  <filename> to <message>"


git remote -v

git remote add origin <url of the origin from where repo is clone on local>


git push

git push <location as per git remote>

you can block persons to push to master

you can lock the branches so that no one can pull or push to these;
github -> settings -> lock ??

you can 
