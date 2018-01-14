<img src="etc/banner.png">

[![](https://zenodo.org/badge/117367205.svg)](https://zenodo.org/record/1146890#.WlpxPZM-f9s)

# APE = Awk Plus Extensions

## Usage

    cd src
    chmod +x # only needed first time
    ./ape
 
This will print the current command line options.

## About

APE is  pre-processor to awk that handles:

- structs, with field accessed via a nested dot syntax;
- auto initialization of nested structures
     - utilizing Gawk 4.0's nestes lists, plus indirect function calls
- unit tests
- multi-line comments containing markdown
- tests for for rogue locals

Also supproted in the `ape` tool are convenient
short-cuts for:

- Vim editting
- Git pull and pushing

Further, the current release of `ape` contains (a few) abstract
data types:

- `num` : numbers
- `some` : stochastic sample of numbers

## INSTALLATION

All you need is one file: [`ape`](src/ape). Place in the same
directory as your `*.ape` files. Then

     chmod +x ape

## TESTING

If you check out this repo, then 

     cd src
     ./ape ok 

will print many lines, the last of which should say `:PERCENT 100`. e.g

    # :PASSED 20 :FAILED 0 :PERCENT 100

## COMMANDS

Source file creation

- `./ape twins xxx`  
    - Creates two source code files `xxx.ape` and `xxxok.ape`.
    - `xxx.ape` loads `ape0.ape`
    - `xxxok.ape` load `xxx.ape` and runs unit tests. 

Source file editting

- `./ape ed xxx.ape`
    - Edit `xxx.ape` with `vim` using some convenient settings. 

Gitting

- `./ape pull`
    - Grab files from master
- `./ape push`
    - Git commit, then git push

Source file execution

- `./ape run xxx`
    - runs the  file `xxx.ape`
- XXX from standard input
- XXX from file name nput

Test suite execution

- `./ape ok xxx`
    - runs the  file `xxxok.ape`, reports pass, fails
- `./ape ok `
    - runs all  the `*ok.ape` files, reports pass, fails

Documentation

- XXX generate .md
- XXX generate .html (using grip... may incur github timeout restrictions)

## FILES

### System Files

- `ape`     = the main routines
- `ape0.ape` = core functionality (structs and unit tests)
  This file is auto-generated by `ape` if
   it does not exist.

### Files 

- `xxx.ape` = your code
- `xxxok.ape` = test scripts for `xxx.ape`

These two files can be auto-generated using the command   
`./ape twins xxx`.

### DIRECTORIES

- `./` = where to find  `.ape` source files; 
- `$Var` = where to store long-lived temoraries. Defaults to `$Src/var`;
  If `$Var` is in some version-controlled directory
  (e.g. git) best to exclude $Var from the files under version control
  (e.g. by adding the $Var pathname to `.gitingore`);
- `$Lib` = where to store generated `.awk` files;
- `$Doc` = where to store generated `.md` files.

If `$Var, $Lib, $Doc`  do not exist, they  are auto-generated by `ape`.

## Coding Conventions

### Abstract Data Types

Abstract data type `xx` is stored in file `xs.ape`, which contains an initialization
function:

     function Xx(i, initarg) {
       Object(i)  # supertype initialization. Defaults to "Object"
     }
     function XxAdd(i, x) {
       # do something to add "x" into "i"
     }

Note the Camelcase for the function creation. Also, note the
convention that the operators for the abstract data type is `XxAdd` is
an extended CamelCase.

### Variables

XXX global


