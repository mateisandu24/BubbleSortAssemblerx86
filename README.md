## 📘 `README.md` – **English**

```markdown
# Bubble Sort in Assembly (x86 - MASM)

This repository contains a simple implementation of the **Bubble Sort** algorithm written in **x86 Assembly Language** (MASM/TASM syntax), developed as part of a project for the **Information Technology Basics (BTI)** course, taken in the **1st year, 1st semester** of the **Economic Informatics** specialization, Faculty of Cybernetics, Statistics and Economic Informatics (CSIE).

## 🧠 About the Project

The program allows the user to:
1. Enter the size of a vector (between 3 and 9).
2. Enter each element (only digits 0–9).
3. See the sorted result using the Bubble Sort algorithm.

## 💾 Features

- Prompts user to input vector size and elements.
- Validates all inputs.
- Sorts the vector using the Bubble Sort technique.
- Displays the result using DOS interrupts (`INT 21h`).

## 🛠️ Technologies Used

- Assembly Language (MASM/TASM)
- x86 architecture (real mode DOS)
- Emulator environments like EMU8086 or DOSBox

## 🚀 How to Run

1. Use an x86-compatible emulator (EMU8086, DOSBox).
2. Assemble and link the code using TASM or MASM.

```bash
tasm bubblesort.asm
tlink bubblesort.obj
bubblesort.exe
