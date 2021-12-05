all: clean build

build:
	gcc -c -Wall -Werror -Wextra *.c
	ar -rc libblas.a *.o

clean:
	rm -rf *.o *.a
