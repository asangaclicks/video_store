#############################################################################
# VideoStore
#

OBJ_DIR = ../obj
BIN_DIR = ../bin

DIRS=$(OBJ_DIR) $(BIN_DIR)
OBJS=$(OBJ_DIR)/VideoStore.o $(OBJ_DIR)/Movie.o $(OBJ_DIR)/Rental.o $(OBJ_DIR)/Customer.o
TOBJS=$(OBJ_DIR)/Movie_t.o $(OBJ_DIR)/Rental_t.o $(OBJ_DIR)/Customer_t.o
EXE=$(BIN_DIR)/VideoStore $(BIN_DIR)/Movie_t $(BIN_DIR)/Rental_t $(BIN_DIR)/Customer_t

CC= g++
CFLAGS=-Wall

.PHONY: all
all: $(DIRS) $(EXE) test

# VideoStore
.PHONY: run
run: $(DIRS) $(BIN_DIR)/VideoStore
	@$(BIN_DIR)/VideoStore

# bin dir
$(BIN_DIR):
	mkdir $@

# bin dir
$(OBJ_DIR):
	mkdir $@

$(BIN_DIR)/VideoStore: $(OBJS)
	$(CC) $^ -o $@

$(OBJ_DIR)/VideoStore.o: VideoStore.cpp Movie.hpp Rental.hpp Customer.hpp
	$(CC) $(CFLAGS) -c $< -o $@

# Movie
$(OBJ_DIR)/Movie.o: Movie.cpp Movie.hpp
	$(CC) $(CFLAGS) -c $< -o $@

$(BIN_DIR)/Movie_t: $(OBJ_DIR)/Movie_t.o $(OBJ_DIR)/Movie.o
	$(CC) $^ -o $@

$(OBJ_DIR)/Movie_t.o: Movie_t.cpp Movie.hpp
	$(CC) $(CFLAGS) -c $< -o $@

# Rental
$(OBJ_DIR)/Rental.o: Rental.cpp Rental.hpp Movie.hpp
	$(CC) $(CFLAGS) -c $< -o $@

$(BIN_DIR)/Rental_t: $(OBJ_DIR)/Rental_t.o $(OBJ_DIR)/Rental.o $(OBJ_DIR)/Movie.o
	$(CC) $^ -o $@

$(OBJ_DIR)/Rental_t.o: Rental_t.cpp Rental.hpp
	$(CC) $(CFLAGS) -c $< -o $@

# Customer
$(OBJ_DIR)/Customer.o: Customer.cpp Customer.hpp Movie.hpp Rental.hpp
	$(CC) $(CFLAGS) -c $< -o $@

$(BIN_DIR)/Customer_t: $(OBJ_DIR)/Customer_t.o $(OBJ_DIR)/Customer.o $(OBJ_DIR)/Rental.o $(OBJ_DIR)/Movie.o
	$(CC) $^ -o $@

$(OBJ_DIR)/Customer_t.o: Customer_t.cpp Customer.hpp
	$(CC) $(CFLAGS) -c $< -o $@

# clean
.PHONY: clean
clean: cleanobjects
	rm -f $(EXE)

.PHONY: cleanobjects
cleanobjects:
	rm -rf $(DIRS) $(OBJS) $(TOBJS)

# unit testing
.PHONY: test
test: $(DIRS) $(BIN_DIR)/Movie_t $(BIN_DIR)/Rental_t $(BIN_DIR)/Customer_t
	@$(BIN_DIR)/Movie_t
	@$(BIN_DIR)/Rental_t
	@$(BIN_DIR)/Customer_t
