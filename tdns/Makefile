CXXFLAGS:=-std=gnu++14 -Wall -O2 -MMD -MP -ggdb -Iext/simplesocket -Iext/simplesocket/ext/fmt-5.2.1/include -pthread
CFLAGS:= -Wall -O2 -MMD -MP -ggdb 

PROGRAMS = tdns tdig tres tdns-c-test

all: $(PROGRAMS)

clean:
	rm -f *~ *.o *.d test $(PROGRAMS)

check: testrunner tdns tdig 
	./testrunner
	cd tests ; ./basic

-include *.d

SIMPLESOCKET = ext/simplesocket/comboaddress.o ext/simplesocket/sclasses.o ext/simplesocket/swrappers.o ext/simplesocket/ext/fmt-5.2.1/src/format.o

tdns: tdns.o record-types.o dns-storage.o dnsmessages.o contents.o tdnssec.o $(SIMPLESOCKET)
	g++ -std=gnu++14 $^ -o $@ -pthread

tdig: tdig.o record-types.o dns-storage.o dnsmessages.o $(SIMPLESOCKET)
	g++ -std=gnu++14 $^ -o $@ -pthread

tres: tres.o record-types.o dns-storage.o dnsmessages.o $(SIMPLESOCKET)
	g++ -std=gnu++14 $^ -o $@ -pthread


tdns-c-test: tdns-c-test.o tdns-c.o record-types.o dns-storage.o dnsmessages.o $(SIMPLESOCKET)
	g++ -std=gnu++14 $^ -o $@ 

testrunner: tests.o record-types.o dns-storage.o dnsmessages.o 
	g++ -std=gnu++14 $^ -o $@ 
