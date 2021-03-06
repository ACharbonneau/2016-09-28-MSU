---
layout: lesson
root: .
title: Intro to Organization
minutes: 20
---

[Home](https://acharbonneau.github.io/2016-09-28-MSU/)

[Back: SRA runtables](https://acharbonneau.github.io/2016-09-28-MSU/05-examining-sra-runtable.html)

# Getting your project started

Project organization is one of the most important parts of a sequencing project, but is often overlooked in the excitement to get a first look at new data. While it's best to get yourself organized before you begin analysis,
it's never too late to start.

You should approach your sequencing project in a very similar way to how you do a biological experiment, and ideally, begins with experimental design. We're going to assume that you've already designed a beautiful sequencing experiment
to address your biological question, collected appropriate samples, and that you have enough statistical power. For all of those steps, collecting specimens, extracting DNA, prepping your samples, you've likely kept a lab notebook that details how and why you did each step, but documentation doesn't stop at the sequencer!

Every computational analysis you do is going to spawn many files, and inevitability, you'll
want to run some of those analysis again. Genomics projects can quickly accumulates hundreds of files across tens of folders. Do you remember what PCR conditions you used to create your sequencing library? Probably not. Similarly, you probably won't
remember whether your best alignment results were in Analysis1, AnalysisRedone, or AnalysisRedone2; or which quality cutoff
you used.

Luckily, recording your computational experiments is even easier than recording lab data. Copy/Paste will become your best friend, sensible file names will make your analysis traversable by you and your collaborators, and writing the methods section for your next paper will be a breeze. Let's look at the best practices for documenting your genomics project.

Your future self will thank you.

## Exercise

In this exercise we will setup a filesystem for the project we will be using over the next few days. We will also introduce you to some helpful shell commands/programs/tools:

* ``mkdir``
* ``history``
* ``tail``
* ``|``
* ``nano``
* ``>>``

#### A. Create a file system for a project

We will start by create a directory that we can use for the rest of the workshop:

First, make sure that you are in your home directory:

```bash
$ pwd
/mnt/home/charbo24
# Yours should say: '/mnt/home/<yourID>'
```

Then, make a new directory to hold all of our work for this project:

```bash
$ mkdir dc_workshop
```

**Tip:** Remember, when we give a command, rather than copying and pasting, just type it out. Also the '$' indicates we are at the command prompt, do not include that in your command.

**Tip** If you were not in your home directory, the easiest way to get there is to enter the command ``cd`` which always returns you to home.

Next, try making the following directories using the ``mkdir`` command


* dc_workshop/docs
* dc_workshop/data
* dc_workshop/results


Verify that you have created the directories;

```bash
$ ls -R dc_workshop
```

if you have created these directories, you should get the following output from that command:

```bash
dc_workshop/:
data  docs  results

dc_workshop/data:

dc_workshop/docs:

dc_workshop/results:
```

#### B. Move your data here

Currently, the data is read-only. We can check this by doing an `ls`

```bash
$ ls -l /mnt/research/common-data/workshops/genomics/dc_sample_data/
```
Notice that we didn't have to actually go to that directory in order to see the contents:

```bash
$ pwd
```

Your ls should have given you these results:

```bash
drwxr-sr-- 2 billspat common-data 3 Jul 30  2015 sra_metadata
drwxr-sr-x 2 billspat common-data 4 Jul 30  2015 untrimmed_fastq
```

There are 10 characters at the beginning of each line, and they tell you about permissions, that is, what users are allowed to do with each file.
The 'd' at the beginning tells us that each of these is a directory, then each set of three characters after that tells us abou the privileges for each class of user, in order:

1. Owner (characters 2-4)
2. Group (5-7)
3. Users (8-10)

The three characters each tell us about a different action each user might use, in order:

1. Read
2. Write
3. Execute

For these two directories, the owner, that is, the person that uploaded them, can read, write and execute (run programs that are in) in these folders.
People in groups with special access to these directories can read, but not write, and have special execute privileges.
Everyone else (that's us!) can ONLY read `sra_metadata`, but we can also execute any code in `untrimmed_fastq`

This is how you want to keep your important data, like raw sequencing files. Because we ONLY have read access, we can't accidentally delete or overwrite these files.
If we want to do anything with them other than look at them, we'll have to make a copy to use.

```bash
$ cd dc_workshop/data
$ cp -r  /mnt/research/common-data/workshops/genomics/dc_sample_data/* .
```

This recursively copies the `dc_sample_data` folder to whatever folder you are currently in.

Now, we can give these more permissions:

```bash
$ chmod -R 777 *
$ ls -l
```


#### C. Document your activity on the project

The *history* command is a convenient way to document the all the commands you have used while analyzing and manipulating your project. Let's document the work we have done to create these folders.

1. View the commands that you have used so far during this session using ``history``:

```bash
$ history
```

The history likely contains many more commands that you have used just for these projects. Let's view the last several commands so that focus on just what we need for the project.

2. View the last n lines of your history (where n = approximately the last few lines you think relevant - for our example we will use the last 7:

```bash
$ history | tail -n7
```

As you may remember from the shell lesson, the pipe ``|`` sends the output of history to the next program, in this case, tail. We have used the -n option to give the last 7 lines.

3. Using your knowledge of the shell use the append redirect ``>>`` to create a file called **dc_workshop_log_XXXX_XX_XX.txt** (Use the four-digit year, two-digit month, and two digit day, e.g. dc_workshop_log_2015_07_30.txt)

4. You may have noticed that your history may contain the ``history`` command itself. To remove this redundancy from our log, lets use the ``nano`` text editor to fix the file:

```bash
$ nano dc_workshop_log
```

From the nano screen, you should be able to use your cursor to navigate, type, and delete any redundant lines.

5. Add a dateline and comment to the line where you have created the directory e.g. <br>

```
# 2015_07_30
```

<br>

```

# Created sample directories for the Data Carpentry workshop
```

6. Next, remove any lines of the history that are not relevant. Just navigate to those lines and use your delete key.

7. Close nano by hitting 'Control' and the 'X' key at the same time; notice in nano this is abbreviated '\^X'; nano will ask if you want to save; hit 'Y' for yes. When prompted for the 'File Name to Write' we can hit 'Enter' to keep the same name and save.

8. Now that you have created the file, move the file to 'dc_workshop/docs' using the ``mv`` command.


#### C. Intro to Markdown

As you start to build your notebook, there is an easy way to format these notes - [Markdown](https://guides.github.com/features/mastering-markdown/).

Markdown is a simplified version of HTML, the code that is behind most webpages on the internet.

One reason to markdown is that it is a simple way to create documents that anyone can access. You may be very use to using word processing programs like Microsoft Word. While these are very nice, they are not free and not everyone has access. Also, when we are doing work on the computer usually using Linux we would not be able to read these Microsoft documents.

To write something in Markdown, all you need to do is write text like you always do, but you will format it using some special symbols.
**Using an editor**

It helps to have an editor so that you can see what your markdown will look like when it is rendered (final version that people see). Suggestions for free software include:

- [MacDown - Mac](http://macdown.uranusjr.com/)
- [Markdown Pad - Windows](http://markdownpad.com/)

**Markdown basics**

See a really good guide at: https://help.github.com/articles/markdown-basics/
Paragraphs

Regular paragraphs are no different than typing on any text editor/word processor. Just type.

**Adding Headings**
Use the '#' key to make a line a heading (subtitle). For really big fonts use just one '#' the more '#'s' used, the smaller the subtitle.

# Example 1

```# Example 1```

## Example 2

`## Example 2`

### Example 3

`### Example 3`

#### Example 4

`#### Example 4`

### Bolding and emphasis

Surrounding a word or phrase with one set of asterisks `*makes it italic*` *makes it italic*. Using two sets `**makes it bold**` **makes it bold**.

#### Lists
Lists can be:

`* Unordered`

`* Start with a single asterisk`

`* Have one item per line.`


* Unordered

* Start with a single asterisk

* Have one item per line.

To make an ordered list:

`1. Start the list with one number, followed by a period`

`2. On the next line, just use the next number.`

1. Start the list with one number, followed by a period

2. On the next line, just use the next number.


#### Links and Images
A link is properly written in markdown using a pair of square brackets '[]' followed by round parentheses '()'. The text of the link will go in the square brackets, and the actual URL will go in the parentheses:

`[Link to Markdown Basics](https://help.github.com/articles/markdown-basics/)`

[Link to Markdown Basics](https://help.github.com/articles/markdown-basics/)

If you want an image, just follow the link text in the brackets with an exclamation mark '![ ]\( )'

`![Kitten image](files/kittens.jpg)`

![Kitten image](files/kittens.jpg)



**Questions**: <br>
1. What is the default number of lines that tail displays?<br>
2. What is the difference between '>' and '>>'


### References

[A Quick Guide to Organizing Computational Biology Projects](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424)


[Next: BASH](https://acharbonneau.github.io/2016-09-28-MSU/07_the_filesystem.html)

[Home](https://acharbonneau.github.io/2016-09-28-MSU/)
