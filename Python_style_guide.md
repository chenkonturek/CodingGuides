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


https://www.python.org/dev/peps/pep-0008/




