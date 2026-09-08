CFLAGS=-g -Wall -Wextra -pedantic #-fsanitize=address

all: first showfile pointers arrays stack sanitize passing printf fwrite-simple

first: first.c
	gcc first.c -o first $(CFLAGS)

showfile: showfile.c
	gcc showfile.c -o showfile $(CFLAGS)

pointers: pointers.c
	gcc pointers.c -o pointers $(CFLAGS)

arrays: arrays.c
	gcc arrays.c -o arrays $(CFLAGS)

stack: stack.c
	gcc stack.c -o stack $(CFLAGS)

sanitize: sanitize.c
	gcc sanitize.c -o sanitize $(CFLAGS)

passing: passing.c
	gcc passing.c -o passing $(CFLAGS)

printf: printf.c
	gcc printf.c -o printf $(CFLAGS)

fwrite-simple: fwrite-simple.c
	gcc fwrite-simple.c -o fwrite-simple $(CFLAGS)

clean:
	rm -f first showfile pointers arrays stack sanitize passing printf fwrite-simple

