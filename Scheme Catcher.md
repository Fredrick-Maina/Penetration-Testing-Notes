open ports: 22, 80

dir bursting: dev - zip file--> beacon.bin
	server-status
Beacon.bin
	stat, file, xxd, strings

checksec --file=beacon.bin

`$ checksec --file=beacon.bin`
# Get more details

`readelf -h beacon.bin  # ELF header`

i) canary found
ii) no PIE- means it executes in the same memory address
iii) NX enabled- No eXecutable - memory is marked as either for data or code

`objdump -d beacon.bin`

` objdump -t beacon.bin | grep -E "(read_opt|menu|start_socket_server|main|delete_cmd|payload_load)"
	`  THIS ARE THE ADDRESSSES FOR EVERYTHING

# use GDB

gdb beacon.bin # you have to know which functons you are disassebling

`pip3 install lief`

`python3 << 'EOF'`
`import lief`
`import json`

`binary = lief.parse("beacon.bin")`

# `Get all strings`
`print("=== STRINGS ===")`
`for s in binary.strings:`
    `if len(s) > 4:`
        `print(s)`

# `Get imported functions`
`print("\n=== IMPORTS ===")`
`for lib in binary.imports:`
    `print(f"\nLibrary: {lib.name}")`
    `for func in lib.entries:`
        `print(f"  {func.name}")`

# `Get sections`
`print("\n=== SECTIONS ===")`
`for section in binary.sections:`
    `print(f"{section.name}: {section.size} bytes, flags: {section.characteristics}")`
`EOF`

first flag: THM{Welcom3_to_th3_eastmass_pwnland}

# Recon
file beacon.bin
checksec --file=beacon.bin
strings beacon.bin
nm beacon.bin

# Disassembly
objdump -d beacon.bin
objdump -t beacon.bin
readelf -h beacon.bin

# Tracing
ltrace ./beacon.bin
strace ./beacon.bin

# Debugging
gdb ./beacon.bin

# Analysis
xxd beacon.bin | head -50
hexdump -C beacon.bin | head -50

# GDB quick commands
break main
break *0x401234
info functions
disassemble main
run
continue
stepi
nexti
x/10i $rip
x/s $rdi
info registers
print $rax
quit