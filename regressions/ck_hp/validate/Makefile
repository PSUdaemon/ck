.PHONY: check clean distribution

FILES=$(shell find . -name "*.c")
OBJECTS=$(FILES:.c=) $(FILES:.c=_cpp)

all: $(OBJECTS)

check: all
	./serial
	./ck_hp_stack $(CORES) 100 1
	./ck_hp_fifo $(CORES) 1 16384 100
	./nbds_haz_test $(CORES) 15 1
	./ck_hp_fifo_donner $(CORES) 16384
	./serial_cpp
	./ck_hp_stack_cpp $(CORES) 100 1
	./ck_hp_fifo_cpp $(CORES) 1 16384 100
	./nbds_haz_test_cpp $(CORES) 15 1
	./ck_hp_fifo_donner_cpp $(CORES) 16384

%: %.c
	$(CC) $(CFLAGS) $< -o $@ ../../../src/libck.a

%_cpp: %.c
	$(CXX) $(CXXFLAGS) $< -o $@ ../../../src/libck.a

clean:
	rm -rf *~ *.o *.dSYM *.exe $(OBJECTS)

include ../../../build/regressions.build
CFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
CXXFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
