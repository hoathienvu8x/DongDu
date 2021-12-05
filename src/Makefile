CC = g++
CFLAGS = -c -O3 -std=c++11 -Wall
LDFLAGS = -L./liblinear/blas -lblas
SOURCES = Feats.cpp Machine.cpp SylMap.cpp FeaturesSelection.cpp DicMap.cpp StrMap.cpp
OBJECTS = $(SOURCES:.cpp=.o)
OBJECTS := $(addprefix objects/,$(OBJECTS))
PREDICTOR = preditctor
LEARNER = learner

all: objects blas $(SOURCES) $(PREDICTOR) $(LEARNER)

objects:
	@mkdir -p objects

blas:
	@cd liblinear/blas && $(MAKE) all

$(PREDICTOR): $(OBJECTS) objects/tron.o objects/linear.o objects/preditctor.o
	$(CC) $(OBJECTS) objects/tron.o objects/linear.o objects/preditctor.o -o $@ $(LDFLAGS)

$(LEARNER): $(OBJECTS) objects/tron.o objects/linear.o objects/learner.o
	$(CC) $(OBJECTS) objects/tron.o objects/linear.o objects/learner.o -o $@ $(LDFLAGS)

objects/linear.o: liblinear/linear.cpp liblinear/linear.h
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS)

objects/tron.o: liblinear/tron.cpp liblinear/tron.h
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS)

objects/learner.o: learner.cpp
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS)

objects/predictor.o: predictor.cpp
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS)

objects/%.o: %.cpp
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS)

clean:
	rm -rf objects/*.o $(PREDICTOR) $(LEARNER)
