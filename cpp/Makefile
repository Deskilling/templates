PROJECT  := template

BUILD_DIR := bin
OBJ_DIR   := obj
SRC_DIR   := src

CC      := g++
# -std=c++ 	which c++ standart to use
# -Wall 	enables common warnings
# -Wextra 	enables additional warnings
# -I. 		adds the current directory to the header search path
# -MMD		enables generation of .d files next to each .o file (important for the Makefile)
# -MP		generates dummy rules for the .d files (also important for the Makefile)
CFLAGS  := -std=c++23 -Wall -Wextra -I. -MMD -MP
# -l links math
LDFLAGS := -lm

# search recursively in SRC_DIR for .c files
SRC_S := $(shell find $(SRC_DIR) -name "*.cpp")
# for SRC_S replace every file with the same layout but in OBJ_DIR and .o extension
OBJ_S := $(SRC_S:$(SRC_DIR)/%.cpp=$(OBJ_DIR)/%.o)
# for OBJ_S replace .o with .d
DEPS := $(OBJ_S:.o=.d)

TARGET := $(BUILD_DIR)/$(PROJECT)

.PHONY: all clean

all: $(TARGET)

$(BUILD_DIR):
	mkdir -p $@

$(TARGET): $(OBJ_S) | $(BUILD_DIR)
	$(CC) -o $@ $(OBJ_S) $(LDFLAGS)

$(OBJ_DIR)/%.o: $(SRC_DIR)/%.cpp
	@mkdir -p $(dir $@)
	# -c no linking
	# -o build .o
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -rf $(BUILD_DIR) $(OBJ_DIR)

-include $(DEPS)
