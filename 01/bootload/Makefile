PREFIX	= /usr/local/h8-elf
ARCH	= h8300-elf
BINDIR	= $(PREFIX)/bin
ADDNAME	= $(ARCH)-

AR		= $(BINDIR)/$(ADDNAME)ar
AS		= $(BINDIR)/$(ADDNAME)as
CC		= $(BINDIR)/$(ADDNAME)gcc
LD		= $(BINDIR)/$(ADDNAME)ld
NM		= $(BINDIR)/$(ADDNAME)nm
OBJCOPY	= $(BINDIR)/$(ADDNAME)objcopy
OBJDUMP	= $(BINDIR)/$(ADDNAME)objdump
RANLIB	= $(BINDIR)/$(ADDNAME)ranlib
STRIP	= $(BINDIR)/$(ADDNAME)strip

H8WRITE	= ../../tools/h8write/h8write

H8WRITE_SERDEV = /dev/cu.usbserial-FTRVI7J0

OBJS  = vector.o startup.o intr.o main.o interrupt.o
OBJS += lib.o serial.o xmodem.o elf.o

TARGET = kzload

CFRAGS = -Wall -mh -nostdinc -nostdlib -fno-builtin
CFRAGS += -I.
CFRAGS += -Os
CFRAGS += -DKZLOAD

LFRAGS = -static -T ld.scr -L.

.SUFFIXES: .c .o
.SUFFIXES: .s .o
.SUFFIXES: .S .o

all :	$(TARGET)

$(TARGET) :	$(OBJS)
	$(CC) $(OBJS) -o $(TARGET) $(CFRAGS) $(LFRAGS)
	cp $(TARGET) $(TARGET).elf
	$(STRIP) $(TARGET)

.c.o : $<
	$(CC) -c $(CFRAGS) $<

.s.o : $<
	$(CC) -c $(CFRAGS) $<

.S.o : $<
	$(CC) -c $(CFRAGS) $<

$(TARGET).mot : $(TARGET)
	$(OBJCOPY) -O srec $(TARGET) $(TARGET).mot

image :	$(TARGET).mot

write :	$(TARGET).mot
	$(H8WRITE) -3069 -f20 $(TARGET).mot $(H8WRITE_SERDEV)

clean : 
	rm -f $(OBJS) $(TARGET) $(TARGET).elf $(TARGET).mot