# VSD-Digital-VLSI-SOC-Design-and-planning



## DAY-1 

We will see how to do synthesis for the particular design picorv32 using the openlane flow and generate the netlist and other necessary reports after the synthesis step

* First of all,we need to make sure that the virtual machine is working
* If everything is fine we can see a terminal inside the machine like this

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3d816dbc-c4d5-4999-9db5-12964e52ac60)



* We need to go to this path Desktop/work/tools/openlane_working_dir/openlane Before doing the further steps
* Then we need to type docker command

  what is docker exactly?
  Docker is a tool that simplifies creating, deploying, and running applications in containers. For example, with OpenLane, an open-source VLSI flow, you can package the 
  entire OpenLane environment and its dependencies into a Docker container. This container ensures that OpenLane runs consistently on any machine, avoiding the hassle of 
  installing and configuring the software manually. Docker images act as blueprints for these containers, making it easy to share and replicate the setup. This guarantees a 
  smooth and consistent experience across different development stages and environments.

* so,after running the docker command we can see the terminal like this

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/080b93ca-9044-4e16-a1c5-dd3095b5ad53)


* we need to run the ./flow.tcl script -interactive where there are commands which explains how the various tools in the openlane should interact with eachother and all the information about how to run the flow in an organised manner
* And regarding the switch in the above command it is specifically mentioned that it should be an interactive mode means instead of automating the entire flow at once we can run the commands in a sequential order.
* After the tool got invoked we see the terminal like this

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c4f4163d-1baf-4d46-8d4e-a209736e20bf)


* we should run these two commands before going for the synthesis step
* package require openlane 0.9
* prep -design picorv32a


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/6c811fb3-4446-4e43-8060-9c0656413f59)



* After running those above two commands we can see the runs directory is created where the results after every intermediate results are stored in a structural way

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/4e0e3904-7330-4607-a904-8eb3be969905)


* Now we are good to go to run the synthesis and generate a netlist out of the design using the command run_synthesis

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/e2ea5c2b-5f7b-4b11-976c-8725032c5f46)


  ### Task-1

  we need to find the dflip flop ratio

  * In the netlist generated we can the dflipflops are mentioned as dfxtp_2

    ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/50879754-30e9-4cb8-b211-e4775fdae22f)

  * if we observe there are 1613 cells are there which are dflipflops
  * And there are total 14876 cells 


    ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/363c2dbe-2cfa-4818-bfd8-7aac5bd38fab)

  * so based on that if we calculate the ratio it is around 0.1084 which is nothing but approximately 10.8 percent out of the total cells





## DAY-2

* So far in the day 1 we have understood about the agenda of doing workshop and the glimpse of the openlane and about the different tools involved in it , finally by taking the example of the existing design which is picorv32a we have generated a netlist from the design by doing the synthesis step.
* Now we need to concentrate on the floorplanning and placement of the specified design

### Floorplanning

* Before actually incorporating the netlist generated in the physical hardware die we need to specify the dimensions of the core and die and also there are some macro steps  involved in the floorplanning itself those are
 
1. Define the dimensions of the core and die.
2. Define the location of pre-placed cells or macrocells.
3. Surround pre-placed cells with decoupling capacitors.
4. Perform power planning.
5. Place pins.
6. Specify logical cell placement blockages.

* By using the command run_floorplan the floorplanning for our design will be done successfully based on the different attributes or parameters covering the above minute steps mentioned in the .tcl file

* So basically if we observe the readme file in the configuration directory we can able to see various switches which can be used at each stage of the design flow


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/d8992f2a-fe31-46dd-953b-29fde9fd5221)


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/cf6ec5d3-10dc-4ac2-9371-e6020cae9dcf)

In the above picture for example we can see the switches for the aspect ratio and the utilization factor which are primarly responsible for determining the core and the die area like that all these switches are set to with some values in their respective .tcl file according to the design

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/ed95b254-3eea-4ae2-a352-36a88e739187)



![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c953190b-8e9a-4a83-aa09-abc11e85f30a)


we can see that all the switches are assigned with some default values

Based on out requirement we can the values of the switches accordingly otherwise the default values are set

* After the command run_floorplan if the floorplanning is successful then 
The terminal will be like this

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/1531eb99-dcce-4b01-85f0-558818443b38)


* Once the floorplanning is done we can able to .def file in the design directory which tells about the implemented floor plan details

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/50d00ed6-347e-4ed0-8845-27adc39e7df7)

### Task
Q) In the def file convert area into micrometers
In the def file the die area is in micron units 
1 micron = 1000 data base units
If we divide those parameters { 0 0 } { 660685 671405 } / 1000 we get dimensions in micrometers

we get length as 660.685 micro meter 
we get width as 671.405 micro meter

* We can visually see the constructed floorplan for our design using the magic open source tool .For that we need to type the command


magic -T /home/vsduser/desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def & 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/0a938481-a847-4f14-a349-c78bcfaf9843)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/517e7896-11ac-42e1-b82f-4696ce2b8a30)


* press s and v to select the entire layout and bring to the center of the screen and to zoom to the particular part of  the layout press left click create a box where you want to see the layout in detail and press right click to lock the box now press z

* so if we zoom further we can see the pins clearly select any particular pin by clicking on the s and we can observe the other window called tkcon where the description the selection pin is seen when we type “what” on that terminal

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/8526e63b-b4c4-4ee1-8973-db7055434861)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/639ea7e1-6456-4bdb-80bb-2d3d096586be)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3fc14c22-5f84-4a2a-bf00-5d26c69fc6d9)


### Placement

* The next step in the design flow is to embibe the netlist to the floorplan which we have created just now
* For that we need to type the simple command run_placement
* After executing we can see the terminal as


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/79577b70-9fd7-4108-a97b-f8a6c5c5e6e9)

* Now its time to see the placement visually through magic tool



![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9f336bab-040c-4d87-bc41-10ae58696e2e)


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/a2a9e286-0b10-4740-9bc0-d5179b7cdcfb)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/88871966-6026-4b9c-bafe-ab5d3ae8e3d1)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/e2e54838-1880-4635-820a-9ae0b98a3ee6)




## DAY-3

* So far we have done upto the placement stage 
* In order to understand the library characterization we will concentrate on the one simple cell lets say inverter and we will extract the information related to the timing by doing the transient analysis
* Finally we will try to place that cell in the existing design picorv32a and see whether it happens or not

### Lab steps to gitclone the VSDSTDcell Design

* we will take an example of the simple cell which is inverter and try to insert that cell in the picorv32 design
* Before that we need to understand about the cell deeply
* There is a github repository where the complete details of the inverter cell using skywater is explained in it
* we will try to clone that repository in our local system


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9753e59a-f1a1-4898-8eb9-231d19e4b677)

* copy the github link and paste it in the terminal along with the git clone command

* now go to the openlane directory and type the command "git clone https://github.com/nickson-jose/vsdstdcelldesign.git "
* Once it is cloned we can see the creation of directory named “vsdstdcelldesign”

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c9688fcd-639b-4cb0-81cb-c4c105f46ccb)

* Before playing around with the properties of the inverter cell if we observe the .mag file to understand the layer structure used for designing inverter layout
  
* In order to open the .mag file we need the .tech file which is available inside the the pdks directory so we need to copy that and paste in the present directory

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2981e89b-5841-45c0-a0df-8f6e51675605)

* Now we can see that sky130A.tech file is copied in the present directory

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2e2ddeee-4f07-4488-9dbf-cb414557a4ba)

* Its time to visually see the layout of the inverter / std cell by using the magic tool with the command

* magic -T sky130A.tech sky130_inv.mag &

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c8c7c4af-a693-4e49-8b56-d6743974c7a2)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/78bc578b-d3c4-47bf-a496-612f12142c4b)

* On the right side of the magic tool we can see the colour palette which is nothing but the different metal layers indicators and if we place the mouse pointer to any particular that selected layer name is displayed on the right top

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b0832c11-fff7-4373-bd44-b51a71d82c4e)

### checking whether the layout performs intended inverter functionality


nmos
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9e32a534-e9f7-4033-a6e3-52fa00464eb0)


pmos
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b52f6446-1b7f-4e82-a10d-2adedcbb658a)


drain of pmos and nmos connected to out
![Screenshot 2024-05-28 142513](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/de8190fd-5c7c-4c79-9238-dc6c581728f3)

source of pmos connected to vdd
![Screenshot 2024-05-28 142740](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2bb86b09-2b84-4ac9-a5ae-05172dc8536a)

source of nmos connected to gnd
![Screenshot 2024-05-28 142844](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/bad1a7ea-ceda-436d-8244-617246d254f0)


extract all command to extract the layout to spice
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/4f772f4b-1d46-4f05-9c6a-b421806a2920)


checking whether external file created
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9a171dfe-5a54-4edc-ab03-42c143870601)


ext2spice command 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/37404204-bd59-4937-a2a3-b26214e727ab)


spice file created
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/675954ca-bc5a-40d4-8c92-08968a6ed78d)



checking the unit cell size which is 0.01u
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/f4aefc39-1b4c-4923-9048-2ef8a834e08f)


editing the netlist according to our requirements
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/12cd44f7-906e-4dfa-89c3-d3de13441be0)


invoking the ngspice tool
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/f937a290-31c9-4072-b7ad-464baad99e5b)


changing the capacitance value for smoother transistion of signals 
*c3 to 2fF
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/aed0a7b3-21d7-45db-80fa-610e4a76ddc6)


transient analysis of the graph
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/64dcca4b-76d9-4929-9278-e674029faa86)

* 80 percent of 3.3 is 2.64
* 20 percent of 3.3 is 0.66

rise time 20% transistion of output
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/91c2a0c7-a657-4bf0-9061-2f35fea66052)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9b143b7e-4f55-4b27-aa21-2cda36807e53)

rise time 80% transition of output
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2e000840-bb08-4ac2-9e3f-6a2eeb81af1b)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/279304c8-7f93-4cba-963b-edc3342786d0)

fall time 80% transistion of output

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/cd71a8c1-03ec-4998-9879-d2c91fda83bc)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/22cd3cda-d54e-4af8-bb0f-3c3cc722aa42)

fall time 20% transistion of output
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c21ad5e8-ff7a-451a-9835-d19f63f9769c)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/4f932fa6-a63c-4003-9f10-d052f475328b)

50 percent of 3.3 is 1.65

input fall and output rise

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/307022d3-c0a6-4fd0-9cd3-5487b0578b82)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/6e7a4f81-e15f-4a1e-9ca0-e4e389cc638e)


output fall and input rise

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b749d814-bc65-492d-8462-44ae43ef76af)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/eea9906c-0db6-432b-bf66-eb5492a268c2)




 ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/aabd980d-6977-48e5-b16a-9913ef6af98f)



* After extracting the zip file drc tests go to that directory and observe the files in it

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/30c9adde-adb4-464c-8bc8-2ea659a13fc0)

 
* We can see various .mag files with errors in it which helps us to understand the DRC rules


* Now invoke the magic tool with the command magic -d XR & and open the net3.mag inside the tool
 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/d6b7e534-6130-41e4-898b-a563792a28bd)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/5bcb4b71-8cf5-45ff-afab-b3b50a8985a5)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/f62392c8-69b6-4a12-a4dc-3ca07bac0d2f)

* Now in order to see the DRC errors select the entire design by pressing S and open the tkcon window and type “ drc why “ 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c631afe4-b9b7-4b09-8fd6-124a76ae69cd)

 
* We can able to see some errors with the description as well
* In order to understand about that violations in detail we need to go to the website google skywater documentation
* In that we need to select design rules and then the periphery rules to see the description of the rules for each layer in skywater 130 pdk
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9cbc8eef-029a-4857-b2c1-1c565b6211e3)


* Now based on the errors generated in the tkcon window we can see the description of those errors in the documentation
 
 ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/8dd333a6-f042-4b53-b710-3f942b976554)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/bab237df-6378-456d-b1b3-4107dcff543c)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/122d0be1-ce81-498e-bb37-d338a21a919d)

 ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/069abb64-4008-4c20-834e-448ce5ae339b)

 


* Create a empty box like this
  
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/69e888cb-ce1a-4e85-9807-b37cbd496f50)

 
* Place the mouse pointer at m3 contact and click on the p to paint it in the box which we have created

  
 ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/7ea891bd-70da-44d4-997c-ff4b21cf8fe6)

 ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/bcc520b5-b911-4445-a0d4-374ae381a6e2)


* Then in the tkcon window press cif see VIA2 to see like this
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2e770149-31f5-443c-8c26-50563f51ac44)


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/7317f777-7bd0-45c8-b34b-4d65bef94051)



### Lab exercise to fix poly.9 error in Sky130 tech-file

* Open poly.mag file
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/e195a015-39b2-4a99-bb62-4256bec0c8a9)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9b48e264-c761-4f00-97c9-7b7efcac5f36)

* We can see that there are so many problems in the .mag file if we consider one particular problem which is poly.9

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/e75e50f5-4930-4056-871d-bb73dad16aaa)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/6f350da2-384d-4fa4-b710-98232959109e)


* We can see clearly that the spacing is less than required 
* Required : 0.480um
* Actual: 0.320um

* To debug this problem we need to inspect the file sky130.tech Search for poly.9 which is the problem we are interested in There are two instances in a file where poly.9 is found

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/55bd769f-8e69-4b9f-af63-3942b5d44e7c)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/27ac69d8-05bc-441b-b1db-cd669b3ffc8b)

 
* Added these lines
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/a5159ba6-2633-4a98-a27d-1b221dd13def)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b5c2d774-9638-40c5-8cf9-4d6eba6ae615)



* After saving the file in the tkcon window load the tech file and run drc check again

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/4bfca793-0878-4147-972d-d4123f27271d)



### DRC error as geometrical construct

* Load nwell.mag and see for errors after that run the below commands

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/548b7f4b-e3b2-4514-ad24-25fb76509fc4)

 
* In order to rectify the errors open the tech file
  
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/5ad61392-d924-437c-bdba-01d32613a4cf)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9a49dfdc-e90d-4e26-86e8-88a0767a3bce)

 
 
* Added lines in the tech file
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/11864a0e-5b27-411e-b30d-1e6cb2a4d56a)


## DAY-4

* So far we have done with the design setup , floorplan , placement and finally learned about the stdcell characterization using the mag file
* For the placement of the new cell in the existing design we may not need the all intricate details ( mag file)
* Only information is needed is about the boundaries pwr,gnd,out ports
* That’s where lef file is generated which is gives the overview of the cell 
* By doing this one can secure the IP (Intellectual property) by hiding the exact details and showing the necessary details only
* First of all, we need to check for the std cell guidelines
*	The input and output ports must lie on the intersection of vertical and horizontal tracks
* The width of the standard cell must be the multiple powers of the track pitch 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/e49d157c-2f47-47ca-9c83-81f18ce62c35)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/5d928d13-0157-47a7-850c-8a715b93a2dd)

 
* Now open the inverter layout again then press g to enable the grid 
* Change the grid dimensions according to the dimensions mentioned in the layers.info
* Format of grid command
* grid x-spacing y-spacing x-orgin y-origin
* so the command will be grid 0.46 0.34 0.23 0.17

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/a23e7340-f400-47af-9d07-cddc02f6e71e)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/02a50b13-7334-4c5f-8fc1-f3339abc1628)



* We can see that the input and output ports must lie on the intersection of vertical and horizontal tracks
  
* Saving those changes as a file name sky130A_vsdinv.mag

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/959499d2-961d-44a9-b6e7-48967f171f17)



* File is created and the layout is opened
  
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/a56fb323-fc90-46a7-808b-fd96c7adca34)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/ee505947-c43f-4294-9900-04f2a3335b39)
 


 
* With the above command “lef write” lef file is created 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/7f67898a-ef76-4eee-a890-d886c7676c27)


* Glimpse of lef file
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c2391823-0a11-4bfc-9b87-1d7dc7bb3edf)


* Now based on the lef file we will insert this cell into our design picorv32
  
* Before that copy the lef file into the design src directory


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3e168e8c-d93b-43e5-b9c4-abd681c83fb0)

 ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/bf632b88-0573-4d95-bc2b-12ee248c0aad)
 

* Also copy the libs as well to the design source directory
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/7116156b-e9dc-4a42-8daf-63dd2f408be7)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/80ae0f85-e0f7-482e-a361-206e346e0e4d)


* We need to edit the config.tcl file
  
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/9696f2e4-3947-4882-a787-636a0741986d)

 
* After including the necessary lines the config.tcl file will be like

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/bc86a1ee-98f1-4c78-bc9b-63a5684311ba)


* Now we run the synthesis again but now with the added lef 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/47578f84-bbdf-42d3-bcfd-2904e6b615b7)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/74466707-6c0a-4f1b-b906-6f6979b4326a)



* After running the synthesis

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3f9e135c-3c3a-4622-9607-9b7e105cf07d)


 
* Although tns and wns was slightly decreased that was not a good results so we need to do something with respect to the timing
* Hence we will try using the synthesis strategy switch and see whether delay is reduced or not

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/34be9d4a-2cc3-4b67-99b3-4271bb019685)



* Now if we run the synthesis step again

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/583b98c3-11ff-43d3-9a1d-1e8b7f81e4ce)

* We got the zero delay

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/819feb6e-74e7-4438-9903-7306d67f5768)

* With tradeoff of increase in the area


* I have noted down the values of area and delay before and after modifying the switches

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/784e2f4b-e4a7-4b50-a285-525b9ab90b5e)

 
* Area got increased and delay was reduced a lot

* Checking whether the inverter cell is embedded or not by seeing the merged.lef

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/a21adc9a-8f5d-4d33-b74b-463bd28bdb07)

 
* Now we can confirm that the lef file is involved in the lef file


* Then execute run_floorplan

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3d34101b-62fd-4932-a07a-744b67a1f9d2)

 
* We got an issue with the floorplan 

* So we need to execute these commands in order to resolve this issue

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/58c47103-7c3f-420b-99e9-6431cd7c4872)


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3937bd85-9604-4817-a5a7-49c3359c5e72)


* Now its time to run the placement
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/ae79ade1-b30a-4a60-9167-1386acab1f14)


* Placement delay

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/f57b7ea9-6ca3-47bf-9208-fec1b99077c9)


* After floorplanning We will get like this

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/c317ab71-a3f9-4724-9800-61aeb0d8b248)


* Now we can able to see the .def file created if we invoke the magic tool now to the layout after placement visually we need to do like this

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/8f9f236b-cf34-41f7-ab6d-3bc32bbe6857)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/cfc3c383-a1e8-43b9-9aae-522a12c38cb4)

 
* In the huge layout we can able to see the cell using this command

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/12eff90a-c2ab-4a82-bfdb-ee53c3b57c3f)

* Now its time to run the cts with the command run_cts

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2400a2fb-d7ae-47fb-ac1c-79a6d6d10bc0)

* minimum path delay
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/66403a58-4182-4d37-9852-e95910f984cc)


* max path delay

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/f6732e45-2e6c-41e1-acda-23348ada0714)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/88c3de5f-a9e4-485f-8c5f-deaffb89160f)


* Cts completed successfully
  
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/de365bf4-9437-4837-9d1f-fe6f5396341b)

### Post cts timing analysis

* New sdc file created

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/342f25b4-4b67-4cff-88c7-d050dc8a2132)


 
* So basically we have initialized some switches related to timing some are direct parameters like CLOCK_PERIOD,SYNTH_MAX_FANOUT,SYNTH_CAP_LOAD etc.. and some are the derived parameters like input_delay,output_delay,cap_load etc…

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/ec4a8ec3-abd5-4aa4-8211-e577bb0462cc)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3dbfdf40-452a-4018-af3a-fb035e57279f)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/325e055e-cac7-46ee-ab4a-76d3f818447e)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b3c54f4e-cc46-4ecc-9ff6-5a22968e0680)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/88361629-23a1-4400-b1a9-5f0f92110317)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b06a8fa0-9152-4707-8e56-2c7e2659f9c2)

 
* Removing the clk_buffer 1 and doing the cts again

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/83246a18-1bb4-4543-8506-e3c26cd0835b)

 
* Post cts simulation with removed clock buffer 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/abc16c6b-f8ac-4ac0-a308-90cb87212a71)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b51d2423-d4ba-4736-8143-23604a8c1d12)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b9f137d6-9b27-4c27-9e7a-7521899f7c25)

 
* Earlier the slack was violated (-0.0745) now it is fixed 

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3fbdcd8f-d7fe-4dd7-aef8-b5f9b74e1012)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/75b59639-c831-416a-b8db-12c76f1188ac)
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/e9e7cca8-db2b-4848-8fc5-814e5f0dfbc4)
 
 
* Now inserting the clk buffer 1 again in the list
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/198943aa-b0dc-4138-a173-5cb306c17aeb)


### DAY-5

* As a part of the final day we will deal with the creation of PDN(power distribution network) and routing.
* 

### Generation of POWER Distribution network with command gen_pdn

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/ff0396bb-736f-48e0-919e-4d8e96ca0087)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/d47a92ee-100d-447f-912a-ababac4512ae)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/ee7c07ec-6e4c-4586-b337-dbefc0c7925c)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b896fa1c-8173-4262-baae-912bd45641af)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/0c653a56-0d55-432c-b7bc-ac474200ce13)

 
* Invoking the magic tool to observe the generated PDN for our design
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/10ed04e0-8052-48ee-8666-6965edbdf2c4)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/b2985d49-e02f-4314-a902-c6ce3c057e0c)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2736c43c-2a8a-44ae-b6de-9b9a573a05d5)

 
* Now we need to route all the cells for that we need to execute the below commands

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/64be3178-b7f8-4c54-878d-6b99b8505dcd)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/5f85bc92-ab66-409e-8836-8f9160f51624)
 
 
* Using the magic tool we will see how routing done for our design
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/6e6b0522-521e-4ada-a0e1-9027582bd38f)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/bd808d1b-6b89-488b-98de-7c28ee49349f)
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/76de99ba-e231-4759-9efa-651d9b55e3e2)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/0ddcf4d0-52e5-41da-b194-47d85e8f7ed2)


 * Fast route guide

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/0d633bc0-317d-4322-9e80-a2399174b43b)

 

* Fast route def file

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/0cc7c87e-8cd1-42d9-adef-62b6929de391)

 
### Post route parasitic extraction

* During the routing itself the spef file is generated 
 
![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/3ed68f37-09f6-46d6-bf69-46f85831d380)

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/d93d5dd7-6248-4126-a50b-f8b53e61931f)


* After going through upto routing we will get a snip of our design like this

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/cf7eb7c2-c69a-4b3d-856c-c49a54b3302f)




































