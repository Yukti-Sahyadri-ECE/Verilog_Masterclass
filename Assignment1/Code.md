### CODE

```verilog

module fourto1mux(
  input [1:0] sel,
  input [3:0] I, 
  output reg y
);
  always@(*)
    begin
    case(sel)
      2'b00:y=I[0];
      2'b01:y=I[1];
      2'b10:y=I[2];
      2'b11:y=I[3];
      default:y=I[0];
    endcase
    end
  endmodule
```

### TEST BENCH

```verilog

  module tb_mux();
  reg [1:0] sel_tb;   
  reg [3:0] I_tb;
  wire y_tb;

  fourto1mux u0 (
    .sel(sel_tb),
    .I(I_tb),
    .y(y_tb)
  );
  
  initial begin
    $dumpfile("mux.vcd");
    $dumpvars(0, tb_mux);
    I_tb = 4'b1011;
    sel_tb = 2'b00;
    $display("%b   %b = %b", sel_tb, I_tb, y_tb); 
    #10 sel_tb = 2'b01;
    $display("%b   %b -> %b", sel_tb, I_tb, y_tb);
    #10 sel_tb = 2'b10;
    $display("%b   %b -> %b", sel_tb, I_tb, y_tb);
    #10 sel_tb = 2'b11;
    $display("%b   %b -> %b", sel_tb, I_tb, y_tb);
    #10 $finish;
  end
endmodule

```
