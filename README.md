# Buffer Overflow Attack
This repo contains a C code to demonstrate exploitation of buffer overflow during unsafe copy operation.

OS Used:
- SEEDLAB, Ubuntu 16.04 32-bit (Should work on any 32-bit or i386 architecture)

Demonstration:
- Login as normal user(i.e. not as `root`)
- First disable virtual address randomization 
```bash
sudo sysctl -w kernel.randomize_va_space=0
```
- Now debug `demo.c` with gdb to know the return address to exploit and its offset from buffer to exploit
```bash
debug.sh demo.c
```
- You should be in gdb console now. Finding address and offset from gdb using following commands
```gdb
b foo
run
p $ebp
p &buffer
p/d $1-$2
q
```
   Note address of ebp from `p $ebp` and offset from buffer from `p/d $1-$2`

- After quitting from gdb console modify ebp address, and offset updating following lines in `exploit.py` 
```python
ebp_offset = <offset_obtained_from_gdb>
addr_ebp = <address_of_ebp_obtained_from_gdb>
```
- Finally run the attack using `run.sh`
```bash
run.sh
```
- If everything is okay, a bash would be opened as root. Check using
```bash
whoami
```  
  
Resources used:
- shellcode and `demo.c` from SEEDLAB