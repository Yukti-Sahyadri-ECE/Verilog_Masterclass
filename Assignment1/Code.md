### CODE

```verilog
module updown_counter(
    input clk,        
    input rst,        
    input up_down,    
    output reg [3:0] count 
);
    always @(posedge clk or posedge rst) begin
        if (rst)
            count <= 4'b0000;
        else if (up_down)
            count <= count + 1;
        else
            count <= count - 1;
    end
endmodule
```

### TEST BENCH

```verilog
module tb_updown_counter;
    reg clk_tb;
    reg rst_tb;
    reg up_down_tb;
  wire [3:0] count_tb;

    updown_counter uut (
      .clk(clk_tb),
      .rst(rst_tb),
      .up_down(up_down_tb),
      .count(count_tb)
    );

    initial clk_tb = 0;
    always #5 clk_tb = ~clk_tb;

    initial begin
        $dumpfile("updown_counter.vcd");
        $dumpvars(0, tb_updown_counter);

        rst_tb = 1;
        #10 rst_tb = 0; up_down_tb= 1;
        #50 up_down_tb= 0;
        #50 $finish;
    end
endmodule
```
