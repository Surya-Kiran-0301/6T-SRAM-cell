# 6T-SRAM-cell

An SRAM (Static Random Access Memory) cell is a bistable memory element used to store one bit 
of data. A conventional SRAM cell consists of six MOS transistors (6T): two cross-coupled CMOS 
inverters that form a latch for data storage, and two access transistors that connect the cell to the bit 
lines during read and write operations. Unlike DRAM, SRAM does not require periodic refreshing as 
long as power is supplied, making it faster and more reliable for high-speed applications such as 
processor caches and embedded memories. 

# Working

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







