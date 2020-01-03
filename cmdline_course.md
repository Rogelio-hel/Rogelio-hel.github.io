---
layout: default
---

## Command Line Tools for Linguists (KIK-LG219)

This very intense course took place on the second period of the Autumn Semester. I was interested in improving my language technology skills, in view of its growing application to language research in general. What I discovered is that UNIX environment allows for very complex operations in all areas, and that automation of these processes can be of great help for the researcher.

The course favored a very practical approach, so that we could experiment each week with different features of the command line environment. I thought it was a humorous idea to state as one of the course's objectives "stay calm and google when things go wrong", but in the end this is really one of the most valuable skills learned; since the knowledge in this area is constantly changing and improving, and there is an infinity of issues that can go wrong, it only makes sense to learn to put the appropriate search items in google and to interpret them.

The material was mostly presented online, as videos or reading material, but the weekly lab sessions turned out to be essential to solve some of the problems that we run into.

#### Week 1: Introduction to Command Line Environments

In the fisrt week we got familiarized with some of the basic commands for Unix environments. As a mac user, I had it easy with the installation of the environment, since I just had to open the terminal.  
A very useful tool this week was the **less** command, which allows to see large texts in a readable manner. Emacs turned out to be a rather complicated tool at the beginning; the reason is that I didn't understand how the meta key works and that it should come before the following key, and not simultaneously (as with the shift or alt keys, for example). After understanding this step it was very helpful for editing and writing text.

A couple of examples of useful commands learned this week:
```bash
mkdir week1
```
This command creates a directory called "week1"

```bash
echo "hello world!" > output.txt
```

First, this prints back the argument of the **echo** command, but it then redirects it to a text file called output.txt. It will be created if it doesn't already exist. In general, the ability to redirect the output with  >  proved to be very useful during the course, especially for saving the output of a command that is of interest.

#### Week 2: Navigating a UNIX System

In the second week we had a deeper look a the file organization system in UNIX. We also learned how to copy, move and remove files and directories. Most interesting was to see that mv is also used to rename files and directories. The **ls** command lists the contents of a given directory.
The **top** command was a revealing way to see all the processes that are taking place at a given moment.  
Finally, we connected with a remote server using the **ssh** command. I'm ashamed to confess that I had forgotten my password to the csc puhti server, but I managed to recover it on time.  
The example of code I would like to mention from this week includes the first use I made of the pipe character, and is taken from the reading material:
```bash
ls directory_name | wc -l
```
This uses the **ls** command to list the contents of a directory. But it then passes the output ("pipes" it) to the following command. This week saw also then our first approach to the use of pipes. The output of ls (list the contents of a given directory) is redirected to wc (word cound, with the -l flag to give only the line count of the output). This is a fast way to get the amount of files in a directory. The only printed output is just this number. 

We saw a very informative interview with Tatu Ylönen, creator of the ssh commmand for securely connecting and working on remote server. Here Tatu's picture:

![Tatu Ylonen](https://is.mediadelivery.fi/img/1440/860ef1a8e18647fc8650858820ad3eb9.jpg){:height="50%" width="50%"}

#### Week 3: Basic Corpus Processing

In the third week we learned about commands used for text processing. It took me a while to understand all the conversions necessary to process text files in Unix environment. One has to do with character encoding, which is carried out with the **iconv** command. Another one is done with **dos2unix**, a command that changes the Windows type of line ending for the Unix type in a text file, so as to avoid extra characters at the end of each line. Such characters might appear as **^M**. The **tr** command, used to transform characters and replace them with something else, seems to me a very useful text processing tool, for such tasks as turning upper case letters into lower case, for example.      
With the aid of a video we could generate an alphabetized word list of all the words in the Finnish book _Katinka Rabe_; each word appears only once in the list and the list is alphabetically ordered with the **sort** command. We also tested our knowledge of regular expressions by searching for two consecutive words in the inessive case using the **egrep** command. A difficulty with **grep** and **egrep** is that the printed output is the whole line that contains the matching expression; this can be visually challenging, but the **--color** flag was helpful to see the highlighted expressions.  
Finally, we had a look at formatted text files, such as **CSV** (comma-separated values) used to store tabular data by following a strict text format.  
This command was used to sort each line alphabetically, it has the **-f** flag for ignoring case.
```bash
sort -f text_file_in_finnish.txt
```

The following command I've chosen as an example has a regular expression as its argument:
```bash
egrep '\b[a-zåäö]*ss[aä] [a-zåäö]*ss[aä]\b' text_file_in_finnish.txt > inessives.txt
```
The regular expression matches two consecutive words ending in **-ssa** or **-ssä**, almost certainly a case of an adjective and a noun in the inessive case in Finnish. It will search in the finnish text that is given as argument. The range inside the square bracket matches any sequence of letters from the defined range; the **\*** charachter implies that there can be an indefinite amount of such characters, until the space comes. The second square bracket means that either **a** or **ä** are matched. Finally, the **\b** means a word boundary, making sure that the sequence is an isolated word that could be at the beginning, middle or end of a line. Finally, the output is redirected to the text file inessives.txt and saved in it.


#### Week 4: Advanced Corpus Processing

This week we had a look at more text processing commands and how they can be concatenated through _pipelines_ that pass the output of a command to the next one; we had briefly seen an example in week 2.  
But this week's star was, beyond doubt, the **sed** command. It was laborious to get used to the very precise syntax, but in the end it proved a useful and powerful tool. The **sed** command, short for _stream editor_, can quickly edit files without opening them. We worked mostly with the syntax for substituting, and with the **-E** flag for _extended regular expressions_:
```bash
sed -nE 's/pattern1/pattern2/gp' file.txt
```

The **s** right before the patterns means that _pattern1_ will be replaced by _pattern2_ in file.txt. The patterns must be written between slashes, as shown. The **-n** flag will supress the default printing of every line of the file, and the added **p** in the end will instead print every matching line. The **g** stands for _global_, meaning that the substitution will be carried out for each matching pattern in the line, thus overriding the default action of substituting only the first matching pattern in every line.  
The following command, instead, was used to delete a matching pattern, with the final **d** indicating the delete action:
```bash
sed -nE '/pattern/d' file.txt
```

Something important to notice is that the **sed** command uses regular expressions. This makes the use of the command something very tricky, since regular expressions also have a very precise syntax.  
Besides, we created frequency lists of the words used in a given text file, using the commands **tr**, **sort** and **uniq** with the flag **-c**, to get the count of each word occurrence. With **sed**, **tr** and **grep** we also created a file which has only one sentence per line.

#### Week 5: Scripting and Configutation Files

This week's theme turned out to be very motivating. All the commands can be put together in a _script_, an executable text file that contains a sequence of commands. It functions somehow like the pipeline of commands, but it can be executed as a single command itself in different contexts and with different arguments. This makes complex tasks simpler and manageable. The scripts can contain also so called _if statements_, in which some commands are executed only if certain conditions are met. We had an introduction to the use of variables in scripts as well. Some interesting examples of variables are **$#**, which corresponds to the number of parameters introduced for the execution of the script, and **$?**, which tells whether the preceding command has been successful ($?=0) or not ($?=1). Also, each of the parameters can be used in the script by referring to them with the variables **$1** - **$9**.  
An example of an _if statement_:
```bash
if [ $# -eq 1 ]
then
  echo $1
else
  echo Too many parameters
fi
```
This means that if the number of arguments is equal to one, then the script will print back, or **echo** that argument. Any other number or arguments will result in the error message after the **else** in the script. The statement ends with _fi_, reversal of _if_ just to indicate that the condition is closed here.  
The reading material also included the so called _case statements_ which make the numbering of different conditions and following command sequences for each condition easier.  
A problem I encountered is that **if** and **case** statements don't support regular expressions. Instead, _case statements_ expect the much simpler meanings of **\*** and **?** as wildcard characters, which is its meaning in bash. I tried to solve question 10 from the weekly quiz by using _case statements_, but I was trying to put **\*** as signal that the letter character can be repeated many times, as if it was a regular expression. After solving this in another way, I understood that it would be useful to know when regular expressions will be supported. And also to know how some characters have a different meaning outside regular expressions, maybe the following table will be of use for this:  

|Character|As regular expression|In bash command line|
|:---:|:---:|:---:|
|**\***|Zero or more occurrences of the preceding character|Zero or more of any character|
|**?**|Zero or one occurrence of the preceding character|Any character once|
|**.**|Any character once|No special meaning|
|**+**|One or more occurrences of the preceding character|No special meaning|
|(a**\|**b) i.e. just the _pipe character_|Alternative matching groups|Transfer output to the following command|
|**$**|Anchor expression at the end of the line|Begin recalling of the variable that follows|

  
This week we also had an introduction to environmental variables and to the _bash configuration file_. As a Mac user, this was for me **~/.bash_profile**. Thanks to this my prompt has now some color and leaves some space between each prompt as visual aid.


#### Week 6: Installing and Running Programs

This week we learned about installing software as the root user, who has special permissions to alter the system and install software. The relevant commands were **su**, for switching user, and **sudo** for a temporary change of user. We also learned about software dependencies and why then some versions of the same software can have different dependencies and be incompatible.  
Installing the _python library_ **NLTK** seemed a gentle introduction to python and its use in linguistics. 
But most interesting for me in this week was building a _make file_, which allows for automation of simple or complex tasks. These tasks can then be carried out on large amounts of files or input data. An element in the _make file_ is a  **make rule**, which has roughly the following syntax:  
```bash
target: dependencies
    commands parameters
```
This **make rule** will execute the ```commands``` with the given ```parameters``` using the ```dependencies``` when required. 

The correct use of the **%** sign in a **makefile** was very tricky for me, since it is about going through all possible values of a variable that has been previously defined. Somehow, looking at the variable values elsewhere in the document and then visualizing those values in the **make rule** that had a **%**, just seemed confusing at the beginning. Let's see a concrete example:
```bash
all.no_md.txt: $(BOOKS:%=%.no_md.txt)
    cat $^ > $@
```
This make rule is not identical with the one we solved for homework, but the idea is the same: it will go through each value of the previously defined variable **BOOKS** and assign each one to a file called **value.no_md.txt**. Each of these files will then be parameters for the **cat** command that follows. All possible parameters are referred to with **$^** and the output, a concatenation of all the ```no_md.txt``` files, is then redirected to **$@**, that is, to the target of this make rule, a file called ```all.no_md.txt```.  
With some practice, this syntax became more familiar and the visualization of variables a more simple matter.

#### Week 7: Version Control

On week 7 and the following final project we got to work on a remote repository, with the purpose of following and controlling changes done to a larger project. This allows for independent work on specific parts or _branches_ of the project, and for restoration of the project to previous states in case some part does not work as expected. The work in progress can then be _pushed_ to a remote location, both to save the project in a secure place, and to share it with others that might be working on the same project. 
For this we learned about the **git** commands and used **github** as a repository. The **git** related commands are not difficult in the end, but there are many of them and a large amount of practice is necessary to keep the project in healthy shape. Here is a list of the **git** commands I have been using both on this project and in the shorter one we did as homework on week 7:

* ```git init```

 It initializes a new repository

* ```git clone <repository url>``` . It creates a local copy of an existing remote repository. Useful to
  * start working in a local environment
  * keep track of changes locally made to the project
  * restore previous versions locally
  * finally, to upload or _push_ new versions of the work to the remote repository

* ```git remote add <remote_name> <remote_repository_url>```

 It maps the remote repository to the local one called remote_name 

* ```git add <file_name>```

 It adds the file to the _staging area_, which contains all files in which we are tracking changes.

* ```git commit -m "commit message"```

 It _commits_ to the changes made, that is, the changes are accepted as final changes. The **-m** flag allows to include a message so that it will be easy to find this particular stage of the project when searching for it.

* ```git push```

 It uploads or _pushes_ the local repository to the remote one.
* ```git pull```

 It downloads, so to speak, or _pulls_ the remote repository to the local one.

* ```git branch <new_name>```

 It creates a new branch of work for a part of the project, called **new_name**.
* ```git checkout <branch_name>```

 It switches to **branch_name** as working branch
* ```git branch -a```

 It lists all existing branches, coloring the active one. The remote ones are printed in a different color as well.
* ```git branch -d <branch_name>```

 It deletes the branch called branch_name.
* ```git merge <branch_name>```

 It merges the branch with the ```master branch```
* ```git diff <file_name>```

 It lists the uncommited changes
* ```git status```

 It displays files that have changed, but the changes are not commited yet, and those which have been commited or staged.

 
That was quite a long list, and it's just a fraction of all the existing **git** commands.  
Luckily, I didn't have to use ```git restore``` up to now, to undo any commitments. Still, the whole sense of version control is summarized in the following image, which tells what should be done when it seems that everything will be lost in a moment:
![Github experience](https://img.devrant.com/devrant/rant/r_1424928_uns5D.jpg){:height="50%" width="50%"}

At least the changes made to the project will be safe in a remote repository after the first two items are executed!


#### **Thanks for the course!**
