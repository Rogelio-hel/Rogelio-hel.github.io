---
layout: default
---

## Command Line Tools for Linguists (KIK-LG219)

This very intense course took place on the second period of the Autumn Semester. I was interested in improving my language technology skills, in view of its growing application to language research in general. What I discovered is that UNIX environment allows for very complex operations in all areas, and that automation of these processes can be of great help for the researcher.

The course favored a very practical approach, so that we could experiment each week with different features of the command line environment. I thought it was a humorous idea to state as one of the course's objectives "stay calm and google when things go wrong", but in the end this is really one of the most valuable skills learned; since the knowledge in this area is constantly changing and improving, and there is an infinity of issues that can go wrong, it only makes sense to learn to put the appropriate search items in google and to interpret them.

The material was mostly presented online, as videos or reading material, but the weekly lab sessions turned out to be essential to solve some of the problems that we run into.

#### Week 1: Introduction to Command Line Environments

In the fisrt week we got familiarized with some of the basic commands for Unix environments. As a mac user, I had it easy with the installation of the environment, since I just had to open the terminal.  
A very useful tool was the less command, which allows to see large texts in a readable manner. Emacs turned out to be rather complicated at the beginning; the reason is that I didn't understand how the meta key works and that it should come before the following key, and not simultaneously (as with the shift or alt keys, for example).

A couple of examples of useful commands learned this week:
```bash
mkdir week1
```
This command creates a directory called "week1"

```bash
echo "hello world!" > output.txt
```

This prints back the argument of the "echo" command, but it then redirects it to a text file, which is created if it doesn't already exist. In general, the ability to redirect the output with  >  proved to be very useful during the course.
```bash
ls directory_name | wc -l
```
A first approach to the use of pipes. The output of ls (list the contents of a given directory) is redirected to wc (word cound, with the -l flag to give only the line count of the output). This is a fast way to get the amount of files in a directory. The only output is just this number. 

#### Week 2: Navigating a UNIX System

#### Week 3: Basic Corpus Processing

#### Week 4: Advanced Corpus Processing

#### Week 5: Scripting and Configutation Files

#### Week 6: Installing and Running Programs

#### Week 7: Version Control
