## R : Style Guide 

1. **File Names** : 
   * end in .R 
   * prefix with numbers (e.g. `0-open.R`, `1-close.R`), if need to run in sequence  
2. **Identifiers**: 
    * variable and function names should be lowercase
    * use underscore (_) or dot (.) to separate words 
    * variable names should be nouns 
    * funciton names should be verbs 
3. **Syntax** 
    * Assignment : use <- , not = 
    * Spacing: 
       * place spaces around all infix operators (e.g. =, +, -, <-, etc.)
       * place space after a comma not before 
    * Curly Braces: 
    ```r     
    if (y == 0) {
      message("Y is zero")
    } else {
      message("Y is non-zero")
    }
    ```
    
    * Line length : max 80 characters per line 
    * Indentation: two spaces, no tabs 
 4. **Organisation**
    * Genernal layout of a script 
      * Copyright statement comment 
      * Author comment 
      * File description comment  
      * source() and library () statements [optional]
      * Functions with Roxygen comments on top (e.g. description, @param, @return, @import [optional], @export [optional]) 
    * Use test should go in a separate file named: `originalfilename_test.R`
    * Commenting guidelines 
      * Entire commented lines should begin with # and one space
      * use `# =====` or `# ------` to separate code into meaningful truncks 
