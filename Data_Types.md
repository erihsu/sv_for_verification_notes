# Data types
* Built-in data types 
 1. 4s  
  logic, integer, time 
 2. 2s  
  bit, int, byte, shortint,longint, real 
* Array 
1. Fixed-size Array 
```systemverilog
int array1[16]; // 16 elements of int data, declare
``` 
2. Dynamic Array 
```systemverilog
int array1[]; // declare
array1 = new[5]; // allocate 5 elements
```  
3. Associative Array
```systemverilog
int assoc1[int]; // declare associative array with int type index and int value
``` 
4. Queue
```systemverilog
int queue1[$] = {1,2,3}; // initialize queue
queue1 = {q[0],3,q[1:$]}; // insert element
``` 
* Enumerate data types
```systemverilog
typedef enum {RED, GREEN, BLUE} color_type; // declare a named enumerate data type
``` 
* Constants\
use `const` keyword to decorate a data
* Strings
```systemverilog
s = "systemverilog";
``` 
