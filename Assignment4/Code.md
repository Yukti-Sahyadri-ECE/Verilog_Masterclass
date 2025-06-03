```verilog
module mux_dff_loop (
    input  wire clk,
    input  wire rst,
    input  wire sel,
    input  wire b,
    output reg  q
);
    wire mux_out;
    assign mux_out = sel ? b : q;

    always @(posedge clk or posedge rst) begin
        if (rst)
            q <= 1'b0;
        else
            q <= mux_out;
    end
endmodule
```

### TEST BENCH

```verilog
module tb_mux_dff_loop;
    reg clk, rst, sel, b;
    wire q;

    mux_dff_loop uut (
        .clk(clk),
        .rst(rst),
        .sel(sel),
        .b(b),
        .q(q)
    );

    initial clk = 0;
    always #5 clk = ~clk;

    initial begin
        $dumpfile("mux_dff_loop.vcd");
        $dumpvars(0, tb_mux_dff_loop);
      $monitor("Time = %0t | rst = %b | sel = %b | b = %b | q = %b", 
             $time, rst, sel, b, q);
        rst = 1; sel = 0; b = 0; #12;
        rst = 0;
        sel = 1; b = 1; #10;
        sel = 0;       #20;
        sel = 1; b = 0; #10;
        sel = 0;       #20;
        $finish;
    end
endmodule

```
