# 6T-SRAM-cell

An SRAM (Static Random Access Memory) cell is a bistable memory element used to store one bit 
of data. A conventional SRAM cell consists of six MOS transistors (6T): two cross-coupled CMOS 
inverters that form a latch for data storage, and two access transistors that connect the cell to the bit 
lines during read and write operations. Unlike DRAM, SRAM does not require periodic refreshing as 
long as power is supplied, making it faster and more reliable for high-speed applications such as 
processor caches and embedded memories. 

# Working

1. SRAM cell

   A six-transistor memory cell is formed by two access transistors controlled by the word-line (WL) connecting bit lines BL and BLC with the internal nodes out1 and out2, and two back-to-back connected inverters forming a latch (Fig 3).

When the word line (WL) is asserted high, both access transistors turn on, connecting the storage nodes of the cross-coupled inverters to the bit lines, BL and BLC. During a write operation, BL carries the data while BLC carries its complement (datac). For the first inverter, BLC acts as the input (In1), and its output (Out1) is connected to the input of the second inverter as well as to BL through the access transistor. Similarly, for the second inverter, BL acts as the input (In2), and itsoutput (Out2) is connected to the input of the first inverter and to BLC. This cross-coupled feedback configuration forms a bistable latch capable of storing one bit of data. Once the word line is deasserted, the access transistors turn off, isolating the cell from the bit lines. The stored data is retained indefinitely as long as the supply voltage is maintained, without requiring periodic refresh. This ability to statically preserve data gives the memory its name, Static Random Access Memory 

2. Write Driver

   
The write operation is performed when the control signals are set as WL = 1, WE = 1, and RE = 0. During this operation, the write enable signal (WE) is complemented to generate WEC, and both signals are used to control the transmission gates of the write driver(Fig 4).

When WE = 1 and WEC = 0, both the NMOS and PMOS transistors of the transmission gates are turned ON, providing a low-resistance conduction path between the data inputs and the bit lines. As 
a result, the input data (Data) is transferred to the bit line (BL), while its complement (Datac) is simultaneously transferred to the complementary bit line (BLC) through the second 
transmission gate.
Conversely, when WE = 0 and WEC = 1, both transmission gates are turned OFF, presenting a high-impedance path between the data inputs and the bit lines. This isolates BL and BLC from the write driver, preventing any unintended modification of the stored data.
By driving BL and BLC with complementary logic levels during the write operation, the write driver forces the SRAM cell to store the desired logic value when the word line is asserted.


