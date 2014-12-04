.PHONY: check clean distribution

FILES=$(shell find . -name "*.c")
OBJECTS=$(FILES:.c=) $(FILES:.c=_cpp)
HALF=`expr $(CORES) / 2`

all: $(OBJECTS)

check: all
	./ck_stack $(CORES) 1
	./ck_epoch_synchronize $(HALF) $(HALF) 1
	./ck_epoch_poll $(CORES) 1 1
	./ck_epoch_call
	./ck_stack_cpp $(CORES) 1
	./ck_epoch_synchronize_cpp $(HALF) $(HALF) 1
	./ck_epoch_poll_cpp $(CORES) 1 1
	./ck_epoch_call_cpp

%: %.c
	$(CC) $(CFLAGS) $< -o $@ ../../../src/libck.a

%_cpp: %.c
	$(CXX) $(CXXFLAGS) $< -o $@ ../../../src/libck.a

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM *.exe

include ../../../build/regressions.build
CFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
CXXFLAGS+=$(PTHREAD_CXXFLAGS) -D_GNU_SOURCE
