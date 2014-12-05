.PHONY: check clean distribution

FILES=$(shell find . -name "*.c")
OBJECTS=$(FILES:.c=) $(FILES:.c=_cpp)

all: $(OBJECTS)

%: %.c
	$(CC) $(CFLAGS) $< -o $@ ../../../src/libck.a

%_cpp: %.c
	$(CXX) $(CXXFLAGS) $< -o $@ ../../../src/libck.a

check: all
	./ck_fifo_spsc $(CORES) 1 64000
	./ck_fifo_mpmc $(CORES) 1 16000
	./ck_fifo_spsc_iterator
	./ck_fifo_mpmc_iterator
	./ck_fifo_spsc_cpp $(CORES) 1 64000
	./ck_fifo_mpmc_cpp $(CORES) 1 16000
	./ck_fifo_spsc_iterator_cpp
	./ck_fifo_mpmc_iterator_cpp

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM *.exe

include ../../../build/regressions.build
CFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
CXXFLAGS+=$(PTHREAD_CXXFLAGS) -D_GNU_SOURCE
