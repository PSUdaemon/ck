.PHONY: check clean distribution

FILES=$(shell find . -name "*.c")
OBJECTS=$(FILES:.c=) $(FILES:.c=_cpp)

all: $(OBJECTS)

%: %.c
	$(CC) $(CFLAGS) $< -o $@ ../../../src/libck.a

%_cpp: %.c
	$(CXX) $(CXXFLAGS) $< -o $@ ../../../src/libck.a

check: all
	for d in $(OBJECTS) ; do				\
		echo $$d `expr $(CORES) / 2` 2 1;		\
		./$$d `expr $(CORES) / 2` 2 1 || exit 1;	\
	done;

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM *.exe

include ../../../build/regressions.build
CFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
CXXFLAGS+=$(PTHREAD_CXXFLAGS) -D_GNU_SOURCE
