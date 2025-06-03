### CODE

```verilog

module full_adder(
    input a,     
    input b,     
    input cin,    
    output sum,    
    output cout    
);
    assign sum  = a ^ b ^ cin;
    assign cout = (a & b) | (b & cin) | (a & cin);
endmodule
```

### TEST BENCH

```verilog

module tb_full_adder;
    reg a_tb, b_tb, cin_tb;
    wire sum_tb, cout_tb;

    full_adder uut(
      .a(a_tb), .b(b_tb), .cin(cin_tb),
      .sum(sum_tb), .cout(cout_tb)
    );

    initial begin
        $dumpfile("full_adder.vcd");
        $dumpvars(0, tb_full_adder);

        a_tb=0; b_tb=0; cin_tb=0;;
      #10 a_tb=0; b_tb=0; cin_tb=1;
        #10 a_tb=0; b_tb=1; cin_tb=0; 
        #10 a_tb=0; b_tb=1; cin_tb=1; 
        #10 a_tb=1; b_tb=0; cin_tb=0; 
        #10 a_tb=1; b_tb=0; cin_tb=1; 
        #10 a_tb=1; b_tb=1; cin_tb=0; 
        #10 a_tb=1; b_tb=1; cin_tb=1; 
        #10 $finish;
    end
endmodule
```
