program_NAME := ../bin/linux/ccmd_test 

program_CXX_SRCS := $(wildcard *.cpp)
program_CU_SRCS := $(wildcard *.cu)
program_CXX_OBJS := ${program_CXX_SRCS:.cpp=.o}
program_CU_OBJS := ${program_CU_SRCS:.cu=.o}
program_OBJS := $(program_C_OBJS) $(program_CXX_OBJS)

BUILD_DIR := ../build/linux/
program_OBJS := $(addprefix $(BUILD_DIR), $(program_OBJS))
VPATH = ./ 

# NVCC_PATH = /usr/local/cuda/bin
# CUTIL_LIB = /export/home/tps24/mtb/NVIDIA_GPU_Computing_SDK/C/common/inc
# CUDA_INCLUDE = /usr/local/cuda/include
# CUDA_LIB = /usr/local/cuda/lib
# BOOST_INCLUDE = /home/tps24/mtb/boost_1_49_0
BOOST_INCLUDE = /opt/local/include
CCMD_LIB = ../bin/linux 

# program_INCLUDE_DIRS := $(CUDA_INCLUDE) $(BOOST_INCLUDE) ../src/include
program_INCLUDE_DIRS := $(BOOST_INCLUDE) ../src/include
program_LIBRARY_DIRS := $(CCMD_LIB) /opt/local/lib
program_LIBRARIES := ccmd
# program_LIBRARY_DIRS := $(CUDA_LIB) $(CCMD_LIB)
# program_LIBRARIES := ccmd # cuda cudart

CPPFLAGS += $(foreach includedir,$(program_INCLUDE_DIRS),-I$(includedir))
CPPFLAGS += -I$(CUTIL_LIB)
CPPFLAGS += -O3 -Wall -fPIC

LDFLAGS += $(foreach librarydir,$(program_LIBRARY_DIRS),-L$(librarydir))
LDFLAGS += $(foreach library,$(program_LIBRARIES),-l$(library))
LDFLAGS += -lboost_thread-mt

.PHONY: all clean distclean

all: $(program_NAME)

#bodysystemcuda.o: bodysystemcuda.cu bodysystemcuda.cpp
#	$(NVCC_PATH)/nvcc -O3 --include-path $(CUTIL_LIB) -c bodysystemcuda.cu 

$(program_NAME): $(program_OBJS)
	$(LINK.cc) $(program_OBJS) $(CPPFLAGS) $(LDFLAGS) -o $(program_NAME)
#	$(CXX) -static $(LDFLAGS) $(CPPFLAGS) $(program_OBJS) -lccmd -o $(program_NAME)
#	$(LINK.cc) $(CPPFLAGS) $(program_OBJS) -o $(program_NAME)

$(program_OBJS) : $(program_CXX_SRCS)
	$(CXX) $(CPPFLAGS) -c $< -o $@

clean:
	@- $(RM) $(program_NAME)
	@- $(RM) $(program_OBJS)

distclean: clean
