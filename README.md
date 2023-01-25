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











