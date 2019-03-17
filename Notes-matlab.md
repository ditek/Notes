# Matlab
<!-- MarkdownTOC -->

- [General](#general)
- [Common Commands](#common-commands)
- [Arrays](#arrays)
    - [Vectors](#vectors)
    - [Matrices](#matrices)
    - [Colon Operator](#colon-operator)
    - [Element access](#element-access)
    - [Special Arrays](#special-arrays)
    - [Notes](#notes)
    - [Tips & Tricks](#tips--tricks)
- [Plots](#plots)
    - [Syntax](#syntax)
    - [Plot appearance](#plot-appearance)
    - [Figures](#figures)
- [Operators](#operators)
    - [Arithmatic](#arithmatic)
    - [Logical operators](#logical-operators)
    - [Relational and logical operators](#relational-and-logical-operators)
- [Flow control](#flow-control)
    - [if/else](#ifelse)
    - [for loop](#for-loop)
    - [while loop](#while-loop)
- [Logical indexing](#logical-indexing)
- [Images](#images)
- [Functions](#functions)
    - [Syntax](#syntax-1)
    - [Example](#example)
    - [Subfunctions](#subfunctions)
    - [Notes](#notes-1)
    - [Useful functions](#useful-functions)
- [String functions](#string-functions)
- [Structs](#structs)
    - [Definition](#definition)
    - [Functions](#functions-1)
- [Cells](#cells)
    - [Definition](#definition-1)
    - [Functions](#functions-2)
- [File I/O](#file-io)
    - [Linux commands](#linux-commands)
    - [File handling](#file-handling)
    - [Binary files](#binary-files)

<!-- /MarkdownTOC -->

## General
- A `;` can be used to separate commands without echoing the result.
- A `,` can be used to separate commands with echoing the result.  
    `x = 3; y = 4, z = 5;       %This will echo y=4`
- Puting `...` will allow the command to continue on the next line.
- Convention: Vectors start with a lower-case letter while matrices start with a capital letter.
- Indices start with 1
- `inf` is a keyword to represent infinity.

---------------------------------------
## Common Commands
```matlab
>> clear
    Clears the variables list.
>> clc
    Clear command window.
>> help <cmd>
    Prints the help page of a command
>> doc <cmd>
    Shows the the documentation page of a command
>> format <param>
    Changes the way the output is printed (<format comapct> reduces line spacing)
>> pause(x)
    Pauses execution for x seconds
>> fprintf('%d items at %.2f each. Total=%5.2f\n', n, price, total)
    Prints a formatted string (.2f: float with 2 decimal places, 5.2f: float with 5 digits totally)
>>
>> x = input('Enter a number:')
    Accept user input
>> whos [<vars>]
    Prints details about the variables or prints all workspace variable.
>> save [file_name] [<vars to save>]
    Save all or some of workspace variables to matlab.mat file (default) or to the specified file name.
>> load [file_name] [<vars to restore>]
    Restore a saved workspace. Looks for matlab.mat if no file name is specified.
```

---------------------------------------
## Arrays

### Vectors
    Definition: X = [1,2,3] OR X = [1 2 3]
    Length:     length(X)   %will return 3

### Matrices
    Definition: Y = [1 2 3; 3 2 1]
    Size:       size(Y)     % Returns 2 3
                size(X)     % Returns 1 3

### Colon Operator
    Syntax:     X = start:step:finish
                X = start:finish
    Example:    X = 1:3:11      % X = 1 4 7 10
                X = 5:-2:1      % X = 5 3 1
                X = 2:5         % X = 2 3 4 5

### Element access
    >> X(2,2)       % Returns the element at position 2,2
    >> X(2, [1 3])  % Returns the 1st and 3rd element of the 2nd row e.g. ans = 4 6

### Special Arrays
- `ones(x)`, `ones(n,m)`, `zeroes(x)`, `zeroes(n,m)` create an `x*x` or `n*m` matrix of ones/zeroes
- `diag(X)` creates matrix with `X` as its diagonal and the rest elements are zeroes.

### Notes
- end is a keyword that refers to the last index e.g. in `X(2,end)` it refers to the last column.
- `:` can be used instead of 1:end e.g. `X(1,:)` returns the first row.
- `X(:)` will return all elements of `X` as a vector.
- `'` is used to get the transposition of a matrix. e.g. `if size(X)=1 2 then size(X')=2 1`
- `.* ./ .\ .^` are used for array operations (each element with its counterpart).
- Matrix multiplication requires compatible dimensions i.e. `Z = X*Y => LxN = LxM * MxN`

### Tips & Tricks
- When using two variables to get the output of max function we get the max and its index.
- When indexing the matrix using one index, it is treated as a large vector.
- A code section can be created by putting `%%` in its beginning. We can then just run this section be choosing the `Run section` command from the toolbar.
- The Publish command will create an html page with sections and their code.
- To get a certain function output argument use tilde as a place holder: `[~, ~, raw] = xlsread('my_file.xls')`

---------------------------------------
## Plots

### Syntax
    >> plot(X,Y)            % X,Y can be variables or vectors
    >> plot(X,Y,lineSpec)   % lineSpec changes how the plot is drawn ('r*' will use red stars)
    >> bar(X,Y)             % Draw a bar graph
    >> pie(X)               % Draw a pie chart

### Plot appearance
    >> xlabel/ylabel(string)    % Change axis label
    >> title(string)            % Change plot title
    >> axis([x1,x2,y1,y2])      % Override automatic axis assignment
    >> legend(str1,str2,..)     % Insert legends for the drawn plots
    >> grid <on/off>            % Turn on/off the grid when drawing plots
    >> axis <on/off>
    >> hold <on/off>            % Don't erase the previous plot when redrawing

### Figures
    >> figure(n)    % Create a new figure numbered n or set n as the active figure
    >> close(n)     % Close figure n
    >> close all    % Close all figures

---------------------------------------
## Operators

### Arithmatic
    ^(exp) mod(x1,x2)
### Logical operators
    and or not xor any all ~ & |
### Relational and logical operators
     ~= == && ||

---------------------------------------
## Flow control

### if/else
    if condition1
        % statements
    elseif condition2
        % statements
    else
        % statements
    end

### for loop
    for i = list | for i=1:N
        ...
        break/continue
    end

### while loop
    while <condition>
        ...
    end

---------------------------------------
## Logical indexing
Used to create an array `A` using the elements of an array `B` that matches 1's in a logical array `C`.

    B = 1 -1 3
    C = B>0     => C = 1 0 1
    A = B(C)    => A = 1 3
    A = B(B>0)  => A = 1 3
    % Do operations on elements of B
    B(B<0) = 0  => B = 1 0 3
    B(B<0) = B(B<0) + 10    => B = 1 9 3

The result of logical indexing is ALWAYS a vector (when used on the right side of the equation)

---------------------------------------
## Images
    >> pic = imread('pic.jpg')  % Stores the image as a matrix
    >> image(pic)               % Display the actual image stored in the matrix

---------------------------------------
## Functions

### Syntax
    function [<return_vars vector> =] <name>[(pram1,param2,..)]
    <statements>
    end

### Example
    function [A,s] = func(x1,x2)
    A = [x1:x2];
    s = sum(A);
    end
    % In command window:
    >> [a b] = func(1,3)    % a= 1 2 3 b= 6

### Subfunctions
There can be many functions in a `.m` file but only the first one can be called from the outside.

### Notes
- `global` can be used to declare a variable to share it by functions and the workspace.
- `persistent` is used to declare a variable that keeps its value between function calls (static).
- `nargin` and `nargout` store the number of input/output arguments of a function which is useful for polymorphism.

### Useful functions
    rand(n,m)               returns n*m random matrix with values in the range [0,1]
    randi(x/[x1,x2],n/<n,m>) returns n*m (or n*n) random integer matrix with values from 1 to x or from x1 to x2.
    randn(n/<n,m>)          random matrix with normal distribution (mean=0, standard diviation=1).
    fix(X)                  return the integer part of numbers
    isscalar(var)           checks if a variable is scalar.
    error(string)           Prints a text in red and quits the function.
    isempty(var)            Checks if a a declared variable has been defined.
    logical(X)              Converts X into a logical array ( return X(i)>0?1:0
    Type conversion  int8(x), uint32(x), double(x)
    class(var)            Returns the type of the variable
    intmax/intmin('int32'), realmax/realmin('double')  Types range.
    [num, txt, raw] = xlsread(file_name [, sheet][, cells]) 	Reads an Excel file and stores it in 3 arrays for numbers, strings and everything. E.g. >> [~,~,all] = xlsread('file.xls', 2, 'D2:E6')

---------------------------------------
## String functions
    - char(var):                Convert to string.
    - strcmp/strcmpi(s1, s2):   Compare strings. Case sensetive/insensetive.
    - strncmp/strncmpi():       Compares the first n letters.
    - findstr(s1, s2):          Searches for s2 inside s1
    - strmatch():               Searches an array for rows starting with string.
    - isletter():               Finds letters
    - isspace():                Finds white spaces
    - upper/lower(str):         Convert to upper/lower case
    - str2num(), num2str():     Convert between numbers and strings.
    - str=sprintf():            Similar to fprintf but prints to a string
    - strrep(str, s1, s2)       Looks for s1 in str and replaces it with s2

---------------------------------------
## Structs

### Definition
    - struct1.field1 = 5        % Matlab creates a struct called struct1 with a field called field1.
    - struct1 = struct(field1_name, field1_val, field2_name, field2_val, ...)
        struct1 = struct('Name', 'John', 'Age', 25)

### Functions
    - isstruct(var):                    Checks if var is a struct.
    - isfield(struct1, 'age'):          Checks if there is a field called 'age' in struct1.
    - struct2=rmfield(struct1, 'age'):  Creates struct2 that equals to struct1 after removing field 'age'.
    - setfield(), getfield():           Sets/returns the value of a field in a struct.
    - orderfields():                    Changes fields order.

---------------------------------------
## Cells
- They are pointers to other variables.
- Mostly used in cell arrays.
- Cells in cell arrays are accessed using big brackets, e.g.

### Definition
    - p{1} = 3.1    % create a cell array named p with the first cell pointing at 3.14
    - cell(3,3)     % Create a 3x3 cell array
    - p = {3.14, 'hi'; 'bye', 5}	% Create and populate a 2x2 cell array

### Functions
    - celldisp():   Show all objects pointed at by a cell array
    - cellfun():    Apply a function to all the objects pointed at by a cell array
    - cellplot():   Plot cell array elements
    - cell2struct(): Convert cell array into a struct array
    - num2cell():   Convert a numeric array into a cell array.
    - deal():       Copy a value into output arguments
    - cellfun(func, c_arr):	apply function func to c_arr elements
        - b = a(cellfun(@(x)isempty(strfind(x,str)),a));    % return elements that do not contain str.
        - out = cellfun(@(x) x(1:3), days, 'UniformOutput', false)  % return first three characters of each element. The output can be ununiform.

- Delete an element
    - p(2,2) = []   % remove one element
    - p(2,:) = []   % remove the second row

---------------------------------------
## File I/O

### Linux commands
    - Linux file and directory management commands can be used in matalab in a similar way, but options are not supported.
    - cd C://       <=>     cd('C://')      <=>     x='C://'; cd(x)
    - pwd, ls

### File handling
    - str = fileread(filename):             Reads a file to a string
    - fid = fopen(filename, <permission>):  Open file and return fileID (negative if unsuccessful).
    - fclose(fid)
    - Permissions: rt-open/read, 'wt'-open/create/overwrite/write, 'at'-open/create/write/append, 'r+t'-open/read/write, 'w+t'-open/create/overwrite/read/write, 'a+t'-open/create/append/read/write
    - fprintf(fid, string, format_args)
    - str = fgets(fid):                 Reads one line from a file. Returns -1 when it reaches EOF.
    - C = textscan(fileID,formatSpec):  Read formatted data from text file or string. E.g. Create a float array:
        >> str = '0.41 8.24 3.57 6.24 9.27';
        >> C = textscan(str,'%f');
    - Print a file one line at a time:
        while ischar(line)  line=fgets(fid);

### Binary files
    - File is opend using fopen with omitting the 't' from the permission.
    - fwrite(fid, Arr, <data_type>):    Writes and array of a certain data type to a file. E.g. >> fwrite(fid, A, 'double')
    - Arr = fread(fid, num, <data_type>):   Reads num items from fid and store it in Arr. E.g. >> A = fread(fid, inf, 'double')
    - The array items are stored in the binary file as a long vector without and dimention information. This information can be stored along side the data to ease retriving it later. This is an example of formating the binary file for storing variable sized arrays:
    % write an array to the file:
    dims = size(A);
    fwrite(A, length(dims), 'double')
    fwrite(A, dims, 'double')
    fwrite(fid, A, 'double')
    % reading from the file
    n = fread(fid, 1, 'double')
    dims = fread(fid, n, 'double')
    B = fread(fid, inf, 'double')
    B = reshape(B, dims')       % Convert B from vector to an array isequal(A, B) = 1
