# vsd  workshop
DAY1 VSD WORKSHOP
Implementation details of DAY1
Day1 we were introduced to OpenLANE and how to use it and we ran the design picorv32a we checked the reports that is stat reports and synthesis as well
The first task was to calculate flop ratio 
we found out all the following results for design picorv32a
![WhatsApp Image 2024-03-29 at 8 30 17 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/bd1e2b59-4702-40d3-8536-26fd0d19ee17)

then preparing design for synthesis

![WhatsApp Image 2024-03-29 at 8 36 55 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/9a13661d-4f49-42b3-8622-1fdbe51ff370)

ran synthesis successfully

![WhatsApp Image 2024-03-29 at 8 37 56 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/02840799-0495-4ea7-9d16-1c237a3ad87e)

flop ratio= Number of DFF/Total number of cells
percentage=flopratio*100
![WhatsApp Image 2024-03-28 at 9 51 39 PM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/8248cd94-1e5b-480e-9653-8b7375a941de)

![WhatsApp Image 2024-03-28 at 9 51 39 PM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/d70cf74b-baba-4f95-8034-9b364fb2ed73)
flop ratio=1613/18036
flop ratio=0.0894322466178
percentage=8.9432


#DAY2 vsd workshop

THEORY

In the day 1 we learnt how to synthesise the design that is synthesis of  design  picorv32a was done.Next further continuing the next step in the physical design is floor planning and power planning.

.We understood the parameters used in floor planning like utilisation factor = Area occupied by the netlist/Area occupied by the entire core .Ideally utilisation factor =1,but practically utilisation factor of 0.5 to 0.6 is considered and the rest area is used for optimisation.
Then the other term is aspect ratio which is =height/width
if aspect ratio=1,the netlist occupied the core is in the shape of square,otherwise it is rectangle.

.To define the location of preplaced cells 
preplaced cells are the cells that are used in the design repeatedly ,so that logic is made in to the black box that is blocks and placed on the floor planning,whenever automatic placement and routing routing of the other cells wrt design happens they dont touch area that is occupied by preplaced cells.

.Power disrtibution :When there is only one source of power supply the circuit which is placed at far distance cannot get the 100 percent power supply because of presence of resistance,inductance parameters on the wire that is used for transferring the power so there comes the term decoupling capacitor,which is very closely placed to the design which decouples the design with the main power supply and the other problem that comes is it is not feasible to use more decoupling capacitors in the entire circuit design ,so the solution to this use of more and more power supplies so that the any part of the circuit can tap the power from the nearest source.

.Next step is placement of input and output pins on the die and the area between the core and area should not be occupied by any cells because that area is used for pin locations.

.Now next we proceeded with performing floor planning in the OpenLANE 
There first we check the floor plan default values  that is how much of core is utilised,aspect ratio ,verical metal layer,horizontal metal layer and then we need to check the values in the config.tcl file of the design picorv32a so the values present in this will take precedence of floor default values and the highest precedence is taken by sky130A config.tcl.

1)The following results are shown below.

![WhatsApp Image 2024-03-30 at 6 32 43 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/d5ffa223-1ae3-4e1a-98d9-1c2aaba91ab8)
![WhatsApp Image 2024-03-30 at 6 32 44 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/d58d118f-2527-4131-bf44-9eb3570ea661)


THE COMMAND TO RUN IS run_placement

2)Next number of created techniology layers and library cells are displayed

![WhatsApp Image 2024-03-30 at 6 32 45 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/2ed3dcf5-868d-447f-9bd3-45782213e562)


3)Core rea and core width are displaced

![WhatsApp Image 2024-03-30 at 6 32 46 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/aa878602-3ff5-4b4b-9173-cd6d883712e2)

4)How many original rows ,endcaps,tap cells inserted are also shown 

![WhatsApp Image 2024-03-30 at 6 32 49 AM (1)](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/008286bf-9277-49fa-ae04-9c242717cf46)

Run placement was successfull

![WhatsApp Image 2024-03-30 at 6 32 50 AM (1)](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/e00a6587-9b32-41e9-afae-f92b1d1c15a0)

5)Then the new one floorplan definition gets added and it looks as shown below

![WhatsApp Image 2024-03-30 at 6 32 51 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/0d311baf-e76d-4e19-9154-afea7f42e95a)

6)Next to look at the layout we need to open magic software which will display the layout and we can see that all the tap cells are inserted and input and output pins as well we have left click and right click and press z to zoom out the area whereever you want and then to select the particular component move on iot and press s then it will get selected and in Tkcon.tcl we can give command what and it will display as shown below

![WhatsApp Image 2024-03-30 at 6 32 51 AM (1)](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/137a2612-6b1c-4e7d-b482-e5be6e409e59)
![WhatsApp Image 2024-03-30 at 6 32 51 AM (2)](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/0f18333d-68ea-49ef-b2da-4f831ea31df5)
![WhatsApp Image 2024-03-30 at 6 32 52 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/2d8db2d5-a817-4eb6-b802-f8149b7e53e7)

7)Next step is the placement of netlist on the floorplan ,placement is done in two steps  1)global placement 2)Detailed placement
in the global placement the cells are roughly placed on the floorplan here the main reason for this global placement is wire length,where as legalisation occurs in detailed placementwhere the overlap between the cells is minimized 

.command is run_placement.

![WhatsApp Image 2024-03-30 at 6 32 52 AM (1)](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/6d9a8bcc-570d-4b67-b327-b327e81fc98e)
![WhatsApp Image 2024-03-30 at 6 32 52 AM (2)](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/2e1d5970-189c-4b1f-b3a5-537902f43a0f)
![WhatsApp Image 2024-03-30 at 6 32 53 AM](https://github.com/HarikaVeluru/Day1_vsd/assets/165346462/cab23d0d-9f06-4a8b-9ec1-e59172b741ca)


As we can see all the cells are placed on the floor plan 

Next we proceeded with cell design flow ,consider the example of inverter all the standard cells are placed in the library and different functionality of the same cells are also placed,which varies in the size,resistance.To design the particular cell there are three steps inputs,design steps,outputs.

In inputs we take it from the foundry DRC & LVC rules,spice models and user defined specifications
Design steps we do circuoit design that is transistor level and layout design and characterisation which gives information about timing,power,noise which are the outputs
layout gives LEF,extracted spice netlist(.cir)

next we saw the 8 steps  considered in the characterisation flow and these are fed to GUNA software which will give results or information about timing,noise,power.
8 steps are as follows 
1)To read the model of NMOS & PMOS that is given by foundry
2)To read the extracted spice netlist
3)understand the behavior of the design
4)Read the subcircuit of the design
5)Attach the necessary power sources
6)Apply the necessary stimuls to the design (Vpulse etc)
7)To provide necessary output capacitance 
8)necessary simulation commands like (.trans)

Next we moved to timing characterisation that is propagation delay(50% input and 50% output) and transition of the output(20% to 80%) .








