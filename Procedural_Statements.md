# Procedural Statement

## Basic procedural statement
**function & task & void function**\
function and task are the two main procedural statement in sv. The most distinguish difference between them is whether this procedural consume time.\
Void function is a alternative to the zero-consumption task and it's the preferred choice when we want the no time cost procedural.

## Some bullet keywords about function and task
Feature keywords: less-verbose, dynamic variable, return array, automatic(auto) storage, unambiguous time values,   
Grammar reserved keywords: function, task, void, ref, const, input, output, inout, automatic

## Return from routine
Compared with verilog, systemverilog allow returning array from function and task. This is very useful when initializing an array.

## Local Storage
automatic

## Time value
**Built-in data types about time** : time, realtime\
**system function**: $timeformat\
----
## Solutions for [1] in Chap3
```systemverilog
// Answer for Q1
int my_array[512];
bit [8:0] address;
my_array[511] = 5;
my_task(my_array,address);
task automatic void my_task(const ref int input_array[512],bit [8:0] address);
    print_int(input_array[address]);
    --address;
endtask

function void print_int(int input_data);
    $display("@0t,get indexed data %0d",$time,input_data);
endfunction

// Answer for Q2
// new_address1 = 21
// new_address2 = 20

// Answer for Q3
// new_address1 = 21
// new_address2 = 21

// Answer for Q4
$timeformat(-12,2,"",5)

// Answer for Q5
// 1 5000
// 2 5000
// 1 10500
// 2 11000
// 1 15500
// 2 16000
// 1 21000
// 2 22000

```
