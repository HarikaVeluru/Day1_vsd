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


4)Results of the timing reports,command used is gvim <file_name>

![WhatsApp Image 2024-03-30 at 11 57 56 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/c091a56a-5e9d-4cd0-bbac-e4e004a0404b)



5)flop ratio= Number of DFF/Total number of cells
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


![WhatsApp Image 2024-03-30 at 10 40 28 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/5dbfe665-e15a-40e6-ac44-fa99e05048be)
![WhatsApp Image 2024-03-30 at 10 42 51 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/28aa237c-b585-4a55-bc84-ca52be950279)
![WhatsApp Image 2024-03-30 at 10 43 31 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/2ec1d2e5-d074-47da-82ad-d6522d59e900)


7)Next step is the placement of netlist on the floorplan ,placement is done in two steps  1)global placement 2)Detailed placement
in the global placement the cells are roughly placed on the floorplan here the main reason for this global placement is wire length,where as legalisation occurs in detailed placementwhere the overlap between the cells is minimized 

.command is run_placement.

![WhatsApp Image 2024-03-30 at 10 37 43 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/cfb1279c-1b06-4254-92ec-7e0fd7f6abb9)





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




#Day3 vsd_workshop

SPICE DECK 
component connectivity

![WhatsApp Image 2024-03-30 at 3 57 22 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/5794c061-bf96-415e-92fb-3845b285c67d)

![WhatsApp Image 2024-03-30 at 4 00 00 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/ba6c8400-0bf2-4285-9a2a-e04e6af2e2a6)

Identify nodes,between two nodes there will be a component.
                ***MODEL DESCRIPTION***
            M1 out in vdd vdd PMOS w=0.3754 L=0.254
            ---------------------------------------
            M2 out in 0 0 NMOS w=0.754 L=0.254

Here the order follows as (drain node,gate node,source node,substrate node)
Switching threshold is very important where Vin=Vout,and at this point both NMOS & PMOS both will be active and there might cause leakage of current.

16 MASK CMOS PROCESS
1) Selecting a substrate(where the layout of design is placed).
2) Next step is creating active region of transistors by photoresist.
3) N well and P well formation.
4) Formation of gate.
5) lightly doped drain(LDD) formation.
6) Source & Drain formation.
7) Formation of interconnects & contacts
8) Higher level metal formation
and the rest process follows with in all of these steps executed 16 masks will be used and photolithiography is the main technique.

Next step is adding vsdstdcell to our existing netlist 
so here directly we will use the existing github repo which already has vsdstdcell in it 
github link:https://github.com/nickson-jose/vsdstdcelldesign.git

![WhatsApp Image 2024-03-30 at 8 47 16 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d1b02e9f-0068-4ddf-9a09-0cafbdcec461)

And then in this lets open inverter layout in magic software which is mainly used for layout design

![WhatsApp Image 2024-03-30 at 9 00 08 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/dbfd0b9e-cf97-4261-84c0-cfe0932e6b72)

To place the design at the centere select the design and press v.

Then to understand what each component of the layout is select the respective part and in Tkon.tcl give the command "what".

![WhatsApp Image 2024-03-31 at 9 37 41 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/9bcab16d-9d87-42c9-ae1b-66e9ee01a6b3)

Then by using the command "extract all" we can extract this inverter to our design picorv32a which will have extension .ext as shown below.

![WhatsApp Image 2024-03-31 at 10 01 57 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f2006035-52f8-4d96-8397-5906aa9ad2cb)

![WhatsApp Image 2024-03-31 at 10 02 34 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/9d557a86-8a6f-4c4a-b121-ba3b1eab4a67)

Then we need SPICE file for that the following command is given.

![WhatsApp Image 2024-03-31 at 10 12 11 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/9332f548-dea4-4e24-baa7-3275399a0343)
![WhatsApp Image 2024-03-31 at 10 13 01 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/711b8925-59ec-4d1e-8a3d-52d53dff1452)

The SPICE file looks as shown below.

![WhatsApp Image 2024-03-31 at 10 14 53 AM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/a3b1a827-015f-426c-b513-21a4f2511b84)

Then to run this SPICE file we need to set up the ngspice as below.

![WhatsApp Image 2024-03-31 at 4 46 53 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/43d6d024-f955-4c5a-8be7-82d1050cadc6)
![WhatsApp Image 2024-03-31 at 5 26 04 PM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/901f6c4d-36ba-47cf-8f9c-45671893f1ab)


Then we can plot the output Y vs time t for the input "a".

![WhatsApp Image 2024-03-31 at 5 27 44 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/017ffb6a-16e7-4bd4-8ac5-755746e12bfc)

So now lets charactercise the cell we need to find rise time,fall time,propagation delay

RISE TRANSITION TIME 
![WhatsApp Image 2024-03-31 at 5 55 18 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/605e1205-6f7c-471d-92c1-bc5bca2f51f0)

0.04206 ns.

PROPAGATION DELAY 

![WhatsApp Image 2024-03-31 at 6 04 27 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/893fccb2-8f19-49a5-a426-0a151fc009fe)

0.0822ns.



Now next one is  to find out the errors in the layout for that we used the below githublink.
https://github.com/google/skywater-pdk

Now in the designs we can see drc_tests.tgz file.
![WhatsApp Image 2024-03-31 at 7 25 19 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/079f053c-777a-408d-b07c-5c7a58a36579)

In that a particular layout called as .magiccrc file.
![WhatsApp Image 2024-03-31 at 7 40 29 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/72dfeb08-c8fd-4dc0-9b47-f4e4db5f9752)

So next lets consider METAL layer layout.
![WhatsApp Image 2024-03-31 at 7 44 08 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/30418689-50de-4cd9-99cb-a216376e405c)
![WhatsApp Image 2024-03-31 at 8 03 34 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/6438b1b3-3a78-4504-895c-3ba9457ea9d2)
![WhatsApp Image 2024-03-31 at 8 12 09 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/60e60a4d-2726-4b1d-b794-756ad2643d23)
![WhatsApp Image 2024-04-01 at 12 08 01 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/547bedef-f64a-4db3-8a75-652d255d628b)
The above represents the metal contacts[BLACK CONTACTS].
![WhatsApp Image 2024-04-01 at 12 17 50 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d41f1071-3196-4e68-aa7e-ddb7c14d6530)
![WhatsApp Image 2024-04-01 at 12 18 10 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/3cc75231-963d-4d8a-9b19-ec0e1d0eaeba)
![WhatsApp Image 2024-04-01 at 12 23 55 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/01e21d88-2097-4f50-8a04-a475878022ae)
![WhatsApp Image 2024-04-01 at 12 40 58 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/249d3f31-9865-4ab9-8d1f-251ba56e507d)
![WhatsApp Image 2024-04-01 at 12 57 50 PM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/b7cea4ea-53ae-46af-88b1-504003f5dab1)
![WhatsApp Image 2024-04-01 at 12 59 53 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f8bfb6df-7d65-45c1-8d57-370ba26204e1)
![WhatsApp Image 2024-04-01 at 3 48 43 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/9c363aab-018d-49b0-babe-6dd3f1e0b894)
![WhatsApp Image 2024-04-01 at 5 29 26 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/e9da2b95-a826-40f3-90f2-da2487406e08)



Day4VSDworkshop


To place the standard cell that is placement & routing we need not have to place the entire layout we just need the inner boundary power and ground rails and all this information will be contained in the LEF file so we need to extract that file and we will be learning how to place the designed cell into the design picorv32a.
And the input and output ports must lie on the point where vertical and horizontal lines are met.
During plcement and routing we dont need info about the logic of the cell.
![WhatsApp Image 2024-04-04 at 6 48 12 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/dacad641-b3b1-49de-bf77-0ac9e297bf21)
![WhatsApp Image 2024-04-04 at 6 47 13 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/2a3ad2fd-10ba-4191-9ade-9e7b4d5192ea)
That means horizontal track is at an offset of 0.23 and with the track that is its spaced 0.46 units apart on the horizontal track.
Now we make the grid according to the tracking info.
The syntax is grid[x_spacing][y_spacing] [x_origin][y_origin].
![WhatsApp Image 2024-04-04 at 7 11 45 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/384df091-b2b3-4f47-a583-7ce6cb690f4f)
![WhatsApp Image 2024-04-04 at 7 14 53 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/3a637fca-1e39-4dc0-8039-0d4b788f3f52)

The width of the standard cell should be in the odd multiples of xpitch.

![WhatsApp Image 2024-04-05 at 6 42 05 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/cd183054-272e-4d02-82ab-00be7a169bff)
So if we consider peer boundary the distance between them is 3 times of Xpitch,that is width and the requirement is satisfied.

![WhatsApp Image 2024-04-05 at 6 49 48 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/a2d5f867-bc30-43f3-ac25-cb154cee6f79)

Height is even multiple of ypitch so requirement is satisfied.



Ports in the magic means nothing to it it is required while extracting the LEF file in layout it is all about defining the different  layers and metal contacts.

We can select the paricular part of layout and then edit text lower the label it will be first extracted in LEF file.
And after this we need to define which is output port,power port,ground port,input port.

The syntax is port class and port use.

For example for port Y port class output port use signal.

![WhatsApp Image 2024-04-05 at 7 18 27 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/7f8f7aec-15a3-4be5-a073-187c5114b232)
![WhatsApp Image 2024-04-05 at 7 22 40 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/4b6a5ee7-13d0-46ca-86ee-d75f9d5ed011)

If we dont specify the name the lef file will be created with the cell name only and lef file looks as shown below.

![WhatsApp Image 2024-04-05 at 7 25 53 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f497f0b0-80d6-4f0b-bede-f6384142a162)
![WhatsApp Image 2024-04-05 at 7 26 24 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/a2afa1c1-53c7-4afd-a136-bcd5f4e4f445)
![WhatsApp Image 2024-04-05 at 7 26 52 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/dca2e033-7623-45a1-a631-60952396f39e)

Next step is extracting this LEF file in to our design picorv32a,and copied to our design picorv32a.
![WhatsApp Image 2024-04-05 at 7 04 16 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/6d00340d-9f26-4590-afb6-6dd4fa473f6e)

From the vsdstd celldesign we need to copy the library files in to the design picorv32a.
![WhatsApp Image 2024-04-05 at 7 13 16 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/801cdfec-d338-45a8-a925-e917cfc6b1dd)

Next step is to modify config.tcl file.
![WhatsApp Image 2024-04-05 at 7 25 13 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/89fcba6f-3ae6-40af-bddb-48cc4854deba)

Modified config.tcl file is as shown below.
![WhatsApp Image 2024-04-06 at 5 37 04 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/5c513e12-7812-49f2-8528-dc2ff90a9352)

And now when we do synthesis again,the following results were obtained.
![WhatsApp Image 2024-04-06 at 8 05 12 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/b0318168-347c-4fe0-ac3c-d6637c4dfb46)
![WhatsApp Image 2024-04-06 at 8 06 02 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/cfd24508-3095-47c3-b3cb-82f48bd92c32)

Next comes the concept of CTS(clock tree synthesis).
![WhatsApp Image 2024-04-06 at 8 48 59 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f7eb09b2-766d-4213-9580-44e807f13a7a)
![WhatsApp Image 2024-04-06 at 9 47 09 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/0b67c39d-2414-479c-bbf7-b1ed2a7b8453)

As we saw in the above result of synthesis there is slack violation ,to mitigate this we need to change and set some of the parameters as shown below.
If we want to make any changes we can do it during the flow itself we need not change the config.tcl file and then do it.Synthetic strategy is the one which contains informaion of  delay and the area.
![WhatsApp Image 2024-04-07 at 5 55 36 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f4aa15dd-f50c-4112-afe0-8863da85e3b6)

synth_buffer is very important to be enabled for example if we consider reset it goes through the entire design so we need to reduce the wire delays so we need to add buffers thats why it is very important.
Timing Optimization: One common goal of SYNTH_SIZING is to optimize the timing characteristics of the synthesized circuit. This involves adjusting transistor sizes to meet timing requirements, such as setup and hold times, maximum operating frequency, and signal propagation delays. Sizing optimization can help to minimize critical paths and reduce timing violations.


So we set these variables with the values shown as below to reduce the slack violation.
Before this we need to overwrite the design using the command 
"prep -design picorv32a -tag 07-04_15-26 -overwrite"
Then add the LEF file using the below command.
"set lefs [glob $::env(DESIGN_DIR/src/*.lef]"
"add_lefs -src $lefs"
Then set the environmental parameters as shown.
![WhatsApp Image 2024-04-07 at 6 33 36 AM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/80b9d488-d92d-4394-882c-8ef2a072c3d1)
Then if we run synthesis the tns and wns value is 0.
![WhatsApp Image 2024-04-07 at 10 04 45 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/eaf799f9-bfd8-4d5d-9f4e-d09fdd5fddc0)
Then if we proceed with the further steps that is floorplan we got the error as shown.
![WhatsApp Image 2024-04-07 at 10 10 35 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/812a80ec-b358-4c3e-bf90-7eaf26255cf1)
"init_floorplan"
"place_io"
"tap_decap_or"
Floorplan plan  is successfull.
![WhatsApp Image 2024-04-07 at 10 12 44 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/7d049de3-5bb6-449c-afce-64c0752cba54)

Then run placement and command is "run_placement".
![WhatsApp Image 2024-04-07 at 10 15 24 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/044ccf28-0a1f-48b0-a6d2-e45c06d9bbca)

Lets see the placement layout in magic tool.

![WhatsApp Image 2024-04-07 at 10 34 18 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d00a1387-11a8-4d7d-9892-303f2b63d2a8)
![WhatsApp Image 2024-04-07 at 10 36 55 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/b8d0f8be-0571-4850-9f94-9e9454c3e0cf)

Next comes the setup timing analysis
![WhatsApp Image 2024-04-08 at 7 30 59 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/896fc174-bb40-4085-aafd-576cb0060e84)
where the combinational delay should be less than Clock period.
So here the time S  before time T now combinational process and data that is to be captured by the capture flop ,so thetha is less thanT.Next one introduction of jitter that is temporal variance in the time clock period that is the entire time period of the clock which is 1ns now gets shrinked due to delay produced by clock source.We introduce something called as setup uncertainity to model this jitter,so now setup time equation becomes as
"combinational delay thetha<(T-S-SU)".
The combinational delay is as shown below.
![WhatsApp Image 2024-04-08 at 7 48 15 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/7c22edc6-6360-45a5-b264-a8a942ea81a6)

Next we need to do the timing analysis which has slack violation.
In the openlane we create a file as "pre_sta.conf" as shown below.
![WhatsApp Image 2024-04-08 at 8 52 57 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/e47098e7-5296-453e-a424-d34923c1bfcc)
We need to remember that when we are outside openlane , we cannot use the definitions of environmental variables which were used during synthesis. So, we will create a my_base.sdc file which will contain the definitions of environment variables.
![WhatsApp Image 2024-04-08 at 10 00 27 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/e55356d6-944e-45c4-ad79-022594808363)
![WhatsApp Image 2024-04-10 at 9 47 28 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/4dc15c48-c201-4610-88d7-49b4c135bdce)
![WhatsApp Image 2024-04-10 at 9 47 53 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/afc30966-3a06-4133-ad08-5ccc44b69c71)
![WhatsApp Image 2024-04-10 at 9 48 20 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d4fca477-4434-4593-9273-6886beb34308)
![WhatsApp Image 2024-04-10 at 9 48 36 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/6e85ab04-0945-4e86-8b66-a2cc90110392)


 Now to optimize the set up time we will changethe FANOUT parameter and check.
 ![WhatsApp Image 2024-04-09 at 6 58 01 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/fe6161aa-c740-4979-903e-965231864eaf)
 As we can see slack has slightly got reduced.Now lets check in the sta file whether the changes made in synthesis file are reflecting here or not.
 ![WhatsApp Image 2024-04-09 at 7 01 00 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/7888b9c4-4d0b-45a3-a25a-5a1ef8922e16)
 
 To further reduce the slack violation we can check the drive strength of respective gate and presently how many cells it is handling ,and the Fanout value 
 is right or wrong.
 ![WhatsApp Image 2024-04-09 at 7 12 30 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/858057aa-fbc3-43cf-b0cd-5f98e34b346c)
 So lets check this OR gate.
 we know that OR gate drive strength is 2 but here it is driving 4 loads so we need to work on this as shown below
 ![WhatsApp Image 2024-04-09 at 7 14 53 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d25dc4f7-cbe0-4e4b-8f6b-5cc0d00d41bc)
 Now  we need to replace this or gate of drive strength 2 by 4.
 After this lets generate timing reports.
 ![WhatsApp Image 2024-04-09 at 7 27 44 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/bb7fe4fa-b907-4bbe-a128-8402646ae700)
 slack value got reduced comparitvely.

 let's continue the same process for other OR gates as well.
 ![WhatsApp Image 2024-04-09 at 7 35 26 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f6754646-429f-41d7-937e-f84f57f8a8c2)
 ![WhatsApp Image 2024-04-09 at 7 36 02 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/a174ca76-b9a3-4729-bc7a-f0a325b13a8d)
 ![WhatsApp Image 2024-04-09 at 7 38 23 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/ec128346-da7a-4826-a500-45c26daf855a)
 Slack value got reduce more now.

 Next lets work on the delays to reduce the slack value further.
 
 ![WhatsApp Image 2024-04-09 at 7 42 48 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/990ca547-d572-47df-8007-f68224c81cc6)
 ![WhatsApp Image 2024-04-09 at 7 45 41 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/577cadf9-8e27-4749-9455-206a49b32806)
 ![WhatsApp Image 2024-04-09 at 7 46 14 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f0237d2d-fa06-4ec1-9fa1-0e1f3c75558e)
 As we are replacing the cells like for example drive strength of 2 of OR gate to drive strength of 4.
 Let's check if the cells are getting replaced(start point,end point.through)
 ![WhatsApp Image 2024-04-09 at 7 54 49 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/1e7a822d-7f6d-4c1e-8e2a-c80330ade9e5)
 ![WhatsApp Image 2024-04-09 at 7 56 46 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/275642c7-d08d-4513-aa21-d95233b3fe36)

 so now basically we need to replace our synthesis file with the sta file where it was out of openlane flow all the changes in the slack value were there itself so we need to incorporate it in our synthesis file
 ![WhatsApp Image 2024-04-09 at 8 45 38 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/aa6462c8-4f05-4fcf-b695-a4423dfa72e4)
 ![WhatsApp Image 2024-04-09 at 8 53 10 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/602f05a3-4ce5-42a1-8a8a-60d00952e931)
 We can see that synthesis is overwritten.

 The command used for that is 
 ![WhatsApp Image 2024-04-09 at 8 53 49 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/e72d4a3a-b368-4d50-be9d-b5d82e979ac8)
 ![WhatsApp Image 2024-04-09 at 8 56 59 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/0d2b5379-d39e-48ef-af51-89658ba23a7a)
 Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design we are continuing 
 with the clean design to further stages.
 Then let's run cts 
 command is "run_cts"
 ![WhatsApp Image 2024-04-09 at 9 06 18 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/075701a3-64fe-434c-828f-2a25899fc695)
 ![WhatsApp Image 2024-04-09 at 9 07 22 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/29d298c5-460a-4029-bb26-98e8ac5ccdf2)
 As we can see in the above CTS run is successfull.
 core area increases because we have added buffers.
 CTS file is created in the synthesis as shown below.
 ![WhatsApp Image 2024-04-09 at 9 15 54 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/5b9f8663-cdec-47ee-bc72-d41238af7193)

 let's check the tcl commands for cts ,for this we need to open the "tcl_command".
 ![WhatsApp Image 2024-04-09 at 9 18 50 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d2e54883-df39-4180-b97d-f4cabc127c0b)
 ![WhatsApp Image 2024-04-09 at 9 22 43 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/03f3b61b-e52e-4e01-9902-d25b7587b87e)

 lets check maximum TRANS value it should be 10 percent of clock period value.
 ![WhatsApp Image 2024-04-09 at 9 30 07 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/77cfb32b-8386-4b50-93ad-34208886cb75)



 SETUP TIME ANALYSIS WITH REAL CLOCK THAT IS BUFFERS ARE ADDED.

![WhatsApp Image 2024-04-09 at 11 03 21 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/7b08269c-90ea-4cc5-951a-16d1af638242)
![WhatsApp Image 2024-04-09 at 11 06 51 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/6d32c193-deee-43ee-92c1-debfadb347d0)
so here the hold time is time taken to send data outside the capture flop that is delay of mux2 can be considered as hold time.

![WhatsApp Image 2024-04-09 at 11 48 49 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/4ed1a827-10e9-41c5-9504-a4f996c8088b)
![WhatsApp Image 2024-04-09 at 12 24 12 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/a70d652e-ff95-4a1c-afc6-198532c1f8e5)
openroad has integrated opensta with in itself  openroad is a EDA tool.To do timing analysis we use openroad.Environmental variables can be directly used now as we are in the openlane itself.we need not explicitly declare them as we did for pre_sta where we created my_base.sdc file.
![WhatsApp Image 2024-04-09 at 2 14 21 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/f56517da-6f03-4516-959c-4708db514ea4)
To create the db we need to first read lef and def file as above.
![WhatsApp Image 2024-04-09 at 2 20 30 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/619ac94f-e542-4c58-aeb2-fa4d2f359e01)
As we can see db file is created.
![WhatsApp Image 2024-04-09 at 2 48 34 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/8c10dff3-994d-4cb7-a586-6a3637d8d06c)
![WhatsApp Image 2024-04-09 at 4 09 32 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/fac2c217-5cd2-4d41-88cf-8305ea855655)
set_propgate clock will be used  to calculate the delays of the clock.
It calculates the cell delay in clock path.
Next one is generating the timing report.
![WhatsApp Image 2024-04-09 at 4 19 14 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/6be5b059-d5bb-4897-8ec0-725e21a68c74)

The report looks as shown below.

![WhatsApp Image 2024-04-09 at 4 24 14 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/c0d8d299-06f1-4d9b-9a32-e814437f0b53)
![WhatsApp Image 2024-04-09 at 4 25 19 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/42807ab2-55e8-45f5-95e0-981c59bc3f86)
![WhatsApp Image 2024-04-09 at 4 25 53 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/35ad8230-cca6-4368-beb8-0f76fb524947)


![WhatsApp Image 2024-04-09 at 4 38 10 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/057b2ccd-c20a-41df-8668-35c42acf96f8)
![WhatsApp Image 2024-04-09 at 4 39 35 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/1f826169-698a-4cb1-9bbb-2816ee9763a6)
We are cts.tcl file and checking the buffer list.
we will try removing the buffer 1 from the list using lreplace
![WhatsApp Image 2024-04-09 at 4 48 30 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/7407c5c9-ddcf-4e02-85c8-98bfe1866448)
As we can see lreplace will only modify the output ,to permenantly change it we need to use set command as shown below.

![WhatsApp Image 2024-04-09 at 4 52 13 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/088c0364-4614-448c-a302-c1778180ee5e)
Then checking the current def file.
![WhatsApp Image 2024-04-09 at 5 02 54 PM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/b6667570-327b-470b-9e02-89f4a87ea405)




DAY5vsd workshop

![WhatsApp Image 2024-04-09 at 6 24 31 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/a4824daf-fe28-4375-b815-12104dbdb787)

So the next step here is routing so for that we use maze algorithm as shown above and preferably L shape routing .
DRC is very important during routing.
Techniques used to build wires is photolithography there are some rules when two wires are placed parallely that is minimum distancing and minimum width of the wire.
Uses optical photolithography where  light has got certain specific wavelength which will determine the width of the wire.

![WhatsApp Image 2024-04-09 at 6 51 28 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/4046f8ab-1de6-4e8e-8afd-9e5db172f02b)
Three terms to consider 
1)Wire width.
2)Wire pitch.
3)Wire spacing.
![WhatsApp Image 2024-04-09 at 6 52 01 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/6f934a03-d3f1-42a2-93c6-c7e25f2acdea)
![WhatsApp Image 2024-04-09 at 6 56 41 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/74747fc7-04b7-49c0-8013-ee39dd2b3b69)
To avoid this signal short we use different layers that is metal Mn,Mn+1 layers,and the rest three terms will remain same as mentoined above.
Upper metal layers will be more wider compared to lower ones.
![WhatsApp Image 2024-04-09 at 7 03 19 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/0d923b81-79fe-4f07-8eb2-4a11e562f937)
![WhatsApp Image 2024-04-09 at 7 03 42 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/43cedf05-a7c8-486c-8dc2-c68a6f76f900)
![WhatsApp Image 2024-04-09 at 7 05 20 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/1ce03888-3794-40bd-a58d-cda60750cbb1)

Before generating the routing we need to do power distribution and command for that is "gen_pdn".
![WhatsApp Image 2024-04-09 at 7 13 01 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/04be0ef8-ffba-4f9e-ae0e-cb82ddcfe95b)
![WhatsApp Image 2024-04-09 at 7 13 38 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/d0e194da-6cbf-4d6b-a82b-bcab61b4f81f)
PDN generation is successfull.
![WhatsApp Image 2024-04-09 at 7 14 57 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/9e62205e-8cf9-4e4e-a236-66b62b6194fe)
Standard cells needsto have pitch as above or multiples of it to get proper vdd and gnd rails.
![WhatsApp Image 2024-04-09 at 7 26 21 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/b5a65cfd-c675-409d-a5cb-3e2250853635)


![WhatsApp Image 2024-04-09 at 7 51 29 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/37467618-7530-4d8d-a612-6ee27d73860a)

Routing there are two types as shown.
Command for routing is "run_routing.
![WhatsApp Image 2024-04-09 at 7 57 19 PM (1)](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/2b5072ec-ec28-4f94-a839-3261c29efa86)

![WhatsApp Image 2024-04-09 at 8 07 42 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/956c5533-3dd6-41d3-9d90-7e6288ce9b3d)
Perpendicular are merged.Parallel are bridged.

As we can see below that number of violations are zero 
![WhatsApp Image 2024-04-09 at 8 21 27 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/33378eb0-16c4-4b95-adbe-27170092609e)

To see placement let's open magic tool as shown below.
![WhatsApp Image 2024-04-09 at 8 28 50 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/204586a8-7e2a-4977-9edd-8e7f0debc282)
![WhatsApp Image 2024-04-09 at 8 29 41 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/cf537b4e-cab4-4ea4-92f9-f81f6c3c26d0)
![WhatsApp Image 2024-04-09 at 8 31 11 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/33ee2a81-43d7-442b-a2fb-0a4bb5a22565)

Automatically the layout will be generated as below.
![WhatsApp Image 2024-04-10 at 9 41 23 AM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/b6b17a53-30a4-4421-80e1-d311ec60a1e0)
![WhatsApp Image 2024-04-09 at 8 32 57 PM](https://github.com/HarikaVeluru/VSD-workshop/assets/165346462/2d8ea784-0c2e-4356-a713-1af2672b761b)

 


 




 












































