.PHONY: check clean distribution

SERIAL_OBJECTS=serial

CONCURRENT_OBJECTS=mpnc_push mpmc_push upmc_push spinlock_push spinlock_eb_push 	\
		mpmc_pop upmc_pop spinlock_pop spinlock_eb_pop				\
		upmc_trypop mpmc_trypop mpmc_trypair					\
		mpmc_pair spinlock_pair spinlock_eb_pair pthreads_pair			\
		mpmc_trypush upmc_trypush						\

OBJECTS=$(SERIAL_OBJECTS) $(CONCURRENT_OBJECTS) $(SERIAL_OBJECTS:=_cpp) $(CONCURRENT_OBJECTS:=_cpp)

all: $(OBJECTS)

check: all
	for d in $(SERIAL_OBJECTS) ; do  \
		echo $$d;                \
		./$$d || exit 1;         \
	done;
	for d in $(CONCURRENT_OBJECTS) ; do   \
		echo $$d;                     \
		./$$d $(CORES) 1 0 || exit 1; \
	done;
	for d in $(SERIAL_OBJECTS:=_cpp) ; do  \
		echo $$d;                      \
		./$$d || exit 1;               \
	done;
	for d in $(CONCURRENT_OBJECTS:=_cpp) ; do   \
		echo $$d;                           \
		./$$d $(CORES) 1 0 || exit 1;       \
	done;

%: %.c
	$(CC) $(CFLAGS) $< -o $@

spinlock_%: %.c
	$(CC) $(CFLAGS) -DSPINLOCK $< -o $@

spinlock_eb_%: %.c
	$(CC) $(CFLAGS) -DSPINLOCK -DEB $< -o $@

mpmc_try%: %.c
	$(CC) $(CFLAGS) -DTRYMPMC $< -o $@

upmc_try%: %.c
	$(CC) $(CFLAGS) -DTRYUPMC $< -o $@

mpnc_%: %.c
	$(CC) $(CFLAGS) -DMPNC $< -o $@

mpmc_%: %.c
	$(CC) $(CFLAGS) -DMPMC $< -o $@

upmc_%: %.c
	$(CC) $(CFLAGS) -DUPMC $< -o $@

pthreads_%: %.c
	$(CC) $(CFLAGS) -DPTHREADS $< -o $@

%_cpp: %.c
	$(CXX) $(CXXFLAGS) $< -o $@

spinlock_%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DSPINLOCK $< -o $@

spinlock_eb_%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DSPINLOCK -DEB $< -o $@

mpmc_try%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DTRYMPMC $< -o $@

upmc_try%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DTRYUPMC $< -o $@

mpnc_%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DMPNC $< -o $@

mpmc_%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DMPMC $< -o $@

upmc_%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DUPMC $< -o $@

pthreads_%_cpp: %.c
	$(CXX) $(CXXFLAGS) -DPTHREADS $< -o $@

clean:
	rm -rf *~ *.o *.dSYM *.exe $(OBJECTS)

include ../../../build/regressions.build
CFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
CXXFLAGS+=$(PTHREAD_CXXFLAGS) -D_GNU_SOURCE
