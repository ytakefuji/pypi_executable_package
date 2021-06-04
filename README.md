# pypi_executable_package

This repository shows how to generate executable python program for pypi package.

setup.py, setup.cfg, .pypirc, python program (bugcount.py) are needed.

# How to register in pypi
create your account:
https://pypi.org/account/register/

<pre>
$ tree
.
├── LICENSE.txt
├── MANIFEST.in
├── README.md
├── build
│   ├── bdist.linux-x86_64
│   └── lib
│       ├── bugcount.py
│       └── src
│           ├── __init__.py
│           ├── __main__.py
│           ├── bug_count.py
│           ├── bugcount.py
│           └── main.py
├── dist
│   ├── bugcount-0.0.1-py3-none-any.whl
│   ├── bugcount-0.0.1-py3.8.egg
│   └── bugcount-0.0.1.tar.gz
├── setup.cfg
├── setup.py
└── src
    ├── __init__.py
    ├── __main__.py
    ├── __pycache__
    │   ├── __init__.cpython-38.pyc
    │   ├── bug_count.cpython-38.pyc
    │   └── bugcount.cpython-38.pyc
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
    ├── main.py
    ├── pillbug.png
    ├── r.png
    └── src
        ├── __init__.py
        ├── __main__.py
        ├── bugcount.py
        ├── main.py
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
