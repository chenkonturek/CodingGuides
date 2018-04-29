## Python: Coding Style Guide 


1. **File Names** : 
   * end in .py 
   * module names should be lower case, short 
2. **Identifiers**: 
   * constant variable names: upper case (e.g. `CONST`)
   * class names: Camel case (e.g. `ClassName`) 
   * public function names and variable names 
   * private function and variable, with prefix _ or __
   ```python 
   class MyClass():
       def __init__(self):
           self.__superprivate = "Hello"
           self._semiprivate = ", world!"
   ``` 
   
   
3. **Syntax** 
    * Spacings:  
      * separate Functions and methods with 2 blank lines
      * separate Class definitions with 3 blank lines
      * place spaces around all infix operators (e.g. =, +, -, <-, etc.) 
    * Line length:  max 79 characters 
    * Indentation: Use 4 spaces  
    * Docstrings: 
    ```python 
    def function_class_or_method(object):
    """
    Several lines of docstring.

    Preferably using ReST 'markup'.
    """
    ```
    
 4. **Organisation**
    




