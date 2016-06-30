#CC=i386-pc-linux-gcc
CC=gcc

UNAME := $(shell uname)

CFLAGS=-O3 -I ../sources -I ../../libhxcfe/sources -I ../../libusbhxcfe/sources

LDFLAGS= -L../../build
LIBS=-lm -ldl -lpthread

LIBHXCFE= ../../build/libhxcfe.a
LIBUSBHXCFE= ../../build/libusbhxcfe.a
LIBHXCADAPTOR= ../../build/libhxcadaptor.a
DEPS= $(LIBUSBHXCFE) $(LIBXHCFE) $(LIBHXCADAPTOR)

# change above to .so if using shared libraries.  This can be done better.

ifeq ($(UNAME), Darwin)
CFLAGS += -arch i386 -mmacosx-version-min=10.5
LDFLAGS += -arch i386 -mmacosx-version-min=10.5
endif

ifeq ($(findstring CYGWIN,$(shell uname)),CYGWIN)
LIBHXCFE= libhxcfe.dll
LIBUSBHXCFE= libusbhxcfe.dll
endif

EXEC=hxcfe

all: $(EXEC)

hxcfe:  hxcfe.o utils.o $(DEPS)
	$(CC) -o $@ hxcfe.o utils.o $(LIBS) -lhxcfe -lusbhxcfe -lhxcadaptor $(LDFLAGS)
	cp $@ ../../build

hxcfe.o: ../sources/hxcfe.c 
	$(CC) -o $@ -c $< $(CFLAGS)

utils.o: ../sources/utils.c
	$(CC) -o $@ -c $< $(CFLAGS)

clean:
	rm -rf *.o *.so *.a

mrproper: clean
	rm -rf $(EXEC)

.PHONY: clean mrproper
