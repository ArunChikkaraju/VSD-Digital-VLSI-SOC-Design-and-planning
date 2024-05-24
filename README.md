# VSD-Digital-VLSI-SOC-Design-and-planning



## DAY-1 

We will see how to do synthesis for the particular design picorv32 using the openlane flow and generate the netlist and other necessary reports after the synthesis step

* First of all,we need to make sure that the virtual machine is working
* If everything is fine we can see a terminal inside the machine like this

  ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/4f6d2d99-f51a-42ac-85a2-e7f9a89e492f)


* We need to go to this path Desktop/work/tools/openlane_working_dir/openlane Before doing the further steps
* Then we need to type docker command

  what is docker exactly?
  Docker is a tool that simplifies creating, deploying, and running applications in containers. For example, with OpenLane, an open-source VLSI flow, you can package the 
  entire OpenLane environment and its dependencies into a Docker container. This container ensures that OpenLane runs consistently on any machine, avoiding the hassle of 
  installing and configuring the software manually. Docker images act as blueprints for these containers, making it easy to share and replicate the setup. This guarantees a 
  smooth and consistent experience across different development stages and environments.

* so,after running the docker command we can see the terminal like this

  ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/0e61f010-0623-4ff8-bac4-dfee141a2a50)

* we need to run the ./flow.tcl script -interactive where there are commands which explains how the various tools in the openlane should interact with eachother and all the information about how to run the flow in an organised manner
* And regarding the switch in the above command it is specifically mentioned that it should be an interactive mode means instead of automating the entire flow at once we can run the commands in a sequential order.
* After the tool got invoked we see the terminal like this

  ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/65681db6-ae51-4a5c-8eb5-f694961749c8)

* we should run these two commands before going for the synthesis step
  package require openlane 0.9
  prep -design picorv32a


  ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/675a9c6a-f53d-4b39-8bac-c084e5d96857)


* After running those above two commands we can see the runs directory is created where the results after every intermediate results are stored in a structural way

  ![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/376b6329-be5f-4c27-b4bc-5b4bbb0779b4)

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





## Day 2

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

![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/2febfec5-bc0e-42aa-9429-fe6d4c7eda35)


![image](https://github.com/ArunChikkaraju/VSD-Digital-VLSI-SOC-Design-and-planning/assets/169176599/f61fe1dc-307a-418f-a705-7776d083d96b)

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

```
magic -T /home/desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def & 






