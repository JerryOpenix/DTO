CLANG ?= clang-8

EXECABLE = monitor-exec

BPFCODE = bpf_program

KSRC = /usr/src/linux-headers-$(shell uname -r)
BPFTOOLS = $(KSRC)/samples/bpf
BPFLOADER = $(BPFTOOLS)/bpf_load.c
LIBBPF_DEV = /usr/local/bpf

CCINCLUDE += -I$(KSRC)/tools/testing/selftests
CCINCLUDE += -I/usr/include/x86_64-linux-gnu

LOADINCLUDE += -I$(KSRC)/samples/bpf
LOADINCLUDE += -I$(KSRC)/tools/lib
LOADINCLUDE += -I$(KSRC)/tools/perf
LOADINCLUDE += -I$(KSRC)/tools/include

LIBRARY_PATH = -L/usr/local/bpf/lib64
BPFSO = -lbpf

.PHONY: clean $(CLANG) bpfload build

clean:
	rm -f *.o *.so $(EXECABLE)

build: ${BPFCODE.c} ${BPFLOADER}
	$(CLANG) -O2 -target bpf -c $(BPFCODE:=.c) $(CCINCLUDE) -o ${BPFCODE:=.o}

bpfload: build
	$(CLANG) -o $(EXECABLE) -lelf -DHAVE_ATTR_TEST=0 $(LOADINCLUDE) $(CCINCLUDE) $(LIBRARY_PATH) $(BPFSO) $(BPFLOADER) loader.c

$(EXECABLE): bpfload

.DEFAULT_GOAL := $(EXECABLE)
