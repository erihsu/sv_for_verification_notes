# Testbench And Design Connection

## Interface
The interface construction in systemverilog is primarily simplify the connection between testbench and design. After the introducing of interface, timing of simulus can be considered when cosntructing interface. It's realized by the clock block and the signal in the clock block is synchronous to the clock signal.

The simpliest interface is just a bundle of bidirectional signals. An example is as follows.

```systemverilog
interface my_if (input bit clk);
  logic a;
  logic b;
endinterface
```

After consider synchronous, we can control the synchronous signal of timing. An example is as follows.

```systemverilog
interface my_if(input bit clk);
  logic a,b;
  clocking cb @(posedge clk);
    input a;
    output b;
  endclocking
    
  modport TEST (clocking cb);
  
  modport DUT (input b, clk, output a);

endinterface
```

## Program Block

The introudce of **Program Block** is to solve the problem of mixing of design and testbench events during the same time slot. Systemverilog schedule the testbench events separately by **Progam** . Thus, program cannot have any hierachy such as instances of modules, interfaces, or other programs.

* Import Region inside a systemverilog time slot    

>slot_n --> Active --> Observed --> Reactive --> Postponed --> slot_(n+1)

>If there are more than one event in Observed or Reactive region, they will return back before Active region to finish schedual.

> - Active Region: Design events
> - Observed Region: Assertion
> - Reactive Region: Testbench events
> - Postponed Region: sample signal

## Connection TB and Design by Interface

When use interface to connect TB and Design, interface must get instantiated.

## Compilation Unit(Top-level Scope)

Scope outside the boundaries of any **module**, **macromodule**, **interface**, **program**, **package** or **primitive** is know as the *compilation-unit* scope.

----
# Solution for [1] in Chap4
```systemverilog
//Answer for Q1
interface ahb_if(input bit HCLK);
  bit [20:0] HADDR;
  bit HWRITE;
  bit [1:0] HTRANS;
  bit [7:0] HWDATA, HRDATA;
  
  clocking cb @(negedge HCLK);
    output HTRANS;
    output HWDATA;
    output HWRITE;
    output HTRANS;
    output HWDATA;
    input HRDATA;
  endclocking
  
endinterface

module testbench();
  bus_master bfm;
  ahb_if ahbif;
  design_slave dut;
  assert(ahbif.cb.HTRANS == 2'b0 || ahif.cb.HTRANS == 2'b10) else $display("ERROR: interface got undefined transaction type!");
  // connect bfm, ahbif and dut

endmodule

// Answer for Q2

interface my_if(input bit clk);
  bit write;
  bit [15:0] data_in;
  bit [7:0] address;
  logic [15:0] data_out;
  
  clocking cb @(negedge clk);
      output write;
      output data_in;
      output address;
      input data_out;
  endclocking

  modport master(
    clocking cb
  );
  
  modport slave(
    input write,data_in,
    output address,data_out,
  );

endinterface

// Answer for Q3


// Answer for Q4

clocking cb @(negedge clk);
   output #25ns write;
   output data_in;
   output #25ns address;
   input #15ns data_out;
endclocking

// Answer for Q5

```

