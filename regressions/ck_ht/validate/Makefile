.PHONY: check clean distribution

OBJECTS=serial serial.delete serial_cpp serial.delete_cpp

all: $(OBJECTS)

check: all
	for d in $(OBJECTS) ; do        \
		echo $$d;		\
		./$$d || exit 1;     	\
	done;

serial: serial.c
	$(CC) $(CFLAGS) -o serial serial.c ../../../src/libck.a

serial.delete: serial.c
	$(CC) $(CFLAGS) -DHT_DELETE -o serial.delete serial.c ../../../src/libck.a

serial_cpp: serial.c
	$(CXX) $(CXXFLAGS) -o serial_cpp serial.c ../../../src/libck.a

serial.delete_cpp: serial.c
	$(CXX) $(CXXFLAGS) -DHT_DELETE -o serial.delete_cpp serial.c ../../../src/libck.a

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM *.exe

include ../../../build/regressions.build
CFLAGS+=-D_GNU_SOURCE
CXXFLAGS+=-D_GNU_SOURCE
