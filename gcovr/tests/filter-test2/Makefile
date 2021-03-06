CFLAGS= -fprofile-arcs -ftest-coverage -fPIC

BASE_OS:=$(shell uname | cut -d'-' -f1)
ifeq ($(BASE_OS),MINGW32_NT)
  BASE_OS:=MSYS_NT
endif
ifeq ($(BASE_OS),MSYS_NT)
  # Absolute filters are known to not work on Windows right now.
  # Use relative path instead
  # GCOVR_TEST_OPTIONS := -f $(shell cygpath -w "$$PWD")\main.cpp
  GCOVR_TEST_OPTIONS := -f main.cpp
else
  GCOVR_TEST_OPTIONS := -f $(shell pwd)/main.cpp
endif

all:
	$(CXX) $(CFLAGS) -c file1.cpp -o file1.o
	$(CXX) $(CFLAGS) -c main.cpp -o main.o
	$(CXX) $(CFLAGS) main.o file1.o -o testcase

run: txt xml html

txt:
	./testcase
	echo "$(GCOVR_TEST_OPTIONS)"
	$(GCOVR) $(GCOVR_TEST_OPTIONS) -d -o coverage.txt

xml:
	./testcase
	$(GCOVR) $(GCOVR_TEST_OPTIONS) -d -x -o coverage.xml

html:
	./testcase
	$(GCOVR) $(GCOVR_TEST_OPTIONS) -d --html-details -o coverage.html

clean:
	rm -f testcase
	rm -f *.gc* *.o
	rm -f coverage.txt coverage.xml coverage*.html
