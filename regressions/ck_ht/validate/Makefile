.PHONY: check clean distribution

OBJECTS=serial serial.delete serial_cpp serial.delete_cpp

all: $(OBJECTS)

serial: serial.c
	$(CC) $(CFLAGS) -o serial serial.c ../../../src/libck.a

serial.delete: serial.c
	$(CC) $(CFLAGS) -DHT_DELETE -o serial.delete serial.c ../../../src/libck.a

serial_cpp: serial.c
	$(CXX) $(CXXFLAGS) -o serial_cpp serial.c ../../../src/libck.a

serial.delete_cpp: serial.c
	$(CXX) $(CXXFLAGS) -DHT_DELETE -o serial.delete_cpp serial.c ../../../src/libck.a

check: all
	./serial || exit 1
	./serial.delete || exit 1
	./serial_cpp || exit 1
	./serial.delete_cpp || exit 1

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM *.exe

include ../../../build/regressions.build
CFLAGS+=-D_GNU_SOURCE
CXXFLAGS+=-D_GNU_SOURCE
