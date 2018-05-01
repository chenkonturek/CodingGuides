## Overview
This guide covers: 
* [Python: Struture a Project](https://github.com/chenkonturek/CodingGuides/blob/master/Python_project_guide.md#python-struture-project)  
* [Python: Coding Style Guide](https://github.com/chenkonturek/CodingGuides/blob/master/Python_project_guide.md#python-coding-style-guide)


## Python: Struture a Project 

* **README.rst**: provides general information to both users and maintainers of a project 
* **LICENSE**: [choose a license](http://choosealicense.com/)  
* **setup.py** : package and distribution managment 
```python
 # -*- coding: utf-8 -*-
 from setuptools import setup, find_packages
 
 with open('README.rst') as f:
     readme = f.read()

 with open('LICENSE') as f:
     license = f.read()

 setup(
     name='packagename',
     version='0.1.0',
     description='Sample package for Python-Guide.org',
     long_description=readme,
     author='xxx xxx',
     author_email='xx@xxx.com',
     url='https://xxxx',
     license=license,
     packages=find_packages(exclude=('tests', 'docs')),
     package_dir = {...},
     install_requires = [...],
     entry_points = {...},
     extras_require = {...},
     dependency_links = [...]
 )
```

* **environment.yml** and **.env** :  for enironment management with conda 
    * **environment.yml** defines environment name, version of python to use, and dependencies. 
    * create conda environment using `$ conda env create`, activate conda environment `$ source activate ENV_NAME`. 
    ```
    name: deeplearning 
    channels:
    - defaults
    - conda-forge
    - ericmjl
    dependencies:
    - python=3.6
    - matplotlib=2.0.2
    - jupyter=1.0.0
    - numpy=1.13.1
    - seaborn=0.8
    - pymc3=3.1
    - pandas=0.20.3
    - biopython=1.69
    - rise=5.0.0
    - environment_kernels=1.1
    - scipy=0.19.1
    ```
    
    * **.env**: this file will automatically run when navigate to the project folder in termal, if [autoenv](https://github.com/kennethreitz/autoenv ) is installed. Thus the envoronment will be automatically activated.  
    ```
    source activate ENV_NAME
    ```
    
* **requirements.txt** : specifies the development dependencies 
  * `$ pip install -r requirements.txt`  
* **Makefile** : for generic mangement tasks (e.g. installation, test, documentation)
  ```
  
  ```
 
* **packagename/** : contains package source code 
  * \_\_init\_\_.py
  * module1.py
  * module2.py
* **docs/** : contains package reference documentation 
* **tests/** : contains package integration and unit tests  
  

## Python: Coding Style Guide 

1. **File Names** : 
   * end in .py 
2. **Naming conventions**: 
   * package names should be lower case and short, discourage the use of _ 
   * module names should be lower case and short, separate words with _ 
   * constant variable names: upper case (e.g. `CONST`)
   * class names: Camel case (e.g. `ClassName`) 
   * function names and variable names should be lower case, separate words with underscore (_) 
   * private function and variable, with prefix _  
   
3. **Syntax** 
    * Spacings:  
      * separate Functions and methods with 2 blank lines
      * separate Class definitions with 3 blank lines
      * place spaces around all infix operators (e.g. =, +, -, <-, etc.) 
      * no space before : , but one after 
    * Line length:  max 79 characters 
    * Indentation: Use 4 spaces  
    * Comments 
      * Block Comments  
      * Inline Comments   
      * Docstrings: 
      ```python 
      def function_class_or_method(object):
      """
      Several lines of docstring.

      Preferably using ReST 'markup'.
      """
      ```
      
 4. **Organisation** 

## References 
* http://docs.python-guide.org/en/latest/
* https://www.python.org/dev/peps/pep-0008/
* https://www.python.org/dev/peps/pep-0020/
* https://github.com/kennethreitz/samplemod 




