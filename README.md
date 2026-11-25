# 6T-SRAM-cell

An SRAM (Static Random Access Memory) cell is a bistable memory element used to store one bit 
of data. A conventional SRAM cell consists of six MOS transistors (6T): two cross-coupled CMOS 
inverters that form a latch for data storage, and two access transistors that connect the cell to the bit 
lines during read and write operations. Unlike DRAM, SRAM does not require periodic refreshing as 
long as power is supplied, making it faster and more reliable for high-speed applications such as 
processor caches and embedded memories. 

To understand how each peripheral circuit is connected together and what are the values of the input pulse voltages given open this [schematic](sram_65nm_fullCKT.asc)

# Working

1. [SRAM cell](6tsram_65nm.asc)<br>

   A six-transistor memory cell is formed by two access transistors controlled by the word-line (WL) 
connecting bit lines BL and BLC with the internal nodes out1 and out2, and two back-to-back 
connected inverters forming a latch.
When the word line (WL) is asserted high, both access transistors turn on, connecting the storage 
nodes of the cross-coupled inverters to the bit lines, BL and BLC. During a write operation, BL 
carries the data while BLC carries its complement (datac). For the first inverter, BLC acts as the 
input (In1), and its output (Out1) is connected to the input of the second inverter as well as to BL 
through the access transistor. Similarly, for the second inverter, BL acts as the input (In2), and 
itsoutput (Out2) is connected to the input of the first inverter and to BLC. This cross-coupled 
feedback configuration forms a bistable latch capable of storing one bit of data. Once the word line is 
deasserted, the access transistors turn off, isolating the cell from the bit lines. The stored data is 
retained indefinitely as long as the supply voltage is maintained, without requiring periodic refresh. 
This ability to statically preserve data gives the memory its name, Static Random Access Memory

2. [Write Driver](write_65nm.asc)

   The write operation is performed when the control signals are set as WL = 1, WE = 1, and RE = 0. 
During this operation, the write enable signal (WE) is complemented to generate WEC, and both 
signals are used to control the transmission gates of the write driver. 
When WE = 1 and WEC = 0, both the NMOS and PMOS transistors of the transmission gates are 
turned ON, providing a low-resistance conduction path between the data inputs and the bit lines. As  a result, the input data (Data) is transferred to the bit line (BL), while its complement (Datac) is simultaneously transferred to the complementary bit line (BLC) through the second transmission gate. 
Conversely, when WE = 0 and WEC = 1, both transmission gates are turned OFF, presenting a high
impedance path between the data inputs and the bit lines. This isolates BL and BLC from the write 
driver, preventing any unintended modification of the stored data. 
By driving BL and BLC with complementary logic levels during the write operation, the write driver 
forces the SRAM cell to store the desired logic value when the word line is asserted.

3. [Precharge Driver](Precharge_driver_65nm.asc)
   
   When the precharge enable (RE) signal is enabled, the precharge circuit is activated, turning 
on the PMOS transistors connected to the bit lines. As a result, both the bit line (BL) and the 
complementary bit line (BLC) are charged to the supply voltage (VDD). In addition, an equalization 
PMOS transistor connects BL and BLC, ensuring that both bit lines are maintained at the same 
voltage level before the start of a read operation. Precharging and equalizing the bit lines minimizes 
the initial voltage difference, thereby improving the speed and reliability of the read operation.

4. [Sense Amplifier](sense_amplifier_sram.asc)

   The sense amplifier operates during the read operation, when the control signals are WL = 1, 
WE = 0, and RE = 0. Initially, both bit lines (BL and BLC) are precharged to VDD by the 
precharge circuit. During this period, the Sense Amplifier Enable (SAE) signal remains low, 
keeping the sense amplifier disabled. 
When the word line (WL) is asserted, the SRAM cell is connected to the bit lines through the access 
transistors. Depending on the data stored in the cell, either BL or BLC experiences a slight voltage 
drop, while the other bit line remains close to VDD. This small differential voltage carries the stored 
information but is insufficient to be directly interpreted as a logic level. 
As the differential voltage develops, the SAE signal is asserted high, enabling the sense amplifier. 
The tail NMOS transistor turns on, allowing current to flow through the cross-coupled latch. Due to 
the positive feedback provided by the cross-coupled inverters, the node connected to the lower
voltage bit line is rapidly pulled toward ground, while the opposite node is driven toward VDD. This 
regenerative action amplifies the small voltage difference between BL and BLC into a full-swing 
digital output. 
Finally, the outputs of the sense amplifier are connected to buffers, which isolate the latch from the 
external load and prevent any degradation of the amplified signal. The buffered outputs provide 
stable logic levels corresponding to the data stored in the SRAM cell.


# Observations

Case 1: Storing bit 1 in SRAM cell <br>

<img width="1619" height="465" alt="image" src="https://github.com/user-attachments/assets/8d83abf4-8b7b-43d8-a9aa-17f7eb94d341" /><br>

<img width="661" height="314" alt="image" src="https://github.com/user-attachments/assets/aaf839b1-60f4-456c-a32f-3b68a0df6b6a" /><br>
Waveforms of WL, WE, RE, Data

<img width="661" height="314" alt="image" src="https://github.com/user-attachments/assets/499cded3-24b6-4f34-9d0e-d2e7342bffbd" /><br>
Waveforms of BL, out1, BLC, out2

<img width="661" height="313" alt="image" src="https://github.com/user-attachments/assets/19364b37-cf71-4c9b-915c-3404434be036" /><br>
Waveforms of EN, SAE, Vout


Case 2: Storing bit 0 in SRAM cell <br>

<img width="1199" height="267" alt="image" src="https://github.com/user-attachments/assets/d4e5ca50-8702-4a53-80ac-81b7dd52fde5" /><br>

<img width="673" height="320" alt="image" src="https://github.com/user-attachments/assets/a909d7c5-593f-48ca-b6a0-8eb73daa98f3" /><br>
Waveforms of WL, WE, RE, Data

<img width="673" height="319" alt="image" src="https://github.com/user-attachments/assets/4cfe639e-2997-4001-a581-8d5fefa67f48" /><br>
Waveforms of BL, out1, BLC, out2

<img width="673" height="319" alt="image" src="https://github.com/user-attachments/assets/ba390854-c03c-4e92-8d8b-9f3cb781d506" /><br>
Waveforms of  EN, SAE, Vout

# Characteristics

The performance of the designed 6T SRAM cell was evaluated through transient and DC 
simulations. The key characteristics analyzed include power consumption, delay, static noise margin, 
write margin, and access time. These parameters provide an indication of the speed, stability, and 
power efficiency of the memory cell. 

<img width="626" height="569" alt="image" src="https://github.com/user-attachments/assets/eb484f71-1f88-48d4-a30f-cc753841b7e5" />






