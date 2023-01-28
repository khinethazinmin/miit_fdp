# miit_fdp
Day1 Content
Introduction to Verilog RTL design and Synthesis
Labs using iverilog and gtkwave
mkdir vsd  
 cd vsd  
 git clone https://github.com/kunalg123/vsdflow.git  
 mkdir vlsi  
 cd vlsi  
 git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git  
 cd SKY130RTLDesignAndSynthesisWorkshop  
 cd my_lib  
 cd lib  
 cd ..  
 cd verilog_model  
 cd ..  
 cd ..  
 cd verilog_files  
![image](https://user-images.githubusercontent.com/123365758/214255393-e497bf9b-5f3d-41cd-863a-b17537f0ffa2.png)
![image](https://user-images.githubusercontent.com/123365758/214255573-b05d953c-f601-404f-a074-3565f454f8a5.png)
![image](https://user-images.githubusercontent.com/123365758/214255647-cc2206d1-010f-4d67-bb18-813291e2e7bb.png)
![image](https://user-images.githubusercontent.com/123365758/214255688-b533a796-7e80-41a5-8066-d31b8baf4637.png)
![image](https://user-images.githubusercontent.com/123365758/214255739-4da420b0-7ff8-4b40-ac46-333bbdf3806d.png)
![image](https://user-images.githubusercontent.com/123365758/214255778-c2583585-f337-4779-8dda-113946cad127.png)
![image](https://user-images.githubusercontent.com/123365758/214255820-9bdef0fa-15b5-4412-87c6-5a52aac5f18e.png)
![image](https://user-images.githubusercontent.com/123365758/214255863-3bf5f68e-3d45-4244-b697-c72aeef216a7.png)
![image](https://user-images.githubusercontent.com/123365758/214255901-97773298-6895-4c83-a32f-a3c4c7d506e7.png)
![image](https://user-images.githubusercontent.com/123365758/214255940-bebf5d55-7170-47e8-b4b9-b3d5348caed1.png)

Day 2 Content

TIMING LIBS, HIERARCHICAL Vs FLAT SYNTHESIS AND EFFICIENT FLOP CODING STYLES

To look into the library, we use the vim command

!vim ../lib/SKY130_fd_sc_hd__tt_025C_1v80.lib

![image](https://user-images.githubusercontent.com/123365758/214512927-ef46c113-5f62-43d7-a746-f69cc625616f.png)

 :syn off command used 
 
 ![image](https://user-images.githubusercontent.com/123365758/214512997-da9f0c54-0fb1-480a-b573-30a78d802a9b.png)
 
:se nu command used

![image](https://user-images.githubusercontent.com/123365758/214513057-806e33d1-75e8-415b-a912-579d6c1e6fa5.png)

:/cell command used

![image](https://user-images.githubusercontent.com/123365758/214513154-0c0349b2-3f14-4626-8f91-47e05558ec53.png)

:/cell  .*and

![image](https://user-images.githubusercontent.com/123365758/214513261-93877971-9b52-406e-b3c4-e832f71f597b.png)

:sp ../lib/sky130……   command used

![image](https://user-images.githubusercontent.com/123365758/214513385-2bbc3850-7e8a-4184-9612-21d1e94f855f.png)

:vsp ../lib/sky130…..   command used

![image](https://user-images.githubusercontent.com/123365758/214513491-eeddbdef-a26a-4dc5-a331-47156becc971.png)

:vs command used

![image](https://user-images.githubusercontent.com/123365758/214513748-33362de5-002e-42b2-9075-ccf12f5a33de.png)

!vim multiple_modules.v command used

![image](https://user-images.githubusercontent.com/123365758/214513816-53260cda-12df-4049-818e-0f2446d5ee36.png)

After the command ----  synth –top multiple_modules, the following screenshot will be shown.

![image](https://user-images.githubusercontent.com/123365758/214513885-89216857-9a63-4b3f-a667-682dea096146.png)

Command used -- abc  –liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

![image](https://user-images.githubusercontent.com/123365758/214514015-d019a23d-bf33-4aae-a337-0bc9eb2f6a50.png)

After the command ------ show multiple_modules, the following result will be shown.

![image](https://user-images.githubusercontent.com/123365758/214514136-1cfb56d2-fdf6-400a-96a0-f6b1b6f03b73.png)

yosys>write_verilog –noattr  multiple_modules_hier.v

yosys>!vim multiple_modules_hier.v

![image](https://user-images.githubusercontent.com/123365758/214514200-2622e224-f669-4217-a6e8-fb9300668b12.png)

yosys> show

![image](https://user-images.githubusercontent.com/123365758/214514272-d2b9faa1-94e3-48bb-888e-875a7042923b.png)

# SUB MODULE LEVEL SYNTHESIS AND ITS NECESSITY

In the following example, I am going to synthesize at sub_module 1 level

yosys>synth –top sub_modules1

yosys>abc –liberty ../lib/ sky130_fd_sc_hd__tt_025C_1v80.lib

yosys>show

After above command, the following result will be shown.

![image](https://user-images.githubusercontent.com/123365758/214751668-e27717ef-dcd7-44ae-970e-e0a6df4f16db.png)

Glitches

Asynchronous and Synchronous Resets

In yosys terminal, type the command - !vim dff_asyncres.v –o dff_async_set.v

![image](https://user-images.githubusercontent.com/123365758/214751736-a1fac05d-d5a8-4c01-bcb3-443872a229db.png)

$ iverilog dff_asyncres.v tb_dff_asyncres.v

$./a.out

$gtkwave tb_dff_asyncres.vcd

![image](https://user-images.githubusercontent.com/123365758/214751844-53e7bf91-3ab1-4339-b500-bf6427090578.png)

•	Q follows d only at the posedge of the clock.

•	But as and when async_rest=1,Q becomes 0 without waiting for the next edge of the clock.

![image](https://user-images.githubusercontent.com/123365758/214752089-68d58789-748f-443f-b252-c061752a5121.png)

•	But when async_reset goes low(1 to 0),Q doesn't become 1 immediately ,it waits for the next clock edge to follow D.

•	Even if asunc_reset=1 and D=1, Q=0 as reset takes high precedence(that is how the code has been written,if condition of reset is checked first).

Synthesis implementation results : asynchronous set:

![image](https://user-images.githubusercontent.com/123365758/214752171-5969f717-9ccb-40cb-bba7-41c59c6d5b7a.png)

Synthesis implementation results : asynchronous reset

![image](https://user-images.githubusercontent.com/123365758/214752226-02ab2329-8156-4258-b1ac-c5971fd913f8.png)

For Synchronous, Synchronous Reset and set :

![image](https://user-images.githubusercontent.com/123365758/214752284-430d7821-8205-4288-abba-7524ed70ed10.png)

Synthesis Results:

![image](https://user-images.githubusercontent.com/123365758/214752327-cb15918d-3cc5-4b97-8d7b-0571d6d3dcaa.png)

Case wherein both both asynchronous and synchronous resets are applied together :
RTL Code:

![image](https://user-images.githubusercontent.com/123365758/214752372-e0dc9787-6380-4cbc-afae-36819475aef2.png)

Synthesis results:

![image](https://user-images.githubusercontent.com/123365758/214752401-2a0f014f-0b45-42cb-b3cb-3eb6b573e3c8.png)

Optimization

Let's Consider the following design where the 3 bit input is multiplied by 2 and the output is a 4 bit value.

RTL Code

![image](https://user-images.githubusercontent.com/123365758/214752480-a5373d69-51e8-4228-b72f-0b5a50fe6750.png)

Synthesis Result:

![image](https://user-images.githubusercontent.com/123365758/214752520-1427ba8b-ee18-4b83-adfb-68e1d26887e6.png)

Let's consider the following design where the 3 bit input is multiplied by 9 and the output is a 6 bit value.

module mult8 (input [2:0] a , output [5:0] y);

	assign y = a* 9;
 
endmodule

![image](https://user-images.githubusercontent.com/123365758/214752577-d6c4c762-3e19-48b1-8889-fc583d2371c8.png)

# Day – 3

# Combinational and Sequential Optimisations

opt_check.v

module opt_check (input a, input b , output y);

	assign y = a?b:0;
	
endmodule

abc -liberty ../my_lib/lib/sky130_fd_sc_hd_tt_025C_1v80.lib  

 write_verilog -noattr opt_check_netlist.v 
 
 show

 ![image](https://user-images.githubusercontent.com/123365758/214754574-79a88822-5a29-4207-bca9-39a066417849.png)


yosys> synth –top opt_check2

![image](https://user-images.githubusercontent.com/123365758/214754602-342e597a-8d1a-4fcf-8148-f9c7c91c6ef7.png)

 
opt_clean –purge
 
![image](https://user-images.githubusercontent.com/123365758/214754623-dc905905-30aa-44f1-b0c2-112f14d942a8.png)

yosys> abc –liberty ../lib/sky….

![image](https://user-images.githubusercontent.com/123365758/214754653-42b1fffb-ef8f-4288-afe7-b8941e5a85ac.png)

 
yosys> show command used

 ![image](https://user-images.githubusercontent.com/123365758/214754669-7efd51d8-b6cd-4a43-b490-11c5fc92155a.png)

yosys> read_liberty –lib ../lib/sky….

Yosys> read_verilog opt_check3.v

![image](https://user-images.githubusercontent.com/123365758/214754712-12f69eb6-64ba-4535-a869-ab67f98a6acb.png)

 
yosys> synth –top opt_check3
 
 ![image](https://user-images.githubusercontent.com/123365758/214754734-1d52cf11-6925-4e77-9d8c-bd00a39c3426.png)
 
 ![image](https://user-images.githubusercontent.com/123365758/214786964-f684c5e1-5a86-4eae-95f1-1e29101edda0.png)

![image](https://user-images.githubusercontent.com/123365758/214787864-8e448a8d-5fef-46a5-831a-97dc47d15ec9.png)



yosys> opt_clean –purge

yosys> and –liberty ../lib/sky…

 ![image](https://user-images.githubusercontent.com/123365758/214754762-b7094691-fd12-4516-aabb-4cf56337a41e.png)

 
yosys> show command used

 ![image](https://user-images.githubusercontent.com/123365758/214754794-c7f0903d-941a-47b0-89dd-495c5dc4f703.png)

vim dff_const1.v –o dff_const2.v

![image](https://user-images.githubusercontent.com/123365758/214754820-0c1ef5ec-d77d-4515-8b98-dbb084a74ace.png)

 
iverilog dff_const1.v tb_dff_const1.v

./a .out 

![image](https://user-images.githubusercontent.com/123365758/214771993-6564183e-8495-46fc-8000-745e77b768cb.png)

![image](https://user-images.githubusercontent.com/123365758/214785580-4c3af457-82ac-49c1-8b2c-2f7ba1c50790.png)

![image](https://user-images.githubusercontent.com/123365758/214785603-3d2d09a0-faf1-42aa-8ffb-362d92aca07d.png)

![image](https://user-images.githubusercontent.com/123365758/214786424-1e4135d9-f486-430b-90e6-f35404152df8.png)


![image](https://user-images.githubusercontent.com/123365758/214786459-967d0539-2b6c-44e7-be6e-6cca2c66ca1f.png)




yosys> dfflibmap –liberty ../lib/sky……

yosys> abc –liberty ../lib/sky……

yosys>show

![image](https://user-images.githubusercontent.com/123365758/214757276-69fdd77d-dc57-4651-af4d-22803633afdf.png)

yosys> read_verilog  dff_const2.v

yosys> synth –top dff_const2

![image](https://user-images.githubusercontent.com/123365758/214757838-17fc4d3c-20bd-4f97-b9a3-5e956be4be6e.png)

yosys> show

![image](https://user-images.githubusercontent.com/123365758/214758188-f2c5caf5-202b-4616-8e9e-c80617aba702.png)

![image](https://user-images.githubusercontent.com/123365758/214781951-54f9b084-73f4-49fd-ab44-4ea94bd06967.png)

![image](https://user-images.githubusercontent.com/123365758/214781991-f561ae25-9d6f-41a8-9c9c-2552ed77e510.png)

![image](https://user-images.githubusercontent.com/123365758/214783973-ce57acc4-2013-46de-bda1-09db91cb5014.png)

![image](https://user-images.githubusercontent.com/123365758/214784020-ee59ef3e-9323-4cca-a659-996375ed1ff8.png)

![image](https://user-images.githubusercontent.com/123365758/214784053-1dd54c90-248a-4cae-9aa4-8c6a5560c683.png)

![image](https://user-images.githubusercontent.com/123365758/214784081-ed46c1a4-14a6-4b8d-b8de-4cce5818795d.png)

![image](https://user-images.githubusercontent.com/123365758/214784122-96c55bfa-db22-41e0-89ae-6660f22860ed.png)

![image](https://user-images.githubusercontent.com/123365758/214784143-9c1154fc-1cd8-42e5-af90-5533c5909b25.png)

# Day 4: Gate Level Simulations,Blocking vs Non Blocking assignments,Synthesis-Simulation Mismatch

# Synthesis Simulation Mismatches

module mux(input i0, input i1, input sel, output reg y);


always @(sel)

begin

	if (sel)
	
	begin
	
		y = i1;
		
	end
	
	else
	
	begin
	
		y = i0;
		
	end
	
end

endmodule

# Blocking and non blocking statements 

module shift_register(input clk, input reset, input d, output reg q1);

reg q0;

always @(posedge clk,posedge reset)

begin
	if(reset)
	
	begin
		q0 = 1'b0;
		q1 = 1'b0;
		
	end
	
	else
	
	begin
		q0 = d;
		q1 = q0;
		
	end
	
end

endmodule

Other example:

module comblogic(input a, input b, input c, output reg y);

reg q0;

always @(*)

begin
	y = q0 & c;
	q0 = a|b;
	
end

endmodule

# Labs on GLS and Synthesis-Simulation Mismatch

![image](https://user-images.githubusercontent.com/123365758/214803790-3c188d8d-c4f5-49d8-ac1c-5a2676fe5862.png)

![image](https://user-images.githubusercontent.com/123365758/214803841-50da6b38-9828-4bea-9444-502c8cbba6ae.png)

![image](https://user-images.githubusercontent.com/123365758/214803888-4104b4b1-e305-4bff-b315-fbebe95deab3.png)

![image](https://user-images.githubusercontent.com/123365758/215038038-0f02a6b1-6fa1-4334-905e-5b752521b244.png)


Example 2:

module bad_mux (input i0 , input i1 , input sel , output reg y);

always @(sel)

begin
	if(sel)
		y <= i1;
	else
		y <= i0;
		
end 

endmodule

![image](https://user-images.githubusercontent.com/123365758/214809012-4ad85201-48b2-47b9-95ca-86ca43f0bcf6.png)

![image](https://user-images.githubusercontent.com/123365758/215039400-5b7a3557-5e75-4792-ab4d-5944812e4dad.png)

![image](https://user-images.githubusercontent.com/123365758/214810628-9d3ebf5d-95ab-4678-a05b-c1e70e8fa546.png)

Example 3: This is an example of synthesis-simulation mismatch due to wrong order of assignment in blocking assignments.

module blocking_caveat (input a , input b , input c , output reg d);

reg x;

always @(*)
begin
	d = x & c;
	x = a | b;
	
end 

endmodule

![image](https://user-images.githubusercontent.com/123365758/214812793-59c988fa-0092-47c9-afc5-ec2e1ed05c2b.png)


If we run gate level simulations on this netlist in verilog, we observe the following waveform.

![image](https://user-images.githubusercontent.com/123365758/214813737-31b9dc86-9e01-4db5-88fa-0a8ff500d4ac.png)

Here , I observe that the circuit behaves as intended combinational ckt. Output d results from the present value of inputs, and not the previous clock values like in the simulation results. Since the waveforms of the stimulated RTL verilog code do not match with the gate level simulation of generated netlist,we get a Synthesis-Simulation Mismatch again.


![image](https://user-images.githubusercontent.com/123365758/214815678-2d5e665c-1fee-40f0-a318-806fc86dd71d.png)

![image](https://user-images.githubusercontent.com/123365758/215040806-90b7c84f-f4c6-4443-99f0-4434c40c1555.png)

# Day 5 - If, Case, For Loop and For Generate

# If Constructs

If condition is used to to write priority logic. The condition one has a priority or if has more priority than the consecutive else statements . Only when condition 1 is not met condition 2 is evaluated and so on and y is assigned accordingly depending on the matching conditions.

if (cond_1)

begin 	

	y = statement_1;
	
	
end

else if (cond_2)

begin

	y = statement_2;
	
end

else if (cond_3)

begin

	y = statement_3;
	
end

else

begin

	y = statement_4;
	
end

If-else block implements a Priority logic that is if cond_1 is satisfied, next if statements are not executed. Thus above If-Else code translates to a ladder like multiplexer structure in the final design instead of a single multiplexer.

Dangers of using Incomplete If statements Inferred Logic which occurs due to bad coding styles that is incomplete if statements.

if (condt1) 

    y-a;
    
else if (condt2)

    y=b;
    
    n the above code if condition 1 is matched y is equal to a else if condition 2 is matched y is equal to b but there is no specification for the case when condition2 is not matched, as a result of which the simulator tries to latch this case to the output y.It wants to retain the value of y.
    
This is a combinational loop to avoid that the simulator infers a latch. Enable of this latch is OR of the condition 1 and condition 2. If neither condition 1 or condition 2 is met the OR gate output disables the latch . The latch retains the value of y and stores it.

This is called the inferred latch due to incomplete if statements which is very dangerous for RTL designing. It should be avoided except for some special cases like the counter.

reg[2:0]

always @(posedge clk,posedge reset)

Begin

If (reset)

Count<= 3'b000;

else if(enable)

Count<= count+1;

end

This is also a case of incomplete if statements. Here ,if there is no enable the counter should latch onto the previous value.For example if the counter has counted up till 4 and there is no enable then it should retain the value 4 rather than going to 0 again.

So here the incomplete if statements result in latching And retaining the previous value which is our desired behavior in a counter. The earlier mux example was a combinational circuit and therefore I cannot has inferred latches.

Note:

If, case statements are used inside always block.

In verilog whatever variable we use to assign in if or case statements must be a register variable.

# CASE Constructs

Let's look at the following verilog code block. Here, the inferred hardware should be a 4:1 multiplexer. The CASE statements do not have priority logic like IF statements.

always @(*)

begin

     case(sel)
     
		2'b00: begin
		
			y = statement_1;
			
			end
			
		2'b01: begin
		
			y = statement_2;
			
			end
			
		2'b10: begin
		
			y = statement_3;
			
			end
			
		2'b11: begin
		
			y = statement_4;
			
			end
			
	endcase
	
end

Depending on the cases matching the select y is assigned accordingly.

Some caveats with using CASE statements:

#  1.Incomplete CASE

reg [1:0] sel

always @(*)

begin

     case(sel)
     
     2'b00: begin
     
                   . condition 1
		   
                   end
		   
     2'b01: begin
     
                   . condition 2
		   
                   end
    end case
    
    end
    
    Then select is C1 or C3 the conditions are not specified. It causes an incomplete case which results in inferred latches for these two cases that latch on to output y.This occurs when some cases are not specified inside the CASE block .For example, if the 2'b10 and 2'b11 cases were not mentioned , the tool would synthesize inferred latches at the 3rd and 4th inputs of the multiplexer.
    
Solution is code case with default inside the CASE block so that the tool knows what to do when a case that is not specified occurs.

Correct code :

reg [1:0] sel

always @(*)

begin

     case(sel)
     
     2'b00: begin
     
                   . condition 1
		   
                   end
		   
     2'b01: begin
     
                   . condition 2
		   
                   end
		   
    default :begin
                   .
		   condition 3
		   
                   end  
		   
    end case
    
    end
    
 #  2.Partial assignments
 
 always @(*)
 
begin

	case(sel)
	
		2'boo: begin
		
			x = a;
			
			y = b;
			
		2'b01: begin
		
			x = c;
			
		default: begin
		
			x = d;
			
			y = d;
			
			end
	endcase
	
end

# 3.Overlapping cases

always @(*)

begin

	case(sel)
	
		2'b00: begin
		
			y = a;
			
		2'b01: begin
		
			y = b;
			
			end
			
		2'b10: begin
		
			y = c;
			
		2'b1?: begin
		
			y = d;
			
			end
			
	endcase
	
end

# Labs on Incorrect IF and CASE constructs

Example 1: Incomplete If statements

Below is the file titled incomp_if.v, and can be found in the directory verilog_files.

module incomp_if(input i0 , input i1 , input i2 , output reg y);

always @(*)

begin

	if(i0)
	
		y <= i1;
		
end

endmodule

The code contains an incomplete IF statement as no else condition corresponding to it is mentioned . On simulating this design , following gtkwave is obtained

$gvim *incomp* -o

![image](https://user-images.githubusercontent.com/123365758/215243083-68ae9dd9-8a05-47d4-913f-7f82abcd98fb.png)

![image](https://user-images.githubusercontent.com/123365758/215243471-3a652e8e-1fae-4418-8326-1b2a1174fc01.png)

From the above waveform, I observe no change in y when i0=0.It's equal to previous value when io=0. This shows latching Action, which is verified by looking at the synthesis implementation using Ysosys.

![image](https://user-images.githubusercontent.com/123365758/215244720-434a1731-f80a-4fa0-9047-1d48065a2819.png)

We see a D latch is created in the synthesized netlist.

Example 2:

Below is a similar example of incomp_if2.v

module incomp_if2(input i0 , input i1 , input i2 , input i3,  output reg y);

always @(*)

begin

	if(i0)
		y <= i1;
		
	else if (i2)
		y <= i3;

end

endmodule

The above code contains an incomplete IF statement as well. Here, I have 2 inputs i1 and i3, as well as 2 conditional inputs i0 and i2. As I do not specifythe case when both i0 and i2 go low,which results in an issue in the synthesis. The gtkwaveform of the simulated design is below

![image](https://user-images.githubusercontent.com/123365758/215247904-587351ec-7978-4a98-b60f-21387f94412b.png)

Observation: When io is high,output follows i1. When io is low,it looks for i2.If i2 is high,it follows i3. But if i2 is low(and io is already low),y attains a constant value=previous output.

This can be verified by checking the graphical realisation of the yosys synthesis below.

![image](https://user-images.githubusercontent.com/123365758/215285279-5b5fe8d8-d008-46cd-bc92-7d31e5965207.png)

Yosys synthesizes a multiplexer as well as a latch with some combinational logic at its enable pin.

Example3:

Below is a design with Incomplete Case's specification in a mux.

module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel , output reg y);

always @ (*)

begin
	case(sel)
	
		2'b00: y = i0;
		2'b01: y = i1;
		
	endcase
	
end

endmodule

The truth table for the above 2X1 mux looks like:

sel[1]	sel[0]	y

0	0	io

0	1	i1

1	0	latch

1	1	latch

Whenever se[1]=1 ,latching action takes place. The yosys synthesis implementation is given below.

![image](https://user-images.githubusercontent.com/123365758/215285531-7c36a941-85b2-40e5-a4cd-a7af439c3835.png)

Observation: 1. !(sel[1]) is going to D latch enable. 2.The inputs io,sel[0], !(sel[1]) go to the upper mixing logic that is implemented on D pin of the latch.

Example 4:

Complete Mux along with all the cases specified.

module comp_case (input i0 , input i1 , input i2 , input [1:0] sel , output reg y);

always @ (*)

begin

	cae(sel)
	
		2'b00: y = i0;
		2'b01: y = i1;
		default:y = i2;
		
	endcase
	
end

endmodule

Output follows i2 at default case,if i1 and io go low. Hence a 4X1 mux is synthesized without any latch that can be verified below.

![image](https://user-images.githubusercontent.com/123365758/215285774-0cdf4c36-86b8-40d4-a015-c9a8b7b550ab.png)

Example 5: Partial Assignments

module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel , output reg y , output reg x);

always @ (*)

begin

	cae(sel)
	
		2'b00: begin
			y = i0;
			x = i2;
			end
		2'b01: y = i1;
		default: begin 
			x = i1;
			y = i2;
			end
	endcase
	
end

endmodule

Expected Circuit: The 2X1 mux with output y is inferred without any latch. To find out the latching condition of the second mux we take the help of the following truth table:

sel[1]	sel[0]	x

0	0	i2

0	1	latch

1	0	i1

1	1	i1

Condition for enabling:

              en=sel[1]+!(sel[0]) 
	  
# Using Redundancy Theorem

Yosys implementation of the above design after synthesis,

![image](https://user-images.githubusercontent.com/123365758/215287801-e097395f-dab3-435c-805d-134d57200e6e.png)

As expected, Only 1 D latch is inferred for X. No latch is inferred for y.

Example 6: Design of 4X1 mux having overlapping cases

module bad_case (input i0 , input i1 , input i2 , input [1:0] sel , output reg y);

always @ (*)

begin

	cae(sel)
	
		2'b00: y = i0;
		2'b01: y = i1;
		2'b10: y = i2;
		2'b1?: y = i3;
		
	endcase
end

endmodule

In gtkwaveform of RTL simulation:

![image](https://user-images.githubusercontent.com/123365758/215288139-3fd93039-f675-4f35-a787-452096d067c5.png)

![image](https://user-images.githubusercontent.com/123365758/215288232-03283967-2139-41d4-b362-e183870cb3e3.png)

Observation : When sel[1:0]=11, the output neither follows i2 nor i3. It simply latches to 1.

Whereas while running GLS on the netlist,the waveform of the synthesized netlist behaves as 4X1 mux as shown below.

![image](https://user-images.githubusercontent.com/123365758/215288553-5495b7f1-aa57-43ac-9e22-2b5481fdadf6.png)

Thus ,Overlapping cases confuse the simulator and leads to Synthesis-Simulation Mismatches.

# Introduction to Looping Constructs

There are two types of FOR loops in verilog.

1.FOR loop 1.Used within the always block 2.Used to evaluate expressions

2.Generate FOR loop 1.Only used outside the always block 2.Used for instantiating hardware

# Necessity of FOR loops

For loops are extremely useful when we want to write a code /design that involves multiple assignments or evaluations within the always block. Lets us take an example: If we want to write the code for 4:1 multiplexer, we can easily do so using a either four if blocks or using a case block with 4 cases,as seen in the previous if-else blocks.But this approach is not suitable for complicated design with numerous inputs/outputs say 256X1 mux.If we wanted to design a 256X1 multiplexer, we will have to write 256 lines of condition statements using select and corresponding assignments. But in for loop ,be it 4X1 or 256X1 we would always be writing 4 lines of code only. Although we need to provide 256 inputs using an internal bus.

integer k;

always @(*)

begin

	for (k = 0, k < 256, k= i  +1)
	begin
		if (k== sel)
		
			y = in[i];
			
		end
	end
end

This code can be infinitely scaled up by just replacing the condition i < 256 with the desired specification for our multiplexer.

Similarly, I can create High input demultiplexers as well.

integer k

always @(*)

begin

	int_bus[15:0] = 16b'0;
	
	for (k= 0; k< 16; k= k+ 1) 
	
	begin
		if (k == sel)
		
			int_bus[k] = inp[k];
		end
		
	end
	
end

Here , I have created a 16:1 demultiplexer using for loops within the always block. The int_bus[15:0] specifies our internal bus which takes on the input of the demux. It is necessary to assign all outputs to low for a new value of sel else latches will be inferred resulting in the incorrect implementation of our logic.

Below are few of the examples of FOR construct .

Example 1:

file mux_generate.v that generates a 4X1 mux using For loop.

module mux_generate (input  i0, input i1 , input i2 , input i3 , input [1:0] sel , output reg y);

wire [3:0] i_int;

assign i_int = {i3,i2,i1,i0};

integer k;

always @(*)

begin

	for(k = 0; k < 4; k=k+1)begin
		if(k == sel)
		
			y = i_int[k];
	end
	
end

endmodule

The 4 inputs get assigned to a the internal 4 bit bus named i_int.

![image](https://user-images.githubusercontent.com/123365758/215288930-ba16c2c9-c2f3-4d67-9c8f-7f79655ed144.png)

The gtkwave obtained after the simulation.

![image](https://user-images.githubusercontent.com/123365758/215289145-c15c1adb-6f0e-4b65-a220-a944ae166898.png)

Example 2:

Similar to example 1, file demux_generate.v that generates a 4X1 demux using For loop.

module demux_generate (output o0 , output 02 , output o3 ,  output o4 , output o5 , output o6 , output o7 , input [2:0] sel , input i);

reg [7:0]y_int;

assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;

integer k;

always @(*)

begin

	y_int = 8'bo;
	for( k = 0; k < 8; k++) begin
		if(k == sel)
			y_int[k] = i;
	end
	
end 

endmodule

The above code has good readabilty,scalability and easy to write as well. Let's verify if it functions as a 8X1 demux as expected by viewing its gtkwave simulated waveform.

![image](https://user-images.githubusercontent.com/123365758/215289528-8cc9b5d9-b6f8-412a-bd88-39cdc036cbcd.png)

![image](https://user-images.githubusercontent.com/123365758/215289618-21e910b0-91e6-478d-830b-f3091fbb3224.png)

![image](https://user-images.githubusercontent.com/123365758/215290597-de09b76a-4648-408e-8683-3a12b334727b.png)


# FOR Generate and its Uses

FOR Generate is used when I needto create multiple instances of the same hardware. I must use the For generate outside the always block.

I take example of a 8 bit Ripple Carry Adder(RCA) to understand the ease of instantiations provided by the For generate statement. An RCA consists of Full Adders tied in series where the carry out of the previous full adder is fed as the carry in bit of the next full adder in the chain. Hence, I can make use of generate for to instantiate every full adder in the design , as they are all represent the same hardware.

For this example , I use the file rcs.v which holds the code for the ripple carry adder. It also needs to be included in our simulation.

module rca (input [7:0] num1 , input  [7:0] num2 , output [8:0] sum);

wire [7:0] int_sum;

wire [7:0] int_co;

genvar i;

generate

	for (i = 1; i < 8; i=i+1) begin
	
		fa u_fa_1 (.a(num1[i]),.b(num2[i],.c(int_co[i-1],.co(int_co[i]),.sum(int_sum[i]));
	end

endgenerate

fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));

assign sum[7:0] = int_sum;

assign sum[8] = int_co[7];

endmodule

Here, fa references another verilog design file containing the definition of for the full adder submodules .This is shown below, from the fa.v file

module fa(input a, input b , input c,  output co, output sum);

	assign  {co,sum} = a +b + c;
	
endmodule


$ gvim rca.v fa.v -o

![image](https://user-images.githubusercontent.com/123365758/215290267-23031877-5166-499d-82b1-f52c7dbea65b.png)

In the RCA verilog code, we instantiate fa in a loop using generate for outside the always block.

Rules for addition :

N + N bit number --> Sum will be N + 1 bits N +M bit number --> Sum will be max(N,M) +1 bits

Now, let us simulate this design in verilog and view its waveform with GKTWave .As the rca design referances the file fa.v , we must specify it in our commands as follows

iverilog fa.v rca.v tb_rca.v

./a.out

gtkwave tb_rca.v

the resulting gtkwaveform is shown below that shows an adder being simulated:

![image](https://user-images.githubusercontent.com/123365758/215290807-549c1b57-ed67-4824-8a83-bdb9e27b0f8d.png)













































































