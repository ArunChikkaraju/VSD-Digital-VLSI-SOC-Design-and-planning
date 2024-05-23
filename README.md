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




  

An in-depth paragraph about your project and overview of use.

## Getting Started

### Dependencies

* Describe any prerequisites, libraries, OS version, etc., needed before installing program.
* ex. Windows 10

### Installing

* How/where to download your program
* Any modifications needed to be made to files/folders

### Executing program

* How to run the program
* Step-by-step bullets
```
code blocks for commands
```

## Help

Any advise for common problems or issues.
```
command to run if program contains helper info
```

## Authors

Contributors names and contact info

ex. Dominique Pizzie  
ex. [@DomPizzie](https://twitter.com/dompizzie)

## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under the [NAME HERE] License - see the LICENSE.md file for details

## Acknowledgments

Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)
