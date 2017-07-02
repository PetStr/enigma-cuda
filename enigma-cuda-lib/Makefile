# GNU Make version
#
# Copyright (C) 2002-2017 Petter Strandh

CPP = g++
NVCC = /usr/local/cuda-8.0/bin/nvcc

src = $(wildcard *.cpp)
obj = $(src:.c=.o)
dep = $(obj:.o=.d)  # one dependency file for each source
# -Wall -pedantic
LDFLAGS =  -std=c++11 -L/usr/lib64  -L/usr/local/cuda-8.0/targets/x86_64-linux/lib/ -lcuda  -lcudart 

enigma-cuda: $(obj) cuda_code.o
	$(CPP) -o $@ $^ $(LDFLAGS) #-include $(dep)   # include all dep files in the makefile

cuda_code.o: cuda_code.cu
	$(NVCC) -o $@ $^ -c -std=c++11 -arch sm_50

# rule to generate a dep file by using the C preprocessor
# (see man cpp for details on the -MM and -MT options)
%.d: %.c
	@$(CPP) $(CFLAGS) $< -MM -MT $(@:.d=.o) >$@

.PHONY: clean
clean:
	rm -f $(obj) enigma-cuda

.PHONY: cleandep
cleandep:
	rm -f $(dep)

