The goal of this exercise is to learn the basics of reading and writing files
in Python.

# Contents

-   [Getting set up](#getting-set-up)
-   [Learning objective](#learning-objective)
-   [The goal](#the-goal)
-   [The script](#the-script)
-   [Best practice 1: Put code into functions](#best-practice-1-put-code-into-functions)
-   [Best practice 2: Write modules not scripts](#best-practice-2-write-modules-not-scripts)
-   [Best practice 3: Use docstrings to document your code](#best-practice-3-use-docstrings-to-document-your-code)
-   [Best practice 4: Add tests to your docstrings](#best-practice-4-add-tests-to-your-docstrings)
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

Learn how to read and write files in Python.


# Background

Let's open the Python interpreter to learn some basics about how to work with
files in Python:

    $ python3

In Python, we use the `open` function to open a file.
The basic syntax is:

    file_object = open(path_to_file, access_mode)

The `access_mode` is usually `'r'` for **reading** from the file or `'w'` for
**writing** to the file.
There are other modes, but these are the most common and the only modes we will
worry about here.

Let's try opening the `dummy.txt` file in this repo:

```python
>>> file_object = open('dummy.txt', 'r')
>>> type(file_object)
```

Just like any Python object, we can use `help` to find out more about it and
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
Below, we will show a more efficient example.

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

## A simple example

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

Your goal is to write a script that will read `origin.txt`
and find all occurrences of certain words (more on that in a bit)
and write occurrences to a new file.

## The words to find

Find all words related to heritability;
your script should find heritable, inherit, inheritance, and other
forms of these words.
Use a regular expression pattern to find these.

## The format of the output file


# Extra challenges (i.e., not required)

-   The code in our `get_smallest_prime_factor` function is not very efficient.
    Can you improve it?
-   Write another script (module) that calculates and returns a list of prime
    numbers that are factors of an integer provided at the command line
    -   Make sure to `import smallest_factor` and use the
        `get_smallest_prime_factor` function in your new script.
    -   Make sure to follow the best practices above!


# Acknowledgments

## Support
This work was made possible by funding provided to [Jamie
Oaks](http://phyletica.org) from the National Science Foundation (DEB 1656004).


# License

The text version of *On the Origin of Species* in `origin.txt` was copied from
Project Gutenberg under the Project Gutenberg License, which states:

> This eBook is for the use of anyone anywhere at no cost and with almost no
> restrictions whatsoever.  You may copy it, give it away or re-use it under
> the terms of the Project Gutenberg License included with this eBook or online
> at www.gutenberg.org

The full version of the Project Gutenberg License can be found at the end of
the `origin.txt` file.

All content in this repository other than the `origin.txt` file is licensed under a Creative Commons License:

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/deed.en_US">Creative Commons Attribution 4.0 International License</a>.
