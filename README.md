# vsd  workshop
DAY1 VSD WORKSHOP


Implementation details of DAY1
Day1 we were introduced to OpenLANE and how to use it and we ran the design picorv32a we checked the reports that is stat reports and synthesis as well.

The first task was to calculate flop ratio .

1)First navigating to the OpenLANE open source software which is used for complete RTL to GDS flow of an integrated circuit.

![WhatsApp Image 2024-03-30 at 11 34 43 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/59b818f7-ad0e-4bcb-9910-6921934eb1a3)


2)Then preparing design for synthesis,and we are using the design picorv32a.

![WhatsApp Image 2024-03-30 at 11 35 44 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/5fcfb131-ccc5-4786-ad9b-edcdcc11347d)


3)Ran synthesis successfully

![WhatsApp Image 2024-03-30 at 11 37 44 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/949cb11c-c5df-4db9-844d-524ea806f1e5)



4)flop ratio= Number of DFF/Total number of cells
percentage=flopratio*100

![WhatsApp Image 2024-03-30 at 11 43 10 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/4ca9cd14-3caa-4bdc-9159-ab511955f3b5)
![WhatsApp Image 2024-03-30 at 11 44 51 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/06fdb093-316b-4842-ad47-bb92c68ad75a)


flop ratio=1613/14876
flop ratio=0.108429
percentage=10.84

















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
![WhatsApp Image 2024-03-30 at 10 44 46 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/cd831bc7-19e1-44a2-843b-ff5fcc45f0a4)



THE COMMAND TO RUN IS run_placement

2)Next number of created techniology layers and library cells are displayed ,and core area and width is also displayed

![WhatsApp Image 2024-03-30 at 10 34 54 AM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d32b58a6-a9c1-46ce-9b5e-ef98ee05fe82)


4)How many original rows ,endcaps,tap cells inserted are also shown 

![WhatsApp Image 2024-03-30 at 10 34 55 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/2046e503-2b8f-47bf-b557-1a3b16b274bc)


Run floorplan was successfull

![WhatsApp Image 2024-03-30 at 10 34 55 AM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/a6f52add-3d40-426e-9c23-77e7b0c4d6c5)


5)Then the new one floorplan definition gets added and it looks as shown below

![WhatsApp Image 2024-03-30 at 10 34 55 AM (2)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/4ec94ccd-0732-4a66-8d88-924add4c2d69)



6)Next to look at the layout we need to open magic software which will display the layout and we can see that all the tap cells are inserted and input and output pins as well we have left click and right click and press z to zoom out the area whereever you want and then to select the particular component move on iot and press s then it will get selected and in Tkcon.tcl we can give command what and it will display as shown below

![WhatsApp Image 2024-03-30 at 10 39 35 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/1f28a274-dc35-4134-8b67-25f53a051ea9)
![WhatsApp Image 2024-03-30 at 10 40 28 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/5dbfe665-e15a-40e6-ac44-fa99e05048be)
![WhatsApp Image 2024-03-30 at 10 42 51 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/28aa237c-b585-4a55-bc84-ca52be950279)


7)Next step is the placement of netlist on the floorplan ,placement is done in two steps  1)global placement 2)Detailed placement
in the global placement the cells are roughly placed on the floorplan here the main reason for this global placement is wire length,where as legalisation occurs in detailed placementwhere the overlap between the cells is minimized 

.command is run_placement.

![WhatsApp Image 2024-03-30 at 10 37 43 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/cfb1279c-1b06-4254-92ec-7e0fd7f6abb9)
![WhatsApp Image 2024-03-30 at 10 43 31 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/2ec1d2e5-d074-47da-82ad-d6522d59e900)




As we can see all the cells are placed on the floor plan 

Next we proceeded with cell design flow ,consider the example of inverter all the standard cells are placed in the library and different functionality of the same cells are also placed,which varies in the size,resistance.To design the particular cell there are three steps inputs,design steps,outputs.

In inputs we take it from the foundry DRC & LVC rules,spice models and user defined specifications
Design steps we do circuoit design that is transistor level and layout design and characterisation which gives information about timing,power,noise which are the outputs
layout gives LEF,extracted spice netlist(.cir)

next we saw the 8 steps  considered in the characterisation flow and these are fed to GUNA software which will give results or information about timing,noise,power.
8 steps are as follows 
1)To read the model of NMOS & PMOS that is given by foundry.

2)To read the extracted spice netlist.

3)understand the behavior of the design.

4)Read the subcircuit of the design.

5)Attach the necessary power sources.

6)Apply the necessary stimuls to the design (Vpulse etc).

7)To provide necessary output capacitance.

8)necessary simulation commands like (.trans).

.Next we moved to timing characterisation that is propagation delay(50% input and 50% output) and transition of the output(20% to 80%) .








