
# Interface
The interface construction in systemverilog is primarily simplify the connection between testbench and design. After the introducing of interface, timing of\
of simulus can be considered when cosntructing interface. It's realized by the clock block and the signal in the clock block is synchronous to the clock signal

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
  clocking cb@(posedge clk);
    input a;
    output b;
  endclocking
    
  modport TEST (clocking cb);
  
  modport DUT (input b, clk, output a);

endinterface
```

# Program Block
The introudce of **Program Block** is to solve the problem of mixing of design and testbench events during\
the same time slot. Systemverilog schedule the testbench events separately by **Progam** . Thus, program\
cannot have any hierachy such as instances of modules, interfaces, or other programs.

* Import Region inside a systemverilog time slot                                               
slot_n &rarr Active &rarr Observed &rarr Reactive &rarr Postponed &rarr slot_(n+1)
      &uarr (Design)     (Assertion) | (testbench)  |   (sample)              
        |__________________________&darr__________&darr

# Connection TB and Design by Interface
When use interface to connect TB and Design, interface must get instantiated.

# Compilation Unit(Top-level Scope)
Scope outside the boundaries of any **module**, **macromodule**, **interface**, **program**, **package** \
or **primitive** is know as the *compilation-unit* scope.



