## Overview
This guide covers: 
* [Python: Struture a Project](https://github.com/chenkonturek/CodingGuides/blob/master/Python_project_guide.md#python-struture-project)  
* [Python: Coding Style Guide](https://github.com/chenkonturek/CodingGuides/blob/master/Python_project_guide.md#python-coding-style-guide)


## Python: Struture a Project 
* **projectname/**
  * **README.md**: provides general information (e.g. Installation, Repo Contents, Links to User Guide and APIs) to both users and maintainers of a project 
  * **LICENSE**: [choose a license](http://choosealicense.com/)  
  * **setup.py** : package and distribution managment 
  ```python
   # -*- coding: utf-8 -*-
   from setuptools import setup, find_packages

   with open('README.md') as f:

   with open('LICENSE') as f:
       license = f.read()

   setup(
       name='packagename',
       version='0.1.0',
       description='Sample package for Python-Guide.org',
       long_description=readme,
       author='xxx, xxx',
       author_email='xx@xxx.com, xx@xxx.com',
       url='https://xxxx',
       license=license,
       packages=find_packages(exclude=('tests', 'docs'))
   )
  ```

  * **Makefile** : for generic mangement tasks (e.g. installation, test, documentation) during dev 
    ```
    .PHONY: init-conda init-pip activate test doc html lint clean

    init-conda:
	      conda env create
	
    init-pip:
	      pip install -r requirements.txt
  
    activate:   
	      source activate datamule-env

    test:
	      py.test tests

    doc: 
	      sphinx-apidoc -f -o ./docs/source/ ./datamule/

    html: 
	      sphinx-build -b html ./docs/source/ ./docs/build

    lint: 
	      pylint datamule 

    clean: 
	      find . -name '*.pyc' -exec rm -f {} +
	      find . -name '*.pyo' -exec rm -f {} +
	      find . -name '*~' -exec rm -f {} +
	      find . -name '__pycache__' -exec rm -fr {} +
    ```
    * can run each part by using `$ make` command in shell, e.g. `$ make doc` or `$ make test`.
    * note: make sure using a tab, not 4 spaces, inside the Makefile.    
    
  * **packagename/** : contains package source code 
    * \_\_init\_\_.py
    * flower.py
    
  * **tests/** : contains package integration and unit tests  
    * \_\_init\_\_.py
    * test_flower.py
    ```python 
    """Tests for functions in flower.py."""
    import pytest 
    import packagename.flower
    
    class TestFlower(object): 
       def setup_method(self, method): 
           self.file = xxx 
           self.data = xxx 
	   
       def test_xxxx(self):
           assert xxx == xxx
       
       def test_print_xxxx(self, capsys):
           out, err = capsys.readouterr()  
           assert xxx == xxx    
	
       def test_errors_xxx(self): 
            with pytest.raises(ValueError):
                xxxx 	   
		
       def teardown_method(self, method):
            if os.path.exists(self.file):
                 os.remove(self.file)   
    ```   

  * **docs/** : contains package reference documentation 
    * `$ sphinx-quickstar` can be used to create source directory and build directory. In addition, this also produces config file and 2 more folders with your chosen prefix (e.g. _) under the source directory. 
    * **source/**: contains rst doc sources, produced by `$ sphinx-apidoc -f -o ./docs/source/ ./` or `$ make doc`. This directory also contains the Sphix configuration file `config.py`.  
    * **build/**: contains html files, produced by `sphinx-build -b html ./docs/source/ ./docs/build` or `$ make html`
       * **_static**: for custom stylesheets and other static files 
       * **_templates**: for custom HTML templates 
    * **index.html**: a file to redirect the link to the index file inside docs/build/ folder. This is needed to publish API docs on Github using Github Pages (in Github Settings). 
    ```html
    <!DOCTYPE HTML>
    <html lang="en-US">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="refresh" content="1;url=build/index.html">
        <script type="text/javascript">
            window.location.href = "build/index.html"
        </script>
        <title>Page Redirection</title>
    </head>
    <body>
        <!-- Note: don't tell people to `click` the link, just tell them that it is a link. -->
        If you are not redirected automatically, follow the <a href='build/index.html'>link here.</a>
    </body>
    </html>    
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
    
  * **.pylintrc**: a pylint configuration file  
     * generate a pylint configuration file using `pylint --generate-rcfile > ~/projectname/.pylintrc`
     * can either put this config file under the project folder or in your home directory. 
     
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
      * Docstrings: (e.g. using numpydoc version of docstring)
      ```python 
      def function_class_or_method(object):
      """
      Summary line.

      Extended description of function/class.
 
      Parameters
      ----------
      arg1 : boolean (default: ``True``)
          Description of arg1 

      
      Returns
      ------- 
      int 
          Description of return value 
      """
      ```
      
 4. **Organisation** 

## References 
* http://docs.python-guide.org/en/latest/
* https://www.python.org/dev/peps/pep-0008/
* https://www.python.org/dev/peps/pep-0020/
* https://github.com/kennethreitz/samplemod 
* http://pythontesting.net/framework/pytest/pytest-introduction/
* http://assorted-experience.blogspot.co.uk/2014/07/use-numpydoc-sphinx.html



