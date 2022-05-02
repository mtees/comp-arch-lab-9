# comp-arch-lab-9
module controlUnit(clk, reset, statusFlag, instr, ALUop, PCsrc, ALUsrc, Immnet, WB, RegWR, MRW,Co);
input clk;
input reset;
input [31:0] instr; 
input [3:0] statusFlag;
output reg [3:0] ALUop;
output reg PCsrc;
output reg  ALUsrc;
output reg [1:0] Immnet;
output reg WB;
output reg RegWR;
output reg MRW;
output reg Co;

always @ (instr or reset or statusFlag)
begin


//s1
if (reset ==1)
case (instr[6:0])

//R
	7'b0110011:begin
	//output reg [3:0] ALUop;
	ALUop = {instr[30],instr[14:12]};
   PCsrc = 0;
	ALUsrc = 0;
	Immnet = 00;
	WB = 0 ;
	RegWR = 1;
	MRW = 0;
	Co = 0;
	
	end

//I
7'b0010011:begin
	ALUop = {instr[14:12]};
   PCsrc = 0;
	ALUsrc = 1;
	Immnet = 01;
	WB = 0;
	RegWR = 1;
	MRW = 0;
	Co = 0;
	
	end

//S
7'b0100011:begin
	ALUop = {instr[14:12]};
   PCsrc = 0;
	ALUsrc = 1;
	Immnet = 10;
	WB = 1;
	RegWR = 1;
	MRW = 1;
	Co = 0;
	
	end

//B
7'b1100011:begin
	ALUop = {instr[14:12]};
   PCsrc = 1;
	ALUsrc = 1;
	Immnet = 01;
	WB = 0;
	RegWR = 1;
	MRW = 1;
	Co = 0;
	
	end

endcase
//s0
else
case (instr[6:0])
	7'b0000000:begin
	ALUop = {instr[14:12]};
   PCsrc = 0;
	ALUsrc = 0;
	Immnet = 00;
	WB = 0;
	RegWR = 0;
	MRW = 0;
	Co = 0;
	
	end
	endcase




end

endmodule
