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
---
# Solution
1. Answer for Q1
  a.-128~127
  b.TODO
  c.32768
  d.0
  e.-1
2. Answer for Q2(Seems Question have some issues about array indexing)
3. Answer fo Q3
  ```systemverilog
  a.
  bit [11:0] my_array [4];
  
  b.
  bit [3:0] iter;
  foreach (my_array[i]) begin
    iter = i;
    my_array[i] = {iter,iter+1,iter+2};
  end
  
  c.
  
  
  ```


# Reference
[systemverilog for verification]()
