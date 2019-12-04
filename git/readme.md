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

=======================


install git on windows
git credentials manager on windows

dev.azure.com/lalitduggal
create project: demo01; private; advanced -> git; agile)
select project
go to repos
generate git credentials
username: lalitduggal
password: zko7lh7ebtwrqhtjgeudl67bjp2n36zxgdifpnluxa5lz74hmj3a (copy this)


cmd
md demo01repo
cd demo01repo
copy all the project files to this directory
-- echo "one" > one.txt


-- del \f demo01repo
-- rd /s /q test02

-- if exist d:\testclonedest\ rmdir /s /q d:\testclonedest\

--git clone https://lalitduggal@dev.azure.com/lalitduggal/demo01/_git/demo01



git init
git status
git add .
git status
git commit -m "First commit"
git remote -v
git remote add origin https://lalitduggal@dev.azure.com/lalitduggal/demo01/_git/demo01
git remote -v


git push -u origin --all
-- git credentials manager on windows will pop up; then enter below which was generated above
-- lalitduggal
-- zko7lh7ebtwrqhtjgeudl67bjp2n36zxgdifpnluxa5lz74hmj3a

-- set username and email for git
-- set color for git
-- git config

in project settings -> repos -> select repo name ... -> rename repo
repos -> navigate to repo

git remote -v
git remote remove origin

git remote add origin https://lalitduggal@dev.azure.com/lalitduggal/demo01/_git/demo01repo
git push --set-upstream origin master

project setings -> agent pool -> Build01_Pool (new; donot grant permission to all pipelines) -> new agent -. windows (x64 download)

Open powershell in administrator mode

cd c:\

PS C:\> mkdir agent ; cd agent

PS C:\agent> Add-Type -AssemblyName System.IO.Compression.FileSystem ; [System.IO.Compression.ZipFile]::ExtractToDirectory("$HOME\Downloads\vsts-agent-win-x64-2.160.1.zip", "$PWD")

PS C:\agent> .\config.cmd

server URL: https://dev.azure.com/lalitduggal
PAT
project menu -> Personal access token -> Build01_Pool_PAT (30 days; full access): uv6czxpobdsy2r6fbrtqdxri76pujckmkzqlj6zbybrhms2yknaa
Agent Pool name: Build01_Pool
Agent name: lalit_personal_laptop
work folder: _work
run agent as service: y
user account: NT AUTHORITY\NETWORK SERVICE

windows services you will find a running service with name: Azure Pipelines Agent (lalitduggal.Build01_Pool.lalit_personal_laptop)
also check the agent status in project settings -> agent pools -> agents (it should be online and enabled)

pipelines-> build -> use classic editor -> azure repo (project; repo; branch) -> empty pipeline -> click agent (display name: lalit laptop; Build01_Pool as agent pool; allow scripts to access the OAuth token) -> select pipeline and select agent pool: Build01_Pool -> save and run -> comment: my first build; 

_work directory in your agent directory -> \s\ you will find all the checked out code


archive: 
$(Build.BinariesDirectory) is b in _work
$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip is a in _work
s in _work is the source code checkout directory
$(Build.BuildId) where buildId is the build id of the pipeline


$(System.ArtifactsDirectory)

build number format: https://docs.microsoft.com/en-us/azure/devops/pipelines/process/run-number?view=azure-devops&tabs=yaml


$(Pipeline.Workspace)


pipelines -> release -> empty job ->
source type: build
source (build pipeline): demo01-CI
default version: Latest
Source alias: _demo01-CI

artifact -> continous deployment trigger -> enabled 
stage 1: Job tasks: -> agent job -> agent pool: Build01_Pool





to get notification for release success and failure: project settings -> notification -> new subscription -> release -> select appropriate


download build artifacts: _work\r1\a\_demo01-CI\<name of artifact drop or default is Job1>
a: is where artifact is zipped using <buildnumber>.zip
b
s: is source code which was checked out
TestResults: 



build pipeline:
get sources
agent:
	copy files to ...
	archive ...
	publish pipeline artifact

bash
batch script
command line
copy files
copy files over ssh
delete files



release pipeline:
download build artifacts
command line script
extract files

download artifacts from file share
download pipeline artifacts
download a secure file
download package (from azure artifact)

powershell
powershell on target machine
publish build artifacts

ssh

query hs to be shared to appear in dashboard (rename -> move the query to shared folder)


===============
import.giithub.com => github imported ONLY for PUBLIC SVN

empty folders are not migrated so create a sample file in these folders and then delete after migration
git does not allow to push file > 100MB in size

java -jar ~/svn-migration-scrips.jar authors <SVN URL> authors.txt
git svn clone --stdlayout --authors-file=authors.txt <svn URL>

diff between fetch and pull in git:

-------------------------------------

git fetch => is usually for getting a branch from origin; origin/<branchname>: you need to checkout to current branch where you need this info and then: git merge <from origin/master into the current branch>

git pull => is for getting the code from origin AND merging the code in local

As a good practise: git pull is a MUST before git push origin <branch name>

PULL = FETCH + MERGE

git branch
git branch -r (remote tracking branch)

diff between git merge and git rebase:
----------------------------
git checkout <branch where the new code from new branch will be merged>
git merge <name of the branch which needs to be merged>

git merge --squash <name of the branch which needs to be merged>
git commit -m "merge master and feature branch" => this will be one consolidated commit for all changes in master and feature


what is diff between tags and branches:
-----------------------------
git checkout <feature branch>
git rebase <from master>

git checkout master
git rebase <from feature>

DONOT use rebase in public repo and when other repos are involved

--------------
git stash
git stash apply
git stash list
git stash (last stash will be applied ie: 0 latest one)
git stash <number from git stash list; latest is on top with 0 >
git stash push -m "messag for stash"
git stash drop 2
git stash pop 2 <this will be applied and dropped from stash>
git stash clear <to clear all the stash>
===============

git reset --hard <commitid> (CAREFUL CANNOT BE REDONE)

revert unstaged changes: ie git add no performed: git checkout -- .


create a branch from commit: git checkout <commitid>

create a new branch: git checkout -b <new branch name>
for going to master branch shorter way is: git master

git branch -D <branch to be deleted; you should NOT be in the branch which is to be deleted>

git merge <branch to merge from>
if there is conflict: resolve the conflict -> git add . -> git commit -m "resolved merge conflict" => this will merge into the branch ie; master or whereever you are

================
git checkout <branch name where you want to create a tag>
git tag <name of tag>
git tag -a <tagname> -m "message for the tag" => to create annoted tag
git tag => to get list of all tags

git show <tagname> => to get details of a particular tag
git tag -l "someword*" => to use wildcard

tags appear in the release tab in github

git push origin <tagname to be pushed>

git push origin --tags OR git push --tags => to push all the tags

to delete tag from local:
-------------------------
git tag -d <tagname to be deleted>
git tag --delete <tag name to be deleted>
git tag -d <tag name> <tag name> <tag name>


to delete tag from remote:
--------------------------
git push origin -d <tag name to be deleted from remote>
git push origin --delete <tag name to be deleted from remote>
git push origin -d <tag name> <tag name> <tag name>

git checkout -b <branch name to be created> <tag name which needs be in that branch>

tag a particular commit in past => git tag <tag name to be created> <commit id>
git push --tags => will push the tags to remote repository

git lgo


====================

git config core.sshCommand "ssh -i ~\.ssh\id_rsa -F /dev/null"

OR

mkdir ~/.ssh
vi config

Host devopskey1
User git
HostName ssh.dev.azure.com
IdentityFile ~/.ssh/id_rsa

==============================
