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


































