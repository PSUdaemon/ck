.PHONY: check clean distribution

FILES=$(shell find . -name "*.c")
OBJECTS=$(FILES:.c=) $(FILES:.c=_cpp)

all: $(OBJECTS)

%: %.c
	$(CC) $(CFLAGS) $< -o $@ ../../../src/libck.a

%_cpp: %.c
	$(CXX) $(CXXFLAGS) $< -o $@ ../../../src/libck.a

check: all
	for d in $(OBJECTS) ; do        \
		echo $$d;		\
		./$$d || exit 1;     	\
	done;

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM *.exe

include ../../../build/regressions.build
CFLAGS+=-D_GNU_SOURCE
CXXFLAGS+=-D_GNU_SOURCE
