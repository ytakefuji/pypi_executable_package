# pypi_executable_package

This repository shows how to generate executable python program in bin folder for pypi package.

setup.py, setup.cfg, .pypirc, python program (bugcount.py) are needed.

bugcount.py is automatically converted to bugcount binary executable code.

Successfully uploading a new package can run the following commands to run bugcount program.

$ pip install -U bugcount --user

You should download pillbug.png for testing:
https://github.com/ytakefuji/counting-for-entomologists/raw/main/pillbug.png

$ bugcount pillbug.png

https://github.com/ytakefuji/counting-for-entomologists/raw/main/r75.png

# How to register in pypi
create your account:
https://pypi.org/account/register/

# Create .pypirc file using your account information.

<pre>
$ cat .pypirc
[distutils]
index-servers =
    pypi

[pypi]
repository=https://pypi.python.org/pypi
username= ENTER your account name
password= ENTER your account password
</pre>

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
├── edges.png
├── gray.png
├── r.png
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
        ├── __init__.py
        ├── __main__.py
        ├── bugcount.py
        └── pillbug.png

</pre>

setup.py plays a key role for packaging pypi.
<pre>
$ cat setup.py
import setuptools

with open("README.md", "r", encoding="utf-8") as fh:
    long_description = fh.read()

setuptools.setup(
    name="bugcount",
    version="0.0.1",
    author="yoshiyasu takefuji",
    author_email="takefuji@keio.jp",
    description="A package for counting bugs",
    long_description=long_description,
    long_description_content_type="text/markdown",
    url="https://github.com/ytakefuji/counting-for-entomologists",
    project_urls={
        "Bug Tracker": "https://github.com/ytakefuji/counting-for-entomologists",
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
            'bugcount = bugcount:main'
        ]
    },
)
</pre>

# setup.py can create build and dist folders:
<pre>
dist and build folders can be automatically generated:
$ python setup.py sdist bdist_wheel

egg file in build folder can be automatically generated:
$ python setup.py install

You should test your program (bugcount) before uploading the pypi package.
For testing, you should download pillbug.png and run the following command:
$ bugcount pillbug.png

Option: For testing
$ python setup.py test

In order to upload a new package, twine installation is needed.
$ pip install twine

For testing dist package,
$ twine check dist/*

Option: You can also register testpypi before running the following command.
$ twine upload --repository testpypi dist/*

You can finally upload your package to pypi:
$ twine upload dist/*
If the command is successful, pypi link will be shown.

entry_points in setuptools.setup can generate bin execution file.

</pre>

<pre>
$ cat setup.cfg
[metadata]
name = bugcount
version = 0.0.1
author = yoshiyasu takefuji
author_email = takefuji@keio.jp
description = Counting the number of objects or dead bugs
long_description = file: README.md
long_description_content_type = text/markdown
url = https://github.com/ytakefuji/counting-for-entomologists
project_urls =
    Bug Tracker = https://github.com/ytakefuji/counting-for-entomologists
classifiers =
    Programming Language :: Python :: 3
    License :: OSI Approved :: MIT License
    Operating System :: OS Independent

[options]
package_dir =
    = src
packages = find:
python_requires = >=3.6

[options.packages.find]
Where = src
</pre>

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

# How to update a new version of your program
<pre>
1. modify the program (bugcount.py) for update.
2. version number in setup.py and setup.cfg must be modified
3. remove all files in dist folder and in build folder 
   since pypi can only accept new version.
4. run the following commands to generate the necessary files in dist folder.
 $ python setup.py sdist bdist_wheel
 $ python setup.py install for testing bugcount execution.
 $ bugcount pillbug.png
5. finally upload the new package to pypi.
 $ twine upload dist/*
</pre>
