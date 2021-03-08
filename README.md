The goal of this exercise is to learn the basics of reading and writing files
in Python.

# Contents

-   [Getting set up](#getting-set-up)
-   [Learning objective](#learning-objective)
-   [Learning the basics](#learning-the-basics)
    -   [A simple example script](#a-simple-example-script)
-   [The Exercise](#the-exercise)
    -   [The words to find](#the-words-to-find)
    -   [The format of the output file](#the-format-of-the-output-file)
    -   [Use best practices](#use-best-practices)
-   [Extra challenges (not required)](#extra-challenges-not-required)
-   [Acknowledgments](#acknowledgments)
-   [License](#license)


# Getting set up

At this point, you should have
(1) an account on [Github](https://github.com/) and
(2) been introduced to the very basics of [Git](https://git-scm.com/).

1.  Login to your [Github](https://github.com/) account.

1.  Fork [this repository](https://github.com/joaks1/python-file-io), by
    clicking the 'Fork' button on the upper right of the page.

    After a few seconds, you should be looking at *your* 
    copy of the repo in your own Github account.

1.  Click the 'Clone or download' button, and copy the URL of the repo via the
    'copy to clipboard' button.

1.  In your terminal, navigate to where you want to keep this repo (you can
    always move it later, so just your home directory is fine). Then type:

        $ git clone the-url-you-just-copied

    and hit enter to clone the repository. Make sure you are cloning **your**
    fork of this repo.

1.  Next, `cd` into the directory:

        $ cd the-name-of-directory-you-just-cloned

1.  At this point, you should be in your own local copy of the repository.

1.  As you work on the exercise below, be sure to frequently `add` and `commit`
    your work and `push` changes to the *remote* copy of the repo hosted on
    GitHub. Don't enter these commands now; this is just to jog your memory:

        $ # Do some work
        $ git add file-you-worked-on.py
        $ git commit
        $ git push origin master


# Learning objective 

To become fluent in reading and writing files in Python.


# Learning the basics

In Python, we use the `open` function to open a file.
The basic syntax is:

    file_object = open(path_to_file, access_mode)

The `access_mode` is usually `'r'` for **reading** from the file or `'w'` for
**writing** to the file.
There are other modes, but read and write are the most common and the only
modes we will worry about here.

Let's work in the Python interpreter to learn some basics about how to work
with files in Python:

    $ python3

Let's try opening the `dummy.txt` file in this repo:

```python
>>> file_object = open('dummy.txt', 'r')
>>> type(file_object)
```

Just like any object in Python, we can use `help` to find out more about it and
see its methods:

```python
>>> help(file_object)
```

We can use the `read` method to get a string of the entire file:

```python
>>> s = file_object.read()
>>> print(s)
```

For larger files, getting a string of the entire file is not very efficient.
Below, we will learn a more efficient approach.

When we are done with the file, whether reading from it or writing to it,
make sure you **close the file**:

```python
>>> file_object.close()
```

Below, we will see how we can use `with` statements so that files get closed
automatically.

Now, let's create a new file and write a line in it:

```python
>>> new_file = open('my-new-file.txt', 'w')
>>> new_file.write('Hello, this is my new file!')
>>> new_file.close()
```

Quit out of the Python interpreter:

```python
>>> quit()
```

In your directory you should now see a new file called `my-new-file.txt`:

    $ ls
    dummy.txt
    my-new-file.txt
    origin.txt
    README.md

    $ cat my-new-file.txt
    Hello, this is my new file!

## A simple example script

Now, let's write a short Python script to parse the `dummy.txt` file in this
repo.
Create a new file called `dummy.py` and open it with your preferred text editor.
Add the following code to your file:

```python
print('Opening dummy.txt')
with open('dummy.txt', 'r') as in_stream:
    print('Opening output.txt')
    with open('output.txt', 'w') as out_stream:
        for line in in_stream:
            line = line.strip()
            word_list = line.split()
            word_list.sort()
            for word in word_list:
                out_stream.write('{0}\n'.format(word))
print("Done!")
print('dummy.txt is closed?', in_stream.closed)
print('output.txt is closed?', out_stream.closed)
```

Run this script from the command line:

    $ python3 dummy.py

Take a look at the `output.txt` file that was created by the script:

    $ cat output.txt

Notice two things about this script:

1.  We looped over the file object for `dummy.txt` line by line using a for
    loop (`for line in in_stream`).  This is more efficient than reading the
    entire file as a string.
2.  We used `with open(...) as variable_name` statements to ensure the files
    get closed. It is VERY easy to forget to close a file, so use `with`
    statements!

# The Exercise

In this repo is a text version of *On the Origin of Species* by
Charles Darwin. Check it out:

    $ less origin.txt

Your goal is to write a script that will read `origin.txt` and find all
occurrences of certain words and write occurrences to a new file.
Below, I outline which words to find and the format to use when writing them to
the new file.

## The words to find

Find all words related to heritability;
your script should find heritable, inherit, inheritance, and other
forms of these words.
Use a regular expression pattern to find these.

## The format of the output file

When you find such a word, write the line number it was found on and the word
itself separated by a tab (`'\t'`) character.
For example, here is how the first 10 lines of the file should look:

    471	Inheritance
    660	inherited
    799	inheritance
    850	Inheritance
    914	inheritance
    991	INHERITANCE
    993	inherited
    1000	inherited
    1046	inherited
    1047	inheritable

If two words are found on the same line, both should be written to the file on
separate lines (they will have the same line number).

## Use best practices

Remember what you learned from the
[best practices exercise](https://github.com/joaks1/python-script-best-practice):

-   Put meaningful units of code into functions.
-   Make your script importable as a module; i.e., use the
    `if __name__ == '__main__':`
    flow control.
-   Write informative docstrings to document your script and functions.

Also, try to keep your code general/flexible.
For example, write your functions so that they can be reused for other
purposes;
can you write them so they can be used with other files and other regular
expression patterns?

# Extra challenges (not required)

If you look at the contents of `origin.txt`, you will notice that the Gutenberg
Project has added text to the beginning and end of the file.
Can you you update your script to avoid searching this added text?

Try updating your script so that it can search for any regular expression
pattern that is provided via the command line.

Try updating your script so that a path to any text file can be specified via
the command line.
Your script should then search this file rather than `origin.txt`.


# Acknowledgments

Thanks to Project Gutenberg for providing a text version of *On the Origin of
Species*. The `origin.txt` file was copied from
<http://www.gutenberg.org/cache/epub/2009/pg2009.txt>.

## Support
This work was made possible by funding provided to
[Jamie Oaks](http://phyletica.org)
from the National Science Foundation (DEB 1656004).


# License

The text version of *On the Origin of Species* in `origin.txt` was copied from
Project Gutenberg under the Project Gutenberg License, which states:

> This eBook is for the use of anyone anywhere at no cost and with almost no
> restrictions whatsoever.  You may copy it, give it away or re-use it under
> the terms of the Project Gutenberg License included with this eBook or online
> at www.gutenberg.org

The full version of the Project Gutenberg License can be found at the end of
the `origin.txt` file.

All content in this repository other than the `origin.txt` file is licensed
under a Creative Commons License:

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US">Creative Commons Attribution 4.0 International License</a>.
