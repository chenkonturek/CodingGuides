## Overview
This guide covers: 
* [Python: Struture a Project](https://github.com/chenkonturek/CodingGuides/blob/master/Python_project_guide.md#python-struture-project)  
* [Python: Coding Style Guide](https://github.com/chenkonturek/CodingGuides/blob/master/Python_project_guide.md#python-coding-style-guide)


## Python: Struture a Project 
* **projectname/**
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
      * **environment.yml** defines environment name (lowercase), python version, and dependencies. 
      ```
      name: ENV_NAME 
      channels:
      - defaults
      - conda-forge
      - ericmjl
      dependencies:
      - python=3.6
      - matplotlib=2.0.2
      - jupyter=1.0.0
      - numpy=1.13.1
      - pandas=0.20.3
      - scipy=0.19.1
      - pip
      - pip: 
        - xxx
      ```

      * create conda environment using `$ conda env create`, activate conda environment `$ source activate ENV_NAME`. 
      * **.env**: this file will automatically run when navigate to the project folder in termal, if [autoenv](https://github.com/kennethreitz/autoenv ) is installed. Thus the envoronment will be automatically activated.  
      ```
      source activate ENV_NAME
      ```

  * **requirements.txt** (not needed, if using conda environment management) 
    * specifies the package dependencies  
    ```
    numpy==1.13
    scipy==0.19.1
    Flask==0.12.2
    pandas==0.20.2
    scikit_learn==0.18.2
    ```
    * `$ pip install -r requirements.txt`  
   
    
  * **Makefile** : for generic mangement tasks (e.g. installation, test, documentation) during dev 
    ```
    .PHONY: init-conda init-pip activate test doc lint clean

    init-conda:
     conda env create

    init-pip:
     pip install -r requirements.txt

    activate:   
     source activate datamule-env

    test:
     py.test tests

    doc: 
     sphinx-apidoc -f -o source/ ../packagename/ 

    lint: 
     pylint datamule 

    clean: 
     find . -name '*.pyc' -delete  
    ```
    * can run each part by using `$ make` command in shell, e.g. `$ make doc` or `$ make test`.
    * generate pylint configuration file using `pylint --generate-rcfile > ~/.pylintrc`
    * note: make sure using a tab, not 4 spaces, inside the Makefile.    
  * **.coveragerc** : A configuration file for coverage check. 
    ```
    [run]
    branch = true
    omit = */tests/*

    [report]
    # Regexes for lines to exclude from consideration
    exclude_lines =
    # Have to re-enable the standard pragma
    pragma: no cover

    # Don't complain about missing debug-only code:
    def __repr__
    if self\.debug

    # Don't complain if tests don't hit defensive assertion code:
    raise AssertionError
    raise NotImplementedError

    # Don't complain if non-runnable code isn't run:
    if 0:
    if __name__ == .__main__.:

    ignore_errors = False

    [html]
    directory = coverage_html_report
    ```
    
    * `$ coverage run my_program.py arg1 arg2`
    * `$ coverage report -m` 
    * Coverage measurement is typically used to gauge the effectiveness of tests. It can show which parts of your code are being exercised by tests, and which are not.
  * **pytest.ini** : A configuration file for pytest.
    ```
    [pytest]
    addopts =
        --cov-config .coveragerc 
        --cov=packagename
    ```
  
  * **packagename/** : contains package source code 
    * \_\_init\_\_.py
    * module1.py
    * module2.py
  * **docs/** : contains package reference documentation 
    * generate documentation using `$ sphinx-apidoc -f -o source/ ../` and `$ make html`
    
  * **tests/** : contains package integration and unit tests  
    * test_xxx.py
  

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
* http://pythontesting.net/framework/pytest/pytest-introduction/




