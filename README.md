# pypi_executable_package

The example bugcount.py will be automatically converted to bugcount binary executable code.

setup.py, python program (bugcount.py), and README.md are needed for pypi packaging.

Successfully uploading a new pypi package can run the following commands 
to install bugcount program.

$ pip install -U bugcount --user

You should download pillbug.png file for testing:

https://github.com/ytakefuji/counting-for-entomologists/raw/main/pillbug.png

$ bugcount pillbug.png

<img src="https://github.com/ytakefuji/counting-for-entomologists/raw/main/r75.png" width=270 height=270>

You can change the minimum size of objects by Canny-coeffient (default:75):

$ bugcount pillbug.png 10

<img src="https://github.com/ytakefuji/counting-for-entomologists/raw/main/r10.png" width=270 height=270>

$ bugcount pillbug.png 100

<img src="https://github.com/ytakefuji/counting-for-entomologists/raw/main/r100.png" width=270 height=270>

The smaller Canny coeffient, the more objects (BLOBs) can be detected.

======================================================================

# Six steps to package a pypi library.

# 1. Create a Python program (bugcount.py)

# 2. How to register in pypi
create your account:
https://pypi.org/account/register/

# directory-information
<pre>
$ tree
.
├── LICENSE.txt
├── MANIFEST.in
├── README.md
├── blur.png
├── bugcount.egg-info
│   ├── PKG-INFO
│   ├── SOURCES.txt
│   ├── dependency_links.txt
│   ├── entry_points.txt
│   └── top_level.txt
├── build
│   ├── bdist.linux-x86_64
│   └── lib
│       ├── bugcount.py
│       └── src
│           ├── __init__.py
│           ├── __main__.py
│           └── bugcount.py
├── dist
│   ├── bugcount-0.0.5-py3-none-any.whl
│   ├── bugcount-0.0.5-py3.8.egg
│   └── bugcount-0.0.5.tar.gz
├── setup.cfg
├── setup.py
└── src
    ├── __init__.py
    ├── __main__.py
    ├── blur.png
    ├── bugcount.egg-info
    │   ├── PKG-INFO
    │   ├── SOURCES.txt
    │   ├── dependency_links.txt
    │   ├── entry_points.txt
    │   └── top_level.txt
    ├── bugcount.py
    ├── edges.png
    ├── gray.png
    ├── pillbug.png
    ├── r.png
    ├── r10.png
    ├── r100.png
    ├── r75.png
    └── src

</pre>

# 3. Create a setup.py file
setup.py plays a key role for packaging pypi.
<pre>
$ cat setup.py
import setuptools

with open("README.md", "r", encoding="utf-8") as fh:
    long_description = fh.read()

setuptools.setup(
    name=<b>"bugcount",
    version="0.0.1",
    author="yoshiyasu takefuji",
    author_email="takefuji@keio.jp",
    description="A package for counting bugs",
    long_description=long_description,
    long_description_content_type="text/markdown",
    url="https://github.com/ytakefuji/counting-for-entomologists",
    project_urls={
        "Bug Tracker": "https://github.com/ytakefuji/counting-for-entomologists"</b>,
    },
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    package_dir={"": "src"},
    py_modules=['bugcount'],
    packages=setuptools.find_packages(where="src"),
    python_requires=">=3.6",
    entry_points = {
        'console_scripts': [
            <b>'bugcount = bugcount:main'</b>
        ]
    },
)
</pre>
# 4. Create \__init__.py file and \__main__.py file:

<pre>
# __init__.py
$ cat __init__.py
import bugcount
import __main__
</pre>

<pre>
# __main__.py
$ cat __main__.py
import bugcount
</pre>


# 5. Create a build folder and a dist folder using setup.py:
<pre>
A dist folder and a build folder can be automatically generated 
by the following command:
$ python setup.py sdist bdist_wheel

egg file in build folder can be automatically generated:
$ python setup.py install

You should test your program (bugcount) before uploading the pypi package.
For testing, you should download pillbug.png and run the following command:
$ bugcount pillbug.png
</pre>

# 6. Upload files at dist/*.
<pre>
In order to upload a new package, twine installation is needed.
$ pip install twine

For testing dist package,
$ twine check dist/*

You can finally upload your package to pypi:
$ twine upload dist/*
If the command is successful, pypi link will be shown.

entry_points in setuptools.setup can generate bin execution file, bugcount.
</pre>

# How to update a new version of your program
<pre>
1. modify the program (bugcount.py) for update.
2. prepare for a new README.md file using github README.md.
3. version number in setup.py must be modified.
4. remove all files in dist folder and in build folder respectively.
   since pypi can only accept new version.
5. run the following commands to generate the necessary files in dist folder.
 $ python setup.py sdist bdist_wheel
 $ python setup.py install 
   for testing bugcount execution.
 $ bugcount pillbug.png
6. check the new package.
$ twine check dist/*
7. finally upload the new package to pypi.
 $ twine upload dist/*
 pypi will show the new version of pypi URL address:
View at:
https://pypi.org/project/bugcount/0.0.6/
</pre>
