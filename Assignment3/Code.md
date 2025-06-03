### CODE 

```verilog

module mux2to1(
    input sel,     
    input a,      
    input b,      
    output reg  y  
);
    always @(*) 
      begin
        if (sel == 1'b0)
            y = a;
        else
            y = b;
    end
endmodule
```

### TEST BENCH

```verilog

module tb_mux2to1;
    reg a_tb, b_tb, sel_tb;
    wire y_tb;


    mux2to1 uut (
      .sel(sel_tb),
      .a(a_tb),
      .b(b_tb),
      .y(y_tb)
    );

    initial begin
        $dumpfile("mux2to1.vcd");
        $dumpvars(0, tb_mux2to1);

        a_tb = 0; b_tb = 1;
        sel_tb = 0;
        #10 sel_tb = 1;
        a_tb = 1; b_tb = 0;
        sel_tb = 0;
        #10 sel_tb = 1; 
        #10 $finish;
    end
endmodule
```
