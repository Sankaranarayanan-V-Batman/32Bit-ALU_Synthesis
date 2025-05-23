# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,
◦ Liberty Files (.lib)

![Screenshot 2025-05-23 111546](https://github.com/user-attachments/assets/a7925a0f-58ce-4352-9da0-92028dc51711)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)
Design Code:
module ALU ( input [3:0] A, B, input [2:0] ALU_Sel, output reg [3:0] ALU_Out, output regCarryOut );
```
always @(*) begin
  case (ALU_Sel)
    3'b000: {CarryOut, ALU_Out} = A + B;
    3'b001: {CarryOut, ALU_Out} = A - B;
    3'b010: ALU_Out = A & B;
    3'b011: ALU_Out = A | B;
    3'b100: ALU_Out = A ^ B;
    3'b101: ALU_Out = ~A;
    3'b110: ALU_Out = A << 1;
    3'b111: ALU_Out = A >> 1;
    default: ALU_Out =4'b0000;
  endcase
end
endmodule
```
TestBench:
module ALU_tb; reg [3:0] A, B; reg [2:0] ALU_Sel; wire [3:0] ALU_Out; wire CarryOut;
```
ALU uut (
     .A(A),
     .B(B),
     .ALU_Sel(ALU_Sel),
     .ALU_Out(ALU_Out),
     .CarryOut(CarryOut)
);
initial begin
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
    $finish;
end

endmodule
```
### Step 2 : Performing Synthesis

The Liberty files are present in the library path,
![Screenshot 2025-05-23 111248](https://github.com/user-attachments/assets/e85b6bf0-1e9b-4d58-94c4-853f93292767)

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh
![WhatsApp Image 2025-05-22 at 21 07 00_3ea4567f](https://github.com/user-attachments/assets/04476de0-de80-4ca0-89aa-f97b5639d7aa)

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![WhatsApp Image 2025-05-22 at 21 07 00_5a5968e4](https://github.com/user-attachments/assets/aad7b42f-221d-4520-9825-84e08779d27d)

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![image](https://github.com/user-attachments/assets/5a30db43-005e-4ff6-9b72-2e90487355ad)


#### Area report:
![WhatsApp Image 2025-05-22 at 21 07 00_f9456336](https://github.com/user-attachments/assets/fd452594-da9a-4026-bd99-49499173c58f)

#### Power Report:
![WhatsApp Image 2025-05-22 at 21 07 00_53271679](https://github.com/user-attachments/assets/ef889090-6969-47bb-b5f7-b4f522d868ed)

#### Result: 
![WhatsApp Image 2025-05-22 at 21 07 00_c8d41b96](https://github.com/user-attachments/assets/97e6c2c7-6c7a-4acb-8cf2-ec8fbf968356)

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
