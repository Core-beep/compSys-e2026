CFLAGS=-Wall -Wextra -pedantic

all: mem args printf fwrite-simple fwrite-hpps fwrite-int fread-bytes

clean:
	rm -f mem args printf fwrite-simple fwrite-hpps fwrite-int fread-bytes

%: %.c
	gcc -o $@ $(CFLAGS) $^