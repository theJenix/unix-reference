# Basic commands

## Table of contents

1. [Where am I?](https://github.com/tomelm/unix-reference/blob/master/basics.md#pwd)
2. [What's in this directory?](https://github.com/tomelm/unix-reference/blob/master/basics.md#ls)
3. [How do I change directories?](https://github.com/tomelm/unix-reference/blob/master/basics.md#cd)
4. [How do I remove files and directories?](https://github.com/tomelm/unix-reference/blob/master/basics.md#rm)
5. [How do I create empty files?](https://github.com/tomelm/unix-reference/blob/master/basics.md#touch)
6. [How do I create directories?](https://github.com/tomelm/unix-reference/blob/master/basics.md#mkdir)
7. [How do I copy files?](https://github.com/tomelm/unix-reference/blob/master/basics.md#cp)
8. [How do I move files?](https://github.com/tomelm/unix-reference/blob/master/basics.md#mv)
9. [Relative directories](https://github.com/tomelm/unix-reference/blob/master/basics.md#-and-)

## Basics!

You've just opened up a new terminal and something like this pops up

```
$
```

Awesome! But what now? **Where are we?**

### ``pwd``

``pwd`` will show you what directory you're in. Actually, it stands for *print working directory*. Easy enough right?

```
$ pwd
/Users/telmalem
```

So… **what's in here?**

### ``ls``

``ls`` will *list* the content of the current directory.

```
$ ls
Applications Desktop      Documents    Downloads    Dropbox      Library      Movies       Music        Pictures     Public       bnr          code         gt-webdev    school       www
```

Cool, I know what's in here but **how do I get into the ``school/`` folder?**

### ``cd``

I want to get into ``school/``. For that, we can use ``cd`` or *change directory*.

```
$ cd school 
school $ 
```

Let's see what's in here

```
school $ ls
fall-assignments.txt  cs4460
```

CS4460? That was for last semester, I don't need that anymore! **How do I remove it?**

### ``rm``

``rm`` will *remove* things for you. Note: you cannot undo ``rm`` so make sure you really want to remove.

Since the semester is over I don't need either the ``fall-assignments.txt`` file or the ``cs4460/`` folder. I'm going to remove them.

```
school $ rm fall-assignments.txt
school $ ls
cs4460
```

The file is gone, let's remove the folder.

```
school $ rm cs4460
rm: cs4460: is a directory
school $ ls
cs4460
```

``rm`` by itself didn't work here because ``cs4460/`` is a folder. For this to work, we have to specifiy the ``-rf`` flags. The ``-r`` flag tells ``rm`` to remove the entire heirarchy so it'll remove a folder. The ``-f`` flag removes without asking for permission (which is nice if the folder has a lot of files…)

```
school $ rm -rf cs4460
school $ ls
school $
```

I'm in an empty folder now… **how can I create files and folders?**

### ``touch``

Now that we're in an empty directory, we want to create a few empty files in preperation. ``touch`` serves two purposes:

1. It'll create files that don't already exist
2. It'll update the timestamps for filed ``touch``ed that already exist.

Let's create a file called ``spring-assignments.txt``

```
school $ ls
school $ touch spring-assignments.txt
school $ ls
spring-assignments.txt
```

Now, **how do I create folders** for my classes next semester?

### ``mkdir``

We can *make directories* using ``mkdir``. 

```
school $ mkdir cs1332
school $ mkdir cs2110
school $ ls
spring-assignments.txt  cs1332  cs2110
```

Now, I want a copy of ``spring-assignments`` in both my folders, **how do I copy that file there?**

### ``cp``

``cp`` will *copy* files to places for you. The command takes an a file and a location to copy that file to: ``cp file path/to/location``.

Let's copy that file

```
school $ cp spring-assignments.txt cs1332
school $ cp spring-assignments.txt cs2110
school $ ls cs1332
spring-assignments.txt
school $ ls cs2110
spring-assignments.txt
school $ ls
spring-assignments.txt  cs1332  cs2110
```

**What if I want to move** ``spring-assignments.txt`` up a directory so I see it constantly?

### ``mv``

To *move* things around we have the ``mv`` command. This takes a file and a location to move the file to: ``mv file path/to/location``

I'm going to move ``spring-assignments.txt`` up a directory so I always see it.

```
school $ mv spring-assignments.txt ..
school $ ls
cs1332  cs2110
school $ ls ../
Applications           Documents              Dropbox                Movies                 Pictures               bnr                    gt-webdev              spring-assignments.txt
Desktop                Downloads              Library                Music                  Public                 code                   school                 www
```

We moved the file up but **what is ``..``?**

### ``..`` and ``.``

``..`` is the relative path for the parent directory. Previously, we specified ``..`` as the location to move the ``spring-assignments.txt`` file which simply meant 'move the file up to the parent directory'. (These can also be chained so that ``../../..`` is parent/parent/parent.)

``.`` represents the current directory. If you want to move a file in a subfolder to the folder you're currently in you would want to do

```
$ ls
subdirectory
$ mv subdirectory/somefile.txt .
$ ls
somefile.txt  subdirectory
```