# Create Array and Matrix
- `a = [10 20 30]` or `a = [10, 20, 30]`
	- separated by space or comma
	- horizontal
- `a = [10; 20; 30]`
	- separated by semicolon
	- vertical
- `b = [1, 2, 3; 4, 5, 6]`
	- 2 by 3 matrix
- `a(2) and b(1,2)`
	- index

# Variable Information
- `whos`
	- show the variable table and information
- `whos $var`
	- show the information of $var

# Built-in
- `:`
	- `e = 1:3` == 1 2 3
	- `e = 1:2:9` == 1 3 5 7 9
		- the middle one stands for step size
- `rand()`
	- `f = rand(2,3)`
		- create a 2 by 3 matrix with random values between 0 to 1 in each entry
- `linspace()`
	- `g = linspace(0, 1, 5)` = 0 0.25 0.5 0.75 1
		- create a vector with linearly increasing entries
		- the last one decides the length of the vector
- `reshape()`
	- `h = reshape(1:9, 3, 3)`
		- reshape a vector or matrix into ideal form
- `h(:,3)`
	- the 3rd entries of each row
	- the 3rd column
- `size()`
	- `size(h)` = 3 3
		- 3 rows, 3 columns

# Useful CMDs
- `save $filename`
	- save variables to a file
- `load $path/to/filename`
	- load variables from a file
- `clear`
	- clear the variable trable
- `clc`
	- clear the command window
- `eye($n)`
	- create a n by n identity matrix
- `ones($n)`
	- create a n by n matrix of ones
- `zeros($n)`
	- create a n by n matrix of zeros
- `disp()`
	- display

# Calculation
- `+`
- `*`
- `''`
	- `a = a'`
	- transpose

# Functions
```matlab
function [r1, r2] = foo(p1, p2)
	r1 = p1 * p2;
	local_var = p1 + p2;
	r2 = local_var * 2;
end
```
- .m files
- multiple functions can be placed in one .m file
	- ==only the one named the same as the file will be exposed==

# Control Statements
- `if`
- `else`

# Useful
- `imread($\path\to\filename)`
	- read image
- `imshow($var)`
	- display image
- `subplot($m, $n, $p)`
	- divides the current figure into an m by n grid and creates axes in the position specified by p
- `rgb2gray($var)`
	- convert the RGB image to a grayscale image