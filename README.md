SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

APPARATUS REQUIRED: Vivado 2023.1

Procedure:

Open Vivado: Launch Xilinx Vivado software on your computer.

Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

Spartan6 FPGA

LOGIC DIAGRAM

SR FLIPFLOP

image

JK FLIPFLOP

image

T FLIPFLOP

image

D FLIPFLOP

image

COUNTER

image

VERILOG CODE
D Flip Flop
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
JK Flip Flop
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)�        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
SR Flip Flop
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)�        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
T Flip Flop
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
Ripple Carry Counter
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
MOD 10 Counter
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
UP-DOWN COUNTER

VERILOG CODE:

module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
OUTPUT WAVEFORM

D Flip Flop
322413931-0aeeb1ce-64b7-48e0-bcbd-efbf6bf0010d

320558323-8662d8bf-2960-4624-adc8-6df6b2b29437
JK Flip flop
322414053-f58c6b39-81b3-400f-b2e6-5df43dd4f4ce

320563598-5b3ec235-00fc-4f84-b61e-0c457642569d
SR Flip Flop
322414218-c3f2b9c5-897f-48ef-b12d-2f446de70cb8

320568802-5c626c90-315c-48e0-9de3-fe3c4f87bc06
T Flip FLop
322414353-5bae902d-bc9e-48f1-b32c-fdb06441a797

320570273-19d226fa-5bfd-4fe0-9726-3cdfe7d0aa5b
MOD-10 COUNTER
320565050-c71dd581-83a7-4c0a-8486-49c17fde037f 320565249-7dd5026a-585c-40d0-9bff-53ba0834976f
RIPPLE CARRY COUNTER
320566559-c6c79543-f800-467a-81d7-eb7e67d14cbc 320566810-01c95bee-1816-4bb8-bd36-42e3c49ceea4
UP DOWN COUNTER
320571905-eaf2a2ee-935c-457b-92e3-aa92be0c017c 320572212-f2772b2a-196d-4b24-871c-5f153ef91116
RESULT: Thus the simulation and implementation of sequential logic gates is done and verified.
