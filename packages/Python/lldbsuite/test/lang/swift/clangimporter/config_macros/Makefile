LEVEL = ../../../../make
SRCDIR := $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))
SWIFT_OBJC_INTEROP := 1

all: a.out

include $(LEVEL)/Makefile.rules

a.out: main.swift libDylib.dylib
	$(SWIFTC) -g -Onone $^ -lDylib -L$(shell pwd) -o $@ $(SWIFTFLAGS) -I. \
	  -Xcc -DDEBUG=1 -Xcc -DSPACE -Xcc -UNDEBUG

libDylib.dylib: dylib.swift
	$(SWIFTC) -g -Onone $^ -emit-library -module-name Dylib -emit-module \
	  -Xlinker -install_name -Xlinker @executable_path/$@ \
	  -Xcc -DDEBUG=1 -Xcc -D -Xcc SPACE -Xcc -U -Xcc NDEBUG

clean::
	rm -rf *.swiftmodule *.swiftdoc *.dSYM *~ lib*.dylib a.out *.o

