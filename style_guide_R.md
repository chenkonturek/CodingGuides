## Summary: R Style Guide 

1. **File Names** : 
   * end in .R 
   * prefix with numbers (e.g. `0-open.R`, `1-close.R`), if need to run in sequence  
2. **Identifiers**: 
    * variable and function names should be lowercase, use underscore (_) to separate words 
    * variable names should be nouns 
    * funciton names should be verbs 
3. **Syntax** 
    * Assignment : use <- , not = 
    * Spacing: place spaces around all infix operators (e.g. =, +, -, <-, etc.)
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
 4. **Comments**
    * Use commented lines of - and = to break up code into easily readable chunks 
