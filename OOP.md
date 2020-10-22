# OOP
## Class

## Package

## OOP Terminology

**class, object, handle, property, method, proptotype**

### Object

Common class template:
```systemverilog
class abc 

function new();
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
