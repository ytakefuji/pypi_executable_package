# pypi_executable_package

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
