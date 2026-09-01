CC=gcc
CFLAGS=-Wall -Wextra -pedantic -std=c18

all: helloworld error args sum roll side_one side_two

helloworld: helloworld.c
	$(CC) helloworld.c -o helloworld $(CFLAGS)

error: error.c
	$(CC) error.c -o error $(CFLAGS)

args: args.c
	$(CC) args.c -o args $(CFLAGS)

sum: sum.c
	$(CC) sum.c -o sum $(CFLAGS)

roll: roll.c
	$(CC) roll.c -o roll $(CFLAGS)

side_one: side_one.c
	$(CC) side_one.c -o side_one $(CFLAGS)

side_two: side_two.c
	$(CC) side_two.c -o side_two $(CFLAGS)

clean:
	rm -f helloworld error args sum roll side_one side_two
