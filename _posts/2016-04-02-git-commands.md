---
layout: post
title:  "Git Commands"
date:   2016-04-02
excerpt: "What is git and github?"
project: true
tag:
- git
- github
- blog
- about
- commands
- shell
- bash
---

{% include toc.html %}
    
![Logo]({{ site.url }}/{{ site.picture }}){: .selfie}
    
<center>This doc will try to show variaty of commands on the git service, and try explaining them. </center>
    
### What?

* How Git works and using it effectively to store the history of the changes you make
* How to use Github to collaborate effectively with a team if it is a company or a open source project
* Push, pull, fork and many other docs coming up soon! Now I'm just testing the blog
        
## Installation
**If you want to see how to install git click the button below.**     

[Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git){: .btn}
 
## Git basic configuration        

This is focused on global configuration. There is also local configuration.

{% highlight text %}
####Git, configure your system correctly
git config --global user.name "Zukenberg Tyson"     // config for your name
git config --global user.email                      // put your desired email in there
git config --global color.ui true // colors !important // helps with more recognizble colors in the console. for warnings and stuff.
1.4.git config --global core.autocrlf true // true for windows // `input` for macs and linux // and what it does is makes show clear rows in the console.
5.//custom git things// `git config --global alias.s "status -s"` // ===git s=== <-- saves some custom commands like checking the status with only `git s` command 
1.5.1. git config --global alias.lg "log --oneline --all --graph --decorate"  <--custom check current branch and thingZ,//
6.cat ~/.gitconfig              // soon on Windows 10! also "vi" working // shows how your git is cofigured 
/-------------//-----####333--------------#
2.1. git status
2.2. git init web1 <-- new repository
cd web1 
git status <- branch showing
2.5.touch index.html index.css bab.html<== ?no Windows command .. //mkdir?-not the same// I'll soon update this file
3.git add . <-- adds all into staging area 
4.git commit -m "Added home page"
6.git log <-- looks at history
git log --oneline <-- look easy at the commits on ONE line with only some info shown	
git log --oneline --decorate ,което е равно на git lg from above  1.5.1
/!/--------@##############################-----\\\\\\|\\\////##########==--//--
git push -u origin master
////////////----------------------------/////////!/
========================================================================
{% endhighlight %}   

---

## Git rename, delete, .gitignore
{% highlight text %}
####Not so sure about these commands soon updating so skip if u want
mkdir web2
cd web2 
touch index.htm main.css
ls
git init  <-- making the directory a git reposidory // git status <-to check
3.1.0. rm index.html
1.rm main.css           // removes main.css from staging area
2.git mv index.html home.htm <-  // renames index.html to home.html 
git commit -m "Renamed home page to follow corporate guidelines"
3.mv index.html home.htm  git add -A <-- not so sure !careful
4.git rm contact.html // deletes the file
git commit -m "Deleted contact us page" git add -A 
{% endhighlight %} 

{% highlight yaml %}
In .gitignore to ignore a folder or different
kind of files you put "/" in different places


/node_modules  <-- these files will be ignored since "/" its at the start
examplefolder/ <-- this should ignore folder 

.gitignore patterns
Patterns inside the .gitignore file are matched from the root directory 
of the git repository. Patterns are comprised of a wildcard character *, 
to match any character, and literal characters to match the exact phrase.

A typical example of using a .gitignore file would be
to exclude all files ending in .log. The below
pattern would be added to the .gitignore file

*.log
Or, as with something like log4j,
your log files may include numbers at the end.
This pattern will exclude any file names
that contain .log.

*.log*
Another use is to exclude all files in a specific path,
such as the application build directory. This will ignore
the Build directory and everything within it.

/Build/*
Single repository .gitignore
Add your patterns to the below file to add exclusions to affect only
a singe git repository.
You must make sure you have changed to the root directory of your
repository, or include it in the file path.

vi /path/to/repository/.git/info/exclude
Global .gitignore
You must run a git config command to enable .gitignore 
to work across all local repositories. 
You can edit the ~/.gitignore path if required.

git config --global core.excludesfile ~/.gitignore
Once enabled, edit the
~/.gitignore file and add patterns which will affect
the next git add command.

vi ~/.gitignore
For example, you may add a global gitignore entry for .bak files.
Add the following line to you global gitignore file:

*.bak
 {% endhighlight %}


## Git branches
{% highlight text %}
////////////////////////////////////////===================#######3//////////////////////
//---Branches__------------------------------------------------

1.0. git branch <-- Shows all exisiting branches  // *master 
2.0. git branch search <-- Creates a branch named "search" // *master search
3.0. git checkout search <-- Switches branch to the "search" branch // master *search 
-----------# Now you can commit to the search branch  --!/  
git checkout master 
4.0. git merge search <-- Takes the work that we done on the search branch and brings it to master branch
5.0. git branch -d search <-- Lower CASE D Deletes the branch "search" 
6.0. git checkout -b categories <-- Creates a new branch named "categories" and check it out // *categories master // almost all proffessionals would use this
git commit -m "Added categories page"
7.0. git checkout -b products 	//git branches merge example / Fast-forward
	touch products.html <- creates a file called products.html
	git add . <- adds it to the staging area
	git commit -m "Added products page" <- commits it // type-> history <- to see what have u done
	git checkout master //switches to *master branch
	git merge products  // by default is gonna do a Fast-forward merge
	git lg // git log look and it shows that is added a commit to the master branch from the products change as that it was a part from the master 
	git branch -d products // to delete products branch

The reason we were able to do a Fast-forward merge, was because there was no difference in history. Where u dont have many branches before that or something. 
/////////////////////////////---------//
No fast forward merge, but a recursive merge / merges
so now master has a commit that categories does not have,
 $git branch  
 categories
 *master
 $git merge categories / opens a file where you can explain your commit or on windows just adds it automaticaly, you can do it with default message// and the commit is done by recursive merge where you commited it from master to categories
//.------------.----------------------/----------------// So this was basic commands and tactics just to understand what is happening :D//-
$git branch -d categories //delete
$git checkout -b my_account //created and switched to my_account 
$touch account.html
$git add .
$git commit -m "Added account page" 
$git checkout master
$git merge --no-ff my_account // where --no-ff means no fast forward and the reason behind this is if we even delete the my_account branch it will still be showned it the log and the history from where that commitment was comming from, which is usefull peace of extra information to have
/////------/////////////////////////////
####What happens when good merges gone bad 
1.If you make totally different changes to a file on different branches you wont be able to merge them 
	- git status // is your friend and will show you what you need to do 
	- All you need to resove a merge conflict in Git is a text editor
		-delete some conflicts and stuff to show what exactly you want to commit to git. and then just git add .<- or add only the file 

$git checkout checkout_page
$touch git checkout.html //creates the file
$git add . 
$git commit - m "Added checkout page"
vi home.html // vi or other editor  and link to checkoutpage
$git commit -am "Added link to checkout page"
$git checkout master
$cat home.html 
$git checkout -b add_home_page_links  //:D Hope someone understands what is happening these are just examples to try to show the Diff
$vi home.htm
$git commit -m "Added new links to the home page"
$git branch master // switches to master branch
$git merge --no-ff add add_home_page_links //accept the default commit message 
$git branch -d add_home_page_links // deletes  the add_home_age_links branch
And its all commited to the *master branch and deleted the other branch 

#######Git Diff allows you to see the differences between almost anything 
1.If you want to learn almost everything about a Git command you should start with "$git help", so:
$git help diff
///////#########GO:
$vi home.html // and change something in the file 
$git s
	home.htm
$git diff  <---------------will show you what exactly were the changes to that file 
2.If you want to see the STAGING Changes for a file 
$git diff --staged 
3.And if you want to see the difference between your working directory and the last commit you made. 
$git diff HEAD 
-So it will show you Staged and Unstaged changes  

###Idea of git Rebasing. 
This is totally different from a git rebasing -i, and as the two things may be similar in a way they are two totally different things and should be considered that way. 
- Should I rebase or merge?
- Merge.. The question is should you rebase before you merge.


################3######################################----####

{% endhighlight %} 


#### The idea of Rebasing.

`Example:`

{% highlight yaml %}
$git checkout -b feature1
$touch feature1.html
$git add .
$git commit -m "Added feature1"
$git checkout master
$git checkout -b feature2
$touch feature2.html .. add .. commit -m "Add feature2"
$git checkout master
$git merge --no-ff feature1 //making a recursive merge
$git branch -d feature1 //delete feature1
$git lg //log to look out where we are now  and if you have 20 developers it's kind of hard to look at 
$git checkout feature2
$git rebase master   // rebases master HEAD to another place :D ..
Where you can work on feature2 on your own and merge it after you are done. And this allows you to build all your integration testing there and so if it breaks there it wont break the main production branch.
After you test it you can merge it to your master branch.
$git checkout master
$git merge --no-ff feature2 
$git lg // and now we can tell the story 
{% endhighlight %}

## Filename too long fix
{% highlight yaml %}
Windows does not properly support files and directories longer than 260 characters. 
Solution: 
git config --system core.longpaths true
{% endhighlight %}

## About GitHub and Git
     
GitHub is a website where you can upload a copy of your Git repository. It is a Git repository hosting service, which offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features. Unlike Git, which is strictly a command-line tool, GitHub provides a web-based graphical interface and desktop as well as mobile integration. It also provides access control and several collaboration features such as wikis, task management, bug tracking and other features that can be helpful for projects. It allows you to collaborate with other people on a project. It does that by providing a centralized location to share the repository, a web-based interface to view it, and features like forking, pull requests distributed revision control, issues, and wikis. 

## Github for noobs youtube playlist

[Youtube](https://www.youtube.com/watch?v=1h9_cB9mPT8&list=PLqGj3iMvMa4LFz8DZ0t-89twnelpT4Ilw){: .btn}