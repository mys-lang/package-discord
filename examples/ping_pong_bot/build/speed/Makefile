LIB = /home/erik/workspace/mys/mys/mys/lib
#export CCACHE_BASEDIR = /home/erik/workspace/mys/mys/mys
export CCACHE_SLOPPINESS = pch_defines,time_macros,include_file_mtime,include_file_ctime

BUILD := build/speed
GCH := $(BUILD)/mys_pre_
MYS_CXX ?= ccache $(CXX)
MYS ?= /usr/bin/python3 -m mys
CFLAGS += -I$(LIB)
CFLAGS += -I$(LIB)/3pp/include
CFLAGS += -I$(BUILD)/cpp/include
CFLAGS += 
# CFLAGS += -Wall
CFLAGS += -Wno-unused-variable
CFLAGS += -Wno-unused-value
CFLAGS += -Wno-return-type
# CFLAGS += -Wno-parentheses-equality
# CFLAGS += -Wno-unused-but-set-variable
CFLAGS += -Winvalid-pch
CFLAGS += -O3
CFLAGS += -std=c++17
CFLAGS += -fdata-sections
CFLAGS += -ffunction-sections
CFLAGS += -fdiagnostics-color=always
ifeq ($(COVERAGE), yes)
CFLAGS += -DMYS_COVERAGE
TRANSPILE_COVERAGE = --coverage
endif
ifeq ($(UNSAFE), yes)
CFLAGS += -DMYS_UNSAFE
endif
ifeq ($(TRACEBACK), yes)
CFLAGS += -DMYS_TRACEBACK
endif
ifeq ($(TEST), yes)
CFLAGS += -DMYS_TEST
OBJ_SUFFIX = test.o
GCH := $(GCH)test.hpp
else
ifeq ($(APPLICATION), yes)
CFLAGS += -DMYS_APPLICATION
GCH := $(GCH)app.hpp
else
GCH := $(GCH).hpp
endif
OBJ_SUFFIX = o
endif
LDFLAGS += -std=c++17
# LDFLAGS += -static
# LDFLAGS += -Wl,--gc-sections
LDFLAGS += -fdiagnostics-color=always
LDFLAGS += -L$(LIB)/3pp/lib
LIBS += -lpcre2-32
LIBS += -luv
LIBS += -lpthread
LIBS += -ldl
LIBS += 
SRC += $(BUILD)/cpp/src/ping_pong/main.mys.cpp
SRC += $(BUILD)/cpp/src/fiber/lib.mys.cpp
SRC += $(BUILD)/cpp/src/discord/client.mys.cpp
SRC += $(BUILD)/cpp/src/discord/lib.mys.cpp
SRC += $(BUILD)/cpp/src/argparse/lib.mys.cpp
OBJ += $(BUILD)/cpp/src/ping_pong/main.mys.$(OBJ_SUFFIX)
OBJ += $(BUILD)/cpp/src/fiber/lib.mys.$(OBJ_SUFFIX)
OBJ += $(BUILD)/cpp/src/discord/client.mys.$(OBJ_SUFFIX)
OBJ += $(BUILD)/cpp/src/discord/lib.mys.$(OBJ_SUFFIX)
OBJ += $(BUILD)/cpp/src/argparse/lib.mys.$(OBJ_SUFFIX)
EXE = $(BUILD)/app
TEST_EXE = $(BUILD)/test

all:
	$(MAKE) -f $(BUILD)/Makefile $(BUILD)/transpile 
	$(MAKE) -f $(BUILD)/Makefile $(EXE)

test:
	$(MAKE) -f $(BUILD)/Makefile $(BUILD)/transpile 
	$(MAKE) -f $(BUILD)/Makefile $(TEST_EXE)

$(BUILD)/transpile: ./src/main.mys /home/erik/workspace/mys/mys/mys/lib/packages/fiber/src/lib.mys ../../src/client.mys ../../src/lib.mys build/dependencies/mys-argparse-latest/src/lib.mys
	$(MYS) $(TRANSPILE_DEBUG) transpile $(TRANSPILE_COVERAGE) \
	-n ping_pong -p . -s no -m yes -n fiber -p /home/erik/workspace/mys/mys/mys/lib/packages/fiber -s yes -m no -n discord -p ../.. -s yes -m no -n discord -p ../.. -s yes -m no -n argparse -p build/dependencies/mys-argparse-latest/ -s yes -m no -o $(BUILD)/cpp main.mys lib.mys client.mys lib.mys lib.mys
	touch $@


$(TEST_EXE): $(OBJ) $(BUILD)/mys.$(OBJ_SUFFIX)
	$(MYS_CXX) $(LDFLAGS) -o $@ $^ $(LIBS)

$(EXE): $(OBJ) $(BUILD)/mys.$(OBJ_SUFFIX)
	$(MYS_CXX) $(LDFLAGS) -o $@ $^ $(LIBS)

%.mys.$(OBJ_SUFFIX): %.mys.cpp $(GCH).gch
	$(MYS_CXX) $(CFLAGS) -include $(GCH) -c $< -o $@

%.cpp.o: %.cpp
	$(MYS_CXX) $(CFLAGS) -c $< -o $@

$(GCH).gch: $(LIB)/mys.hpp
	$(MYS_CXX) $(CFLAGS) -c $< -o $@

$(BUILD)/mys.$(OBJ_SUFFIX): $(LIB)/mys.cpp $(GCH).gch
	$(MYS_CXX) $(CFLAGS) -include $(GCH) -c $< -o $@
