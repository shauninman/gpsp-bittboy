# gpSP makefile
# Gilead Kutnick - Exophase
# pandora port - notaz
# respberry pi - DPR

# Global definitions

.PHONY: clean
	
CROSS_COMPILE := /opt/trimui/bin/arm-unknown-linux-gnueabi-

CC = $(CROSS_COMPILE)gcc

OBJS      = main.o cpu.o memory.o video.o input.o sound.o gui.o \
            cheats.o zip.o  arm_stub.o  warm.o cpu_threaded.o video_blend.o sha1.o

TARGET    = gpsp

SYSROOT     := $(shell $(CC) --print-sysroot)

# Platform specific definitions 
VPATH      += .. ../arm
INCLUDEDIR = $(SYSROOT)/usr/include
CFLAGS     += -I$(INCLUDEDIR) -DARM_ARCH -DPC_BUILD -Wall -march=armv5te -mtune=arm926ej-s
CFLAGS     += -Ofast -fdata-sections -ffunction-sections -fno-PIC

# expecting to have PATH set up to get correct sdl-config first
LIBS	   += -lSDL
LIBS       += -ldl -lpthread -lz -lgcov -Wl,--as-needed -Wl,--gc-sections -flto -s -lpng

# Compilation:
all: $(TARGET)

%.o: %.S
	$(CC) $(CFLAGS) -c -o $@ $<

cpu.o cpu_threaded.o: CFLAGS += -Wno-unused-variable -Wno-unused-label

$(TARGET): $(OBJS)
	$(CC) $(OBJS) $(LIBS) -o $(TARGET)

clean:
	rm -f *.o $(TARGET)
