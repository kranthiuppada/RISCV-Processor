# 🚀 RISC-V Processor (Verilog Implementation)  

This project implements a **32-bit RISC-V Processor** in Verilog. The design has been simulated using **Vivado** , with testbenches verifying instruction execution, register updates, and program counter (PC) flow.  

---

## 📌 Project Overview  

- **Architecture:** Single-cycle RISC-V processor  
- **ISA Supported:** RV32I (Basic arithmetic, logical, branch, and memory instructions)  
- **Language:** Verilog HDL  
- **Simulation Tools:** Vivado 
- **Verification:** Testbench with waveform analysis  

---

## ⚙️ Features  

- ✅ Program Counter (PC) increment and jump handling  
- ✅ Instruction fetch & decode logic  
- ✅ ALU operations (`ADD`, `SUB`, `AND`, `OR`, etc.)  
- ✅ Register file read/write  
- ✅ Load/Store support  
- ✅ Branch instruction execution (`BEQ`, `BNE`, etc.)  
- ✅ Waveform verification using GTKWave  

---

## 📊 Waveform Explanation  

The waveform confirms correct processor execution:  

- **PC Behavior:**  
  PC starts from reset and increments by 4 every cycle. For branch/jump instructions, PC updates to the target address.  

- **Instruction Decode:**  
  The fetched instruction is decoded into opcode, source registers, destination register, and immediate values.  

- **ALU Operations:**  
  Example:

   add x5, x1, x2 → x5 gets (x1 + x2)
  
   sub x6, x5, x3 → x6 gets (x5 - x3)

  The waveform shows correct ALU outputs being stored in the register file.  

- **Registers:**  
Values are written back into the correct registers during WB stage.  

- **Branches:**  
On `BEQ`/`BNE`, waveform shows the PC updating to the branch target when the condition is satisfied.  

✅ These results verify that the processor executes instructions correctly.  

---

## 🧪 Testbench  

The `RISCV_TB.v` testbench includes:  
- Clock generation (`always #50 clk = ~clk`)  
- Reset sequence  
- Simulation runtime (`#5200; $finish;`)  
- VCD dump for GTKWave visualization  

---

## 📷 Simulation Output  

**Waveform (GTKWave):**  
*![Image](https://github.com/user-attachments/assets/5f98194e-39f7-4b2f-a612-0b7168e4251a)*


**✅ Waveform Verification**

To ensure the RISC-V processor is working correctly, I verified the execution of instructions step by step from the simulation waveform.

Example 1: PC = 0x18

Instruction: 0x00519233 → Decodes to ADD x4, x3, x10

Inputs from waveform:

x3 = 0x28 (40)

x10 = 0x41 (65)

Expected ALU result: 40 + 65 = 105 (0x69)

Waveform result:

WB_data = 0x69

RegWrite = 1

✅ Correct execution (x4 updated to 0x69).

Example 2: PC = 0x1C

Instruction: 0x019806B3 → Decodes to ADD x13, x0, x25

Inputs from waveform:

x0 = 0x0

x25 = 0xFFFFFFF6 (-10)

Expected ALU result: 0 + (-10) = -10 (0xFFFFFFF6)

Waveform result:

WB_data = 0xFFFFFFF6

RegWrite = 1

✅ Correct execution (x13 updated to -10).
 

---  

## 📜 Conclusion

The simulation results and waveform verification confirm that the RISC-V processor is functioning correctly, executing instructions as expected with proper register and memory updates.
