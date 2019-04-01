Using PYTHONPATH
PYTHONPATH is an environment variable.

See the Python 3 docs for PYTHONPATH.

The PYTHONPATH variable has a value that is a string with a list of directories that Python should add to the sys.path directory list.

The main use of PYTHONPATH is when we are developing some code that we want to be able to import from Python, but that we have not yet made into an installable Python package (see: making a Python package).

Returning to the example module and script in Where does Python look for modules?:

```
Contents of code/a_module.py
def func():
    print("Running useful function")
```

```
Contents of scripts/a_script.py
import a_module

a_module.func()
```

At the moment, on my machine, PYTHONPATH is empty:

```
$ echo $PYTHONPATH
```

Before we set PYTHONPATH correctly, a_script.py will fail with:

```
$ python3 scripts/a_script.py
Traceback (most recent call last):
  File "scripts/a_script.py", line 1, in <module>
    import a_module
ModuleNotFoundError: No module named 'a_module'
```

Now I set the PYTHONPATH environment variable value to be the path to the code directory:

```
$ # Set PYTHONPATH to path to the working directory + /code
$ # This is for the "bash" shell on Unix / git bash on Windows
$ export PYTHONPATH="$PWD/code"
$ # Now the script can find "a_module"
$ python3 scripts/a_script.py
Running useful function
```


Setting PYTHONPATH more permanently
You probably don’t want to have to set PYTHONPATH every time you start up a terminal and run a Python script.

Luckily, we can make the PYTHONPATH value be set for any terminal session, by setting the environment variable default.

For example, let’s say I wanted add the directory /Users/my_user/code to the PYTHONPATH:

If you are on a Mac
Open Terminal.app;

Open the file ~/.bash_profile in your text editor – e.g. atom ~/.bash_profile;

Add the following line to the end:

```
export PYTHONPATH="/Users/my_user/code"
```

Save the file.

Close Terminal.app;

Start Terminal.app again, to read in the new settings, and type this:
```
echo $PYTHONPATH
```
It should show something like /Users/my_user/code.

If you are on Linux
Open your favorite terminal program;

Open the file ~/.bashrc in your text editor – e.g. atom ~/.bashrc;

Add the following line to the end:
```
export PYTHONPATH=/home/my_user/code
```
Save the file.

Close your terminal application;

Start your terminal application again, to read in the new settings, and type this:
```
echo $PYTHONPATH
```
It should show something like /home/my_user/code.