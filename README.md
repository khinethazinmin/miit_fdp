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


yosys> dfflibmap –liberty ../lib/sky……

yosys> abc –liberty ../lib/sky……

yosys>show

![image](https://user-images.githubusercontent.com/123365758/214757276-69fdd77d-dc57-4651-af4d-22803633afdf.png)

yosys> read_verilog  dff_const2.v

yosys> synth –top dff_const2

![image](https://user-images.githubusercontent.com/123365758/214757838-17fc4d3c-20bd-4f97-b9a3-5e956be4be6e.png)

yosys> show

![image](https://user-images.githubusercontent.com/123365758/214758188-f2c5caf5-202b-4616-8e9e-c80617aba702.png)

yosys> read_liberty –lib ../lib/sky…..

yosys> read_verilog counter_opt

yosys> synth –top counter_opt

![image](https://user-images.githubusercontent.com/123365758/214773176-6878b02c-7f19-490d-95eb-cd71ca27e10b.png)










































