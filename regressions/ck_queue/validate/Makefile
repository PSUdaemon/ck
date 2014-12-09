.PHONY: check clean distribution

FILES=$(shell find . -name "*.c")
OBJECTS=$(FILES:.c=) $(FILES:.c=_cpp)

all: $(OBJECTS)

%: %.c
	$(CC) $(CFLAGS) $< -o $@ ../../../src/libck.a

%_cpp: %.c
	$(CXX) $(CXXFLAGS) $< -o $@ ../../../src/libck.a

check: all
	./ck_list $(CORES) 5
	./ck_slist $(CORES) 5
	./ck_stailq $(CORES) 1000000
	./ck_list_cpp $(CORES) 5
	./ck_slist_cpp $(CORES) 5
	./ck_stailq_cpp $(CORES) 1000000

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM *.exe

include ../../../build/regressions.build
CFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
CXXFLAGS+=$(PTHREAD_CXXFLAGS) -D_GNU_SOURCE
