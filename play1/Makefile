################################
#
#	created by qiaoyc
#
################################
CXX=g++
#CXX=/home/qiao/user/bin/g++

EIGEN_LOCATION=../
#GPERF_LIB_LOCATION=/home/korchagin/user/lib
GPERF_LIB_LOCATION=/home/qiao/user/lib
BUILD_DIR=objs

TARGETS=
TARGETS+=mainTest

CXXFLAGS=
CXXFLAGS+= -O3
CXXFLAGS+= -std=c++0x
CXXFLAGS+= -funroll-loops
CXXFLAGS+= -march=native
CXXFLAGS+= -m64
CXXFLAGS+= -DEIGEN_DONT_PARALLELIZE
CXXFLAGS+= -DEIGEN_NO_DEBUG
CXXFLAGS+= -DEIGEN_NO_STATIC_ASSERT
CXXFLAGS+= -I $(EIGEN_LOCATION)
CXXFLAGS+= -fopenmp
CXXFLAGS+= -g

LDFLAGS= 
LDFLAGS+= -lm

TC_LDFLAGS=
TC_LDFLAGS+= -ltcmalloc -L $(GPERF_LIB_LOCATION) -Wl,-R$(GPERF_LIB_LOCATION)

SRCS=$(shell ls *.cpp)
OBJS=$(SRCS:.cpp=.o)

all: $(TARGETS)

mainTest: $(BUILD_DIR) $(patsubst %, $(BUILD_DIR)/%, mainTest)

$(BUILD_DIR)/tc_%.o : %.cpp
	$(CXX) -o $@ -c $< $(CXXFLAGS) $(LDFLAGS) $(TC_LDFLAGS)

$(BUILD_DIR)/mainTest : $(patsubst %, $(BUILD_DIR)/tc_%, $(OBJS))
	$(CXX) -o $@ $^ $(CXXFLAGS) $(LDFLAGS) $(TC_LDFLAGS)
	$(CXX) -S -o Func.S Func.cpp $(CXXFLAGS) $(LDFLAGS) $(TC_LDFLAGS)
	mv $@ ./
	rm -f ?*~
clean:
	rm -f $(BUILD_DIR)/* $(TARGETS) ?*~

objs_clean:
	rm -f $(BUILD_DIR)/*.o

.PHONY: all clean objs_clean
