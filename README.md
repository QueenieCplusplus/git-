# git

the git cli: $ git pull --rebase really helps me a lot.
and remember to add URL with port number to the remote branch,
otherwise the git warns you that you are directed..., and git push can't work out. 

<h1> Git Tool 

![git](https://www.perforce.com/sites/default/files/image/2020-01/image-blog-comparison-git-powered-wikis.jpg)

-----------------------------------------------------

# local side 

-----------------------------------------------------

(it is important to know the dir and local branch)

<h3> Git Routine:

## initialize git

  cd < under a dir >

  mkdir < dir name >

  cd < dir name >

  git init

## config (this file can be cd to ~/.gitconfig)

  git config --global user.name "PyQ" < this is the account name >

  git config --global user.email < this address is without "" double quote symbols >

  git config --global http.proxy, to make proxy valid

  git config --global --unset http.proxy, to make proxy unvalid

  git config --global credential.helper store, this step is to make .gitconfig file, otherwise the file will be in the path as
  .git/config, not .gitconfig

  git config --list, to check it out

## local branch 設定本機分支 

  git branch < to check branch name and choices >

  git checkout < branch name you choose >
  
## local branch delete 刪除本機分支

  git branch -a
  
     branchA_name
     
     branchB_name
     
  git checkout branchA_name
  
  git branch -d branchB_name
  
      Delete branch branchB_name ( commit flag number )

## remote branch 設定遠端 

  git remote -v, to check remote repo info, and check whether to do rebase or not

  git remote add origin < url with port number >

  git remote add < remote branch name > < new url with port number >
  
## remote branch delete 刪除遠端分支

  $git branch --remote
  
       origin/HEAD -> origin/master
  
       orign/deleteme
       
  Method 1
  
  $git push origin : <remote_branch_name>
  
  // it means to push null as local branch onto origin's repo's remote branch
       
  Method 2
  
  $git push origin --delete deleteme

       to < origin - url >
  
       - [deleted]  deleteme
  
## ssh, to avoid login to github or gitlab 

* 1. to check ssh key is in the local or not ---

  cd ~/.ssh

  if no such file, then

* 2. to generate a rsa key in local

  ssh-keygen -t rsa -C " < email address with double quote as string symbol > "

  [press enter], to save the rsa key file in specific path in local.

  then your id with rsa key will be save in /c/Users/you/.ssh/id_rsa

  and your pub key will be save in /c/Users/you/.ssh/id_rsa.pub.

  and the key fingerprint will be provided in bash at the same time.

  past the above mentioned pub key info in Github or Gitlab.

* 3. to check the ssh is working in local or not

  ssh -T <the tag name as email address without double quotes>

* 4. to make direct login to github or gitlab

  git remote -v, to check all remote repo, and check whether to do rebase or not.

  git remote add origin git@github.com:account/repo.git
  
  like this ->>> git remote add origin git@0.0.0.0:QC-109/qsdjangogirl.git
  
  port number may be 22 for ssh or 8080 for http req/res

  git remote add < remote name > < url > < : > < account name > < repo name > < .git >

* 5. to modify the remote (重設遠端)

  git remote set-url origin < url >

  git remote set-url < remote > < url >

![git flow](https://gitbook.tw/images/tw/gitflow/why-need-git-flow/flow.png)

## git pull 

  git 

  git pull --rebase (避免斷頭，記得確認遠端名稱與遠端分支)

  (before commit, pull at first step)

## commit 

  git add < readme >

  git commit

  git commit -m"your comment"

## go to vim

  i, to edit

  esc, to escape from editor

## if the env is windows

  ctrl x + ctrl c (另一作業系統如 Unix 家族免用)

## jump from vim

  :q

  :wq | :qw

## go to bash 

  git push < remote name > < local name >: < remote branch >

  git push -u origin master: master (對於冒號後的分支名稱非常重要!)

## if git conflict occurs 

  git push -f, this will overwrite the prepost commit forcely.

  then fighting with co-worker ...  > <  (避免爭吵，敬請慎用)

-----------------------------------------------------

# remote side

  (it is important to know the ssh, url with port number, and rebase)

-----------------------------------------------------

go to github or gitlab

register an account

create a repo

back to bash in local

  cd to specific dir which already got git init

  git branch to specific local branch

  git clone https://github/account/repo.git 

  git pull --rebase, to avoid local is un-headed 斷頭(如同沒父母的孤兒)

  git add 

  git commit

  git push < remote > < local > : < remote branch >

  git push remote master:icon

  git push -f origin master

![git conflict](https://dev.vividbreeze.com/wp-content/uploads/2018/03/gitBasicsBranchingMergeConflictCommitView-1-1024x531.jpg)

-----------------------------------------------------

# Problem Shooting

-----------------------------------------------------

  git reflog, to check local head

  git reset --hard HeadTag, to back to latest head in local

  git reset --hard HeadTag(as follwing numbers)

example: 
39119c9 (HEAD -> master) HEAD@{0}: checkout: moving from 09257aba0c901305a9fabf274f886dec81a631c9 to master

09257ab HEAD@{1}: commit: 0211(0)

305eac9 (origin/master) HEAD@{2}: pull --rebase: checkout 305eac973883a87f24e131f8c1bb74d09b657ab6

39119c9 (HEAD -> master) HEAD@{3}: commit: 0211(-1)

9253342 HEAD@{4}: commit: 0211 prework

172afb7 HEAD@{5}: rebase finished: returning to refs/heads/master

172afb7 HEAD@{6}: pull --rebase: 0211 prework

7d492b7 HEAD@{7}: pull --rebase: 0211 pretest for CICD

df94808 HEAD@{8}: pull --rebase: cicd test0

17a95fa HEAD@{9}: pull --rebase: checkout
17a95fa0cd46dc8b663146fbf48d5cc40efc7316

0b4c5d3 HEAD@{10}: commit: 0211 prework

6fa83e2 HEAD@{11}: commit: 0211 pretest for CICD

6d343f4 HEAD@{12}: commit (initial): cicd test0


  git diff| git status


example: 
On branch master
Your branch and 'origin/master' have diverged, 發散!!!
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

        deleted:    0211_Jenkin.py.py

        deleted:    0211_test_CICD.py
        
        deleted:    README.md

  git add & git commit, it can solve the unmerged problem

[master 622ed2e] with commit tag

-----------------------------------------------------

# Log of Headers in both the Local -> Remote (from 7ba48f1 to 47f9bad)

-----------------------------------------------------


 git log
 
 $ git log
 
    commit the_commit_flag_number_code  (HEAD -> local_branch_name, remote_url_name/remote_branch_name)
 

example: 
commit 47f9bade11f9ac2a2f04a1749ea142259b7443eb (HEAD -> master, origin/master)
Author: QC-109 <109009@concords.com.tw>
Date:   Tue Feb 11 16:20:44 2020 +0800

    add noSQL driver & object

commit 7ba48f1eb861af58df21ac30fc4bff0af82b1ff1
Author: QC-109 <109009@concords.com.tw>
Date:   Tue Feb 11 15:44:17 2020 +0800

    add DB

commit e2e40d98a0c2a617faf3d601c308cc322a235085
Author: QC-109 <109009@concords.com.tw>
Date:   Tue Feb 11 13:33:17 2020 +0800

    add image

commit de047fec9383ecbf48ba214f87fb55679f795b54
Author: QC-109 <109009@concords.com.tw>
Date:   Tue Feb 11 13:29:53 2020 +0800

    0211 add markdown


