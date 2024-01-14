NVCC=nvcc

###################################
# These are the default install   #
# locations on most linux distros #
###################################

OPENCV_LIBPATH=/usr/lib
OPENCV_INCLUDEPATH=$(shell pkg-config opencv4 --cflags)

###################################################
# On Macs the default install locations are below #
###################################################

#OPENCV_LIBPATH=/usr/local/lib
#OPENCV_INCLUDEPATH=/usr/local/include

# or if using MacPorts

#OPENCV_LIBPATH=/opt/local/lib
#OPENCV_INCLUDEPATH=/opt/local/include

OPENCV_LIBS:=$(shell pkg-config opencv4 --libs)

CUDA_CPP_STD_FLAG=--std=c++11
CUDA_INCLUDEPATH=-I/usr/local/cuda-5.0/include

######################################################
# On Macs the default install locations are below    #
# ####################################################

#CUDA_INCLUDEPATH=/usr/local/cuda/include
#CUDA_LIBPATH=/usr/local/cuda/lib

NVCC_OPTS=-O3 -Xcompiler -Wall -Xcompiler -Wextra -m64

GCC_OPTS=-O3 -Wall -Wextra -m64

student: main.o student_func.o compare.o reference_calc.o Makefile
	$(NVCC) -o HW1 main.o student_func.o compare.o reference_calc.o -L $(OPENCV_LIBPATH) $(OPENCV_LIBS) $(NVCC_OPTS)

main.o: main.cpp timer.h utils.h reference_calc.cpp compare.cpp hw1.h
	g++ -c main.cpp $(GCC_OPTS) $(CUDA_INCLUDEPATH) $(OPENCV_INCLUDEPATH)

student_func.o: student_func.cu utils.h
	nvcc $(CUDA_CPP_STD_FLAG) -c student_func.cu $(NVCC_OPTS)

compare.o: compare.cpp compare.h
	g++ -c compare.cpp $(OPENCV_INCLUDEPATH) $(GCC_OPTS) $(CUDA_INCLUDEPATH)

reference_calc.o: reference_calc.cpp reference_calc.h
	g++ -c reference_calc.cpp $(OPENCV_INCLUDEPATH) $(GCC_OPTS) $(CUDA_INCLUDEPATH)

clean:
	rm -f *.o *.png hw
