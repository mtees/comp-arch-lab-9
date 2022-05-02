# comp-arch-lab-9
module controlUnit_tb;

//inputs
reg clk;
reg reset;
reg [31:0] instr; 
reg [3:0] statusFlag;

//outputs
wire [3:0] ALUop;
wire PCsrc;
wire  ALUsrc;
wire [1:0] Immnet;
wire WB;
wire RegWR;
wire MRW;
wire Co;

controlUnit utt(clk, reset, instr, statusFlag, ALUop, PCsrc, ALUsrc, Immnet, WB, RegWR, MRW, Co);

initial begin

clk = 1'b0;
end

always begin 

#10 clk = ~clk;

end

initial begin

//initial
reset = 0;
instr[31:0] = 32'h00000000;
#20;
reset = 1;
// r type
instr[31:0] = 32'h00f507b3;
#20;
//i type
instr[31:0] = 32'h00450693;
#20;
//s type
instr[31:0] = 32'h01162023;
#20;
//b type
instr[31:0] = 32'hfe0896e3;
#20;

#40;
$stop;

end
endmodule
