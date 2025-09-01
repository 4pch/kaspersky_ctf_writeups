# Writeup 1

Ice Trickster - author writeup

The task is basically a PE inside a PE inside a PE and so on. Each stage is decrypted from the previous one using XOR with the key being MD5(input).

There were 5 stages:

AntiDebug - this stage decrypted the target key and compared against your input. Before this action, there were some functions that won't let you through unless you pass their conditions. They were basically various anti-debug checks and were made to actually require the debugger to be present for the stage to run normally. So intended algorithm here was to pass the checks (via either skipping or just meeting the conditions), retrieve the flag and pass again with the same input;

Equations - this stage was basically a system of equations with the variables being the symbols of the flag. The equations were over a integer ring with the modulo 2 ^ 32 (they were non-linear though) . You can solve this by hand (insane) or using SMT solvers, such as Z3;

HashCrack - this stage calculated a hash of you flag (the hash was MurMur3 (x64 128 bit variation)) and compared against the target value. The hash type can be deduced via constants (findcrypt IDA Pro plugin turns to be quite handy here). After this, you can bruteforce the hash or use rainbow tables. I tested bruteforcing an it took me 7 minutes using 16 threads;

VM - here a virtual machine was implemented. It had 16 opcodes - arithmetical operations, push, pop, mov, lea and jumps. Here you had to reverse the VM implementation, implement a disassembler and reverse the program. The program did various checks over flag symbols. In this stage, the VM could misbehave, but this was intended (we do a little trolling, you know);

Final - just a PE playing GIF. The last flag part is on the GIF.

Combining the parts in their order you result with the flag on you hands

There was an intended shortcut - you can deduce the stage key based from the encrypted PE header - there is a string This program cannot run in DOS mode in PEs - that would be enough to calculate the key. Knowing the key, you can acquire each stage but this will give you only the last part of the flag, you still have to revese engineer 4 previous stages
The challenge can be solved without any debugging - but this is a bit harder and not so interesting as soon as you will not meet the famous Ice Trickster
