#Introduction to the command line or shell
-----


The command line is an interface by which you can interact with the computer using commands rather than clicking and navigating with your mouse as you might expect. While it's scary and certainly appears like you're hacking a computer, you're really just issues commands to the computer just as you would with a click.

##Basic Navigation and Layout

Let's get started by opening up your terminal on mac or your git bash shell on windows. Once you get in there you should get a screen with a `$` that starts. That's where the fun begins.

Now let's type
```sh
pwd
```

This stands for print working directory. A directory is a like a folder and is your current location in the file system.

Now let's type:
```sh
ls
```

Now what this does is list all the files and folders in the directory. You'll likely see a lot when you first run it. This is your computers file system, where all programs and files and folders are on your computer.

Now before we go any further, it's really helpful to know where to look for help. We can do that with the `man` command.

```sh
man ls
```

This will give you instructions on what is available to you regarding that specific command. Once you've hit man, you're in an interesting prompt, at the bottom of your screen you should see a

```sh
:
```

This signifies that it's waiting for a command from you. Try typing `q`.

Woah! See how that just cleared everything off your screen, that's because we `quit` the prompt. Let's open it up again and this time type `/-F`. That performs a search in the commands - like how you might type `Cmd-F` or `Ctrl-F` when you're searching in a web page.

You can scroll with the arrow keys or by typing `f` or `b` at the `:` prompt.

Now type `h`. This will definitely be your friend because it shows you all the help commands that you would ever need about navigating the manual of a given function. The `^` symbol means you should be hitting the `ctrl` key to activate this function. There are all sorts of optimizations here but that's the majority of them.

##Motivation

Now at this point we've touched on a couple of commands like `ls`,`pwd`, and `man` and you're probably saying to yourself - "This is dumb, I can do this with my mouse, way faster." And while at this point in time that may be true, what happens when you're navigating a server in the cloud that doesn't have GUI or graphical user interface.

This was something that amazed me at first, but every computer doesn't have a graphic interface because they're actually fairly expensive computationally - the computer has to use up a lot of resources to have it be available and many servers just don't provide this kind of interface. I promise that with time, you will come to love the command line as I have. It's a fantastic way of doing what you want in a precise way and making it super easy to automate a set of instructions.

The other reason you should learn to like it is that you're going to have to use it a fair amount as a data scientist. The vast majority of your work will involve the command line in one way or another.

## Basic Commands - Con't

Let's show you some of the more basic commands, what we're going to do is navigate to the desktop and create a text file. So let's get started.

```sh
cd ~/Desktop
```

`cd` stands for change directory and allows you to navigate the file system. This should switch us into the Desktop which we can check with

```sh
pwd
```

Which should print out that we are on the Desktop, now we can type our next commands.

```sh
mkdir test_creation
touch my_file.txt
echo "Hello From the Command Line" >> my_file.txt
mv my_file.txt test_creation
echo "This is my second echo command" >> test_creation/my_file.txt
cat test_creation/my_file.txt
```

One of the things that you'll notice is that I don't use spaces very often. That's because they're a pain at the command line and have to be escaped with a `\` character. I never use spaces in my file names any more and with time you likely won't either.

Now that we've covered that, let's go through line by line what happened. First we created a directory with the `mkdir` command. This is on our Desktop and we should be able to see it if we navigated there with our mouse.
Next we created a text file, on our Desktop, with the `touch` command which just creates a simple plain text file that is empty. Next we used the `echo` command to append a string to my_file.txt (the one we just created).

Now all echo does is repeat back what you send it, if you type in echo "Hello there" then it will just print out "Hello there", however by using `>>` we append it to `my_file.txt`. This allows us to easy append more information which we will do shortly.

Now we're doing something that we haven't done before my using the `mv` command. we move the direction from location 1 to location 2. This puts our my_file.txt into the folder that we created at the command line.

The next echo command does a similar thing to what we did before, but echos the string into the file that we just moved into the folder. We can see the result of that in the next line.

`cat` is a way of reading the contents of a file. When we execute this command, it will print out everything in the following file(s) that you pass to it as arguments. It should print:

```sh
$ cat test_creation/my_file.txt
```
```
Hello From the Command Line
This is my second echo command
```

What's cool about cat is that it can actually read more than one file at once, concatenating one onto another. Let's show you how that works with the echo command.

```sh
echo "This is the second file" > second_file.txt
```

Notice how there's only one `>` in that code snippet? When we use only one `>` we overwrite everything in the file.

```sh
cat test_creation/second_file.txt
```
will print out what we just wrote in our echo statement. (Notice how it created the file for us too because it didn't exist.)

now what we can run is:

```sh
cat test_creation/my_file.txt test_creation/second_file.txt
```
And take it to the next level with:

```sh
echo "Edited first file to be this" > test_creation/my_file.txt
cat test_creation/my_file.txt test_creation/second_file.txt > all_contents.py
```

Now you'll see that `all_contents.py` is on your desktop. Go ahead and open it up and let's make some changes! Firstly you'll notice that this isn't a valid python file, we've only got strings in here and it certainly doesn't look like python. So let's make it one!

Swap out the contents for:

```py
print("This is one of my first programs.")
print("First we're going to do some basic multiplication.")
print("What is 4x4?\n the Answer is: %i" % (4*4))
```

Now that we've got that file, let's move it into our test folder.

```sh
pwd # Desktop
mv all_contents.py test_creation/contents.py
cd test_creation
python contents.py
python contents.py > contents.txt
cp contents.txt ../contents.txt
```

Now most of those commands should be a bit more familiar. We printed our working direction to make sure that we were on the Desktop. Then we moved our all_contents file to the test_creation folder. After that we changed into our subdirectory and ran the file once where it would just print out to the command line. Once where it would write into contents.txt and finally we used a new command.

The `cp` command is the copy command where we copy from one place to another. However you'll notice that we copied to a `../` directory. This is because we're using a *relative* path as opposed to a *absolute* path.

## Relative vs. Absolute Paths
These are two pretty important distinctions but are straight-forward enough. A relative path is one relative to your current location, the command line knows that we're currently at the Desktop and it knows the contents of the Desktop so when we wrote `cd test_creation` it knew that we were changing into a directory relative to our current one. Another alternative (required at sometimes) is an absolute path. This is what gets printed when we run `pwd`. That gives us the entire path. When we were at the desktop we could have equivalently used the absolute path which would be something like `cd /users/user_name/Desktop/` however we'd obviously get tired of writing that whole path, thus the relative path.

Now that we've covered the distinction between these two, let's go ahead and return to `../`.

## Basic Commands - Con't

Let's go ahead and run in our shell:

```sh
cd ..
ls .
ls test_creation
ls ..
```

This will give us some interesting output. At this point if you haven't quite realized, `..` is short for up one directory. So if we've in a folder contained in another folder, we can use `cd ..` to jump up one directory in the tree (like test_creation to Desktop).

`.` refers to the current directory, so `ls` is actually just short for `ls .`. As you probably saw in the `ls` help, we can pass a directory to `ls` to list its contents. This is what allows us to list everything in test_creation with `ls test_creation` or in the directory above Desktop with `ls ..`.
