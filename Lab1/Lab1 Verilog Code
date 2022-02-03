`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date: 01/27/2022 09:55:23 AM
// Design Name: 
// Module Name: Intro
// Project Name: 
// Target Devices: 
// Tool Versions: 
// Description: 
// 
// Dependencies: 
// 
// Revision:
// Revision 0.01 - File Created
// Additional Comments:
// 
//////////////////////////////////////////////////////////////////////////////////


module Intro(
    input [3:0] button,
    output [7:0] led,
    input sys_clkn,
    input sys_clkp
    );
    
    reg [23:0] clkdiv;
    reg [7:0] counter;
    reg slow_clk;
    reg d;
    
    // This section defines the main system clock from two
    //differential clock signals: sys_clkn and sys_clkp
    // Clk is a high speed clock signal running at ~200MHz
    wire clk;
    IBUFGDS osc_clk(
        .O(clk),
        .I(sys_clkp),
        .IB(sys_clkn)
    );
    
    initial begin
        clkdiv = 0;
        counter = 8'h00;
        d= 1'b0;
    end
    
    assign led = ~counter;
            
    // This code creates a slow clock from the high speed Clk signal
    // You will use the slow clock to run your finite state machine
    // The slow clock is derived from the fast 20 MHz clock by dividing it 10,000,000 time
    // Hence, the slow clock will run at 2 Hz
    always @(posedge clk) begin
        clkdiv <= clkdiv + 1'b1;
        if (clkdiv == 10000000) begin
            slow_clk <= ~slow_clk;
            clkdiv <= 0;
        end
    end
     
    //The main code will run fr0m the slow clock.  The rest of the code will be in this section.  
    //The counter will decrement when button 0 is pressed and on the rising edge of the slow clk 
    //Otherwise the counter will increment
    
    // LAB 1 CODE A
    /*
    always @(posedge slow_clk) begin     
    // count to 100 in binary (independantly) 
        if (counter != 8'd100) begin
             counter <= counter + 8'd10;
         end    
    end 
    */ 
    
    
    // LAB 1 CODE A
    always @(posedge slow_clk) begin     
    // count to 100 in binary (independantly) 
        if ((d==1) && (counter!=8'd0)) begin
            counter <= counter - 8'd10;  
        end
        else if ((d==0) && (counter != 8'd100)) begin
             counter <= counter + 8'd10;
        end
        else if (counter == 8'd100) begin
            d<=1'b1;
        end
        else if ((d==1) && (counter == 8'd0)) begin
            d<=1'b0;
        end 
        
           
    end  
    
endmodule
