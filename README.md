# 16-Bit NASM Assembly Snake Game

A rigorous, bare-metal implementation of the classic Snake Game written entirely in **x86 Assembly (NASM syntax)**. The engine interfaces directly with PC hardware by writing data directly into video memory, hooking system timer vectors for audio feedback, and executing non-blocking hardware keyboard interrupts.

Developed by **Abdullah Asif**.

---

## 🛠️ Low-Level Technical Highlights

* **Direct Video RAM Mapping:** Bypasses standard operating system layers to write raw characters and text color attributes directly to the text-mode video base address at `0xb800`.
* **Real-time Input Handling:** Leverages BIOS interrupt `int 0x16` to poll keystrokes seamlessly without causing execution freezes.
* **Direct Speaker Manipulation:** Features a dedicated programmable interval timer (PIT) audio subsystem (`beep_play`) that toggles the system speaker via hardware Port `61h` to produce sound effects when eating.
* **Hardware Randomization:** Uses the x86 `rdtsc` instruction (Read Time-Stamp Counter) to obtain precise elapsed clock cycles as a seed for random food positioning.

---

## 🕹️ Controls & Mechanics

Every game session launches with a stylized landing instruction layout. Players must press the **'S'** key to clear configurations and trigger the main execution array.

| Key | Action | Engine Impact |
| :---: | :---: | :--- |
| **S** | Start Game | Fires configuration maps and initial loops |
| **W** | Move Up | Adjusts position metrics by `-160` memory offsets |
| **A** | Move Left | Adjusts position metrics by `-2` memory offsets |
| **S** | Move Down | Adjusts position metrics by `+160` memory offsets |
| **D** | Move Right | Adjusts position metrics by `+2` memory offsets |
| **P** | Pause | Intercepts operations into a holding loop (`pausing`) |
| **E** | Manual Exit | Instantly jumps to the termination sequence |

---

## 💾 Core Subroutine Documentation

  ### 1. Direct Framebuffer Segment Write (`print_snake`)
Tracks snake positional geometry through a structural index array. The body segments are rendered using character literal `*` painted with light green attributes (`0x0A2A`), while the leading head updates via structural identifier `0x0A02`.

```assembly
looping_snake:          ; Traverse index structure arrays
mov di, [bx]        ; Retrieve current coordinate segment offset
mov word[es:di], 0x0A2A   ; Inject raw word (Light Green Color Attribute + '*' Char)
add bx, 2           ; Point index pointer to adjacent word element
loop looping_snake

mov di, [bx]        ; Isolate leading head offset address
mov word[es:di], 0x0A02   ; Update display with dedicated snake head literal
```
## 👨‍💻 THE CREATOR

| ABDULLAH ASIF |
| :---: |
| React / Front-End Developer &bull; AI/ML Engineer |
| [![LinkedIn](https://img.shields.io/badge/LINKEDIN-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/abdullah-asif-bhatti/) [![GitHub](https://img.shields.io/badge/GITHUB-%23100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ABDULLAH-ASIF11) [![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=black)](https://leetcode.com/u/Abdullah-Asif11/) |
