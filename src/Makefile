AS = riscv64-linux-gnu-as --march=rv32i
LD = riscv64-linux-gnu-ld -b elf32-littleriscv
OBJCOPY = riscv64-linux-gnu-objcopy
OBJDUMP = riscv64-linux-gnu-objdump
SRC = test

%.o: %.s
	$(AS) $< -o $@

%.elf: %.o
	$(LD) -T link.ld $< -o $@

%.bin: %.elf
	$(OBJDUMP) -D -M numeric,no-aliases -t $<
	$(OBJCOPY) -O binary --reverse-bytes=4 $< $@ 

%.hex: %.bin 
	$(OBJCOPY) -O verilog -I binary $< $@

default: $(SRC).hex

clean: 
	rm -f *.hex *.elf *.bin *.o
