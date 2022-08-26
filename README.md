# Step-7-projects-in-Awl-and-Fbd
Plc programs developed in Siemens Step 7 and WinCC Flexible in Awl (Instruction list) and Fbd(Function block diagram).
## Sorting by Height Advanced process with Shift instruction.
This project consist of **sorting boxes by their height** in order to send them to a specific location of the process/plant. This control is made by a **sensor** located between the main conveyor belts (**feeder** and **entry**).
Once the sensor detects a large box, a bit from a memory word varible (MW) is set on a negative edge detection. At the same time, the sensor that detectes if a box is passing by or not, is in charge to 
**shift** the activated bit, in order to "**follow the large box**" previously detected. 

When any box arrives at the **turn table station**, in that moment, the **shifted bit** is consulted to decide where to send that box to. If the box is a large box, it will be sent to the left conveyor. Otherwise, it will go through the oppsites conveyor.


![](SortingByHeight/img/sortingPlant.png)
## Project execution and main considerations

<img src="SortingByHeight/img/ProgramExample.png" width="600" align="right">

In this project, I have followed the modular programming approach in order to tidy up the logic, be more comprehensive and more readable to those who could come after me.

I have also used the FSM (Finite State Machine) approach to develop two parts of the logic. The part which controls the feeder and entry conveyor and the one that governs the box path selection or turn table. 

*You could see both implementations inside each correspondig [Pdf](SortingByHeight/processPDFs/)*.

While I was implementing the FSM that controls the feeder and entry conveyors, I ran into a problem while using a timer and a counter within the different states. *I used a "SPL" loop in AWL, which is similar to the "Case Statement" in any other high level lenguage*.

The problem was, that the timer and the counter will work only the first time and got frozen for the consecutives cycles. My problem was that I overlooked how other functions work inside loops. I soon realized what the problem was and put the timer and the counter in a separated FC to be called permanently and be activated only with the right conditions.

Once that was implemented, the State machine worked smoothly like it should. Another implementation that I have used during this program, is the use of pointers to read and write the process variables into the data bases variables, as you can see in the picture above.

I will keep refactoring the code and implement and Hmi in the near future.


