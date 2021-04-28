# Data types
* Built-in data types 
 1. 4s  
  logic, integer, time 
 2. 2s  
  bit(unsigned), int, byte, shortint,longint, real 
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
> bit [3:0][7:0] my_array; // packed 4 bytes into 32-bits 
> bit [7:0] my_array [4]; // unpacked array  

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
# Solutions for [1] in Chap2
1. Answer for Q1\
  a.-128~127\
  b.TODO\
  c.32768\
  d.0\
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
  for (int i = 0;i<$size(my_array);i++)begin
    $display("%0d th of my_array[5:4] = %0b",my_array[i][5:4]);
  end // use for loop
  
  foreach(my_array[i]) begin
    $display("%0d th of my_array[5:4] = %0b",my_array[i][5:4]);
  end
  ```
4. Answer for Q4
  ```systemverilog
  // a.1st and 3rd are legal 
  // b.{32'bX,32'bX,32'bX,32'bX,32'b1}
  ``` 
5. Answer for Q5
  ```systemverilog
  // a.3rd is legal
  // b.{32'bX,32'bX,32'bX,32'bX,32'b1}
  ``` 
6. Answer for Q6
```systemverilog
// Street[0] = Tejon
// Street[2] = Platte
// Street[2] = Bijou
// pop_back = Boulder
// street.size = 4
``` 
7.Answer for Q7
```systemverilog
// part a.
typedef bit [23:0] mem_data;
typedef bit [19:0] address;
mem_data memory_space [address]; // declare associative adress
// part b. 
memory_space[0x00000] = 24'hA50400;
memory_space[0x00400] = 24'h123456;
memory_space[0x00401] = 24'h789ABC;
memory_space[0xFFFFF] = 24'h0F1E2D;
// part c.
foreach (memory_space[address]) 
  $display("elements at %0h is %0h", adrress,memory_space[address]);
``` 
8. Answer for Q8
```systemverilog
// part a.
int my_queue[$] = {2,-1,127};
// part b.
$display("sum of number in my_queue is %0d",my_queue.sum());
// part c.
$display("max number in my_queue is %0d",my_queue.max());
$display("min number in my_queue is %0d",my_queue.min());
// part d.

// part e.

``` 

9. Answer for Q9
```systemverilog
typedef bit [6:0] seg7;
typedef struct packed {
  seg7 header,
  seg7 cmd,
  seg7 data,
  seg7 crc;
} packet_s;
packet_s s;
s.header = 7'h5A;
``` 
10. Answer for Q10
```systemverilog
// part a.
typedef bit [3:0] nibble;
// part b.
real r = 4.33;
// part c.
shortint i_pack;
// part d.
nibble k [4];
k = '{4'h0,4'hF,4'hE,4'hD;};
// part e.
foreach (k[i])
  $display("k[%0d] = %0h",i,k[i]);
// part f. TODO 
foreach (k[])
// TODO

// TODO
``` 
11. Answer for Q11
```systemverilog
// part a.
typedef enum {ADD=2'b00,SUB=2'b01,NOT=2'b10,RED_OR=2'b11} opcode_e;
// part b.
opcode_e opcode;
// part c.
opcode = opcode.first;
do begin
  opcode = opcode.next();
  // do something
end while (opcode != opcode.first);
// part d.
ALU (
  .input(opcode),
);
```
