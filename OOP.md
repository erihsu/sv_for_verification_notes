# OOP
## Class

## Package

## OOP Terminology

**class, object, handle, property, method, proptotype**

### Object

Common class template:
```systemverilog
class abc 

function abc new();
...
endfunction

function abcd copy();
...
endfunction

...

endclass

// declare handle
abc abc_o;

//allocate object
abc_o = new();

//deallocate object
abc_o = null;

```

### Method

### Property

## Static Variable & Global Variable

Global Variable means it have the global name space and it's visible to everyone. However, static variable's scope is only limited within the current boundaries, which is primary proposed to solve the problem of variable sharing between different object of the same type.

## Public VS Local
Unlike other OOP language, systemverilog regard variable as public default, to make error injection more easily. Otherwise, you have to add extra code to by-pass data-hidding mechanism.

# Solution for [1] in Chap5
```systemverilog
// Answer for Q1
class MemTrans;
  logic [7:0] data_in;
  logic [3:0] address;
  
  function void print();
      $display("Data:%0d with Address:%0d",data_in,address);
  endfunction
  
  extern function new();

endclass

initial begin
  MemTrans tr;
  tr = new(); // Default set data_in and address all to X
end

// Answer for Q2
function void MemTrans::new();
  data_in = 8'b0;
  address = 4'b0;
endfunction

// Answer for Q3
function void MemTrans::new(input logic [7:0] input_data=8'b0,input logic [3:0] input_address=4'b0);
  data_in = input_data;
  address = input_address;
endfunction

program automatic test;
  MemTrans tr1;
  MemTrans tr2;
  tr1 = new(.input_address(2));
  tr2 = new(.input_data(3),.input_address(4));
endprogram

// Answer for Q4
program automatic test;
  MemTrans tr1;
  MemTrans tr2;
  tr1 = new(.input_address(2));
  tr2 = new(.input_data(3),.input_address(4));
  tr1.address = 4'hF;
  tr1.print();
  tr2.print();
  tr2 = null;
endprogram

// Answer for Q5
class MemTrans;
  logic [7:0] data_in;
  logic [3:0] address;
  static last_address;
  
  function void print();
      $display("Data:%0d with Address:%0d",data_in,last_address);
  endfunction
  
  extern function new();
  extern static function print_last_address();

endclass

function MemTrans::new(input logic [7:0] input_data=8'b0,input logic [3:0] input_address=4'b0);
  data_in = input_data;
  address = input_address;
  last_address = address;
endfunction

// Answer for Q6

static function print_last_adddress();
  $display("Last address:%0d" last_address);
endfunction

program automatic test;
  MemTrans tr1;
  tr1 = new();
  MemTrans::print_last_address();
endprogram


// Answer for Q7

function void print_all;
  print.print_8("data_in",data_in);
  print.print_4("address",address);
endfunction

```
