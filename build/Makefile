#CC=i386-pc-linux-gcc
CC=gcc

UNAME := $(shell uname)

CFLAGS=-O3 -I ../sources -I ../../libhxcfe/sources -I ../../libusbhxcfe/sources

LDFLAGS=-lc -lm  -ldl  -lpthread -L../../build
LIBHXCFE = libhxcfe.so
LIBUSBHXCFE = libusbhxcfe.so

ifeq ($(UNAME), Darwin)
CFLAGS += -arch i386 -mmacosx-version-min=10.5
LDFLAGS += -arch i386 -mmacosx-version-min=10.5
LIBHXCFE= libhxcfe.a
LIBUSBHXCFE= libusbhxcfe.a
endif

ifeq ($(UNAME), Linux)
LDFLAGS += -Wl,-rpath=.
endif

ifeq ($(findstring CYGWIN,$(shell uname)),CYGWIN)
LIBHXCFE= libhxcfe.dll
LIBUSBHXCFE= libusbhxcfe.dll
endif

EXEC=hxcfe

all: $(EXEC)

hxcfe:  hxcfe.o utils.o ../../build/libhxcadaptor.a $(LIBHXCFE) $(LIBUSBHXCFE)
	$(CC) -o $@ hxcfe.o utils.o -lhxcadaptor -lhxcfe -lusbhxcfe $(LDFLAGS)
	cp $@ ../../build

$(LIBHXCFE): ../../build/$(LIBHXCFE)
	ln ../../build/$(LIBHXCFE)  $(LIBHXCFE)

$(LIBUSBHXCFE): ../../build/$(LIBUSBHXCFE)
	ln ../../build/$(LIBUSBHXCFE)  $(LIBUSBHXCFE)

hxcfe.o: ../sources/hxcfe.c 
	$(CC) -o $@ -c $< $(CFLAGS)

utils.o: ../sources/utils.c
	$(CC) -o $@ -c $< $(CFLAGS)

clean:
	rm -rf *.o
	rm -rf *.so

mrproper: clean
	rm -rf $(EXEC)

.PHONY: clean mrproper
