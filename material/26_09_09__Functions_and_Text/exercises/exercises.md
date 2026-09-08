# Exercises

## RISC-V

The following exercises will train you in writing more
complicated RISC-V programs.
You will be given pseudocode or C programs, and asked to write similar
programs in RISC-V assembly.

It is up to you to decide how to test them.

You must use [RARS](https://github.com/TheThirdOne/rars) to develop,
test, and run these programs.  [See this guide on using
RARS](../../../tools/rars.md).

## What to Learn From This Exercise
At this stage in the course we are not too concerned with your knowledge of 
assembly. Later on a whole section will be given over to computer architecture
and you'll be expected to complete an assignment using assembly, but that is 
not to the end of the course. For now this is mostly to illustrate to you that
underneath all of the concepts and features we will be introducing in the next
few months, what is really taking place are millions of these simple 
manipulations of a small amount of registers. 

I expect that playing around by hand with these problems will be the best way
of illustrating quite how complex even these simple problems can be at this low
level, but you may be able to get the same outcome with tools like LLMs, 
reading, or watching videos.

Additionally, there are some exercises to help you get started on A0. Note that
they're intentionally _similar_ to the tasks in A0 but slightly altered. You 
should be able to use your solutions to these exercises in A0 but may need some
minor alternations to do so. 

### Fibonacci function

Implement the standard recursive definition of the Fibonacci function:

    fib(n) = if n < 2 then 1 else fib(n-1) + fib(n-2)

*Don't* rewrite it to be an iterative loop instead.  Yes, that's more
efficient, but it will not give you experience with function calls in
RISC-V.  Assume that `n` is provided in `a0`, and similarly produce
the result in `a0`.

#### Hints

* See the heavily commented [fact.s](fact.s) program.  Computing
  Fibonacci numbers is very similar.  You should structure your
  implementation the same way (although you don't need to use
  multiplication).

* You will need at least three words of stack space.

### Array equality

The following C function is a simplified version of the standard C
function ``memcmp``:

```C
int memeq(unsigned char *p1, unsigned char *p2, int n) {
  for (int i = 0; i < n; i++) {
    if (p1[i] != p2[i]) {
      return 0;
    }
  }
  return 1;
}
```

It returns 1 if the `n` bytes at `p1` and `p2` are identical, and
otherwise 0.  Recall that C represents *false* as zero and *true* as
non-zero.

Write this function in RISC-V assembly.  Accept `p1`, `p2`, and `n` in
`a0-a2`, and return the result in `a0`.

### Array search

The following C function is a simplified version of the standard C
function `memmem`:

```C
unsigned char* memfind(unsigned char *haystack, int haystacklen,
                       unsigned char *needle, int needlelen) {
  for (int i = 0; i < haystacklen-needlelen; i++) {
    if (memeq(haystack+i,needle,needlelen)) {
      return haystack+i;
    }
  }
  return NULL;
}
```

It tries to find the array `needle` (of length `needlelen`) in the
array `haystack` (of length `haystacklen`).  If it can be found, it
returns the starting address of the match.  Otherwise it returns NULL
(`0`).

Write this function in RISC-V assembly.  Accept parameters in `a0-a3`
and return the result in `a0`.  Use your definition of of `memeq` from
the previous exercise as a helper function.

### Stalin sort

Stalin Sort is a particularly brutal *O(n)* sorting algorithm where
every element that is not in sorted order is simply removed.  We can
implement it in C as such:

```C
int stalinsort(int *array, int n) {
  if (n == 0) {
    return 0;
  }

  int prev = array[0];
  int i = 1;
  for (int j = 1; j < n; j++) {
    if (prev <= array[j]) {
      prev = array[j];
      array[i] = prev;
      i++;
    }
  }
  return i;
}
```

We can't change the size of the array, so instead we move the elements
and return the new size.

Write this function in RISC-V assembly.  Accept parameters in `a0-a1`
and return the result in `a0`.

# Data Formatting

The following used to be the introductory assignment but its been demoted to exercise (and shortened a bit to suit). 

The purpose of this exercise is to get you more familiar with C, and a couple
command-line utilities common to a Unix-like development environment.
What better way to do that, than try to implement one of these yourself?

file(1)1 is a classical Unix-like command-line utility for guessing the type
of a file. In a Unix-like operating system, it is often the contents, or the 
metadata of a file, not a filename extension, that determines the “type” of a
file. Standard file(1) uses clever heuristics to guess the file type. Here, we
will implement a basic variant of this tool in C.

We will only discern between the following small subset of the many possible 
file encodings.

* empty: An empty file has 0 bytes.

* ASCII text: An ASCII text file only contains characters from a particular subset of the ASCII-table.

* ISO-8859-1 text: An ISO-8859-1 text file, also known as latin1, originat ing in 1987. It uses 8 bits instead of 7, and encodes most Latin alphabets, including Faroese, Icelandic, and Danish.

* UTF-8 text: There are more Unicode (universal encoding) standards, but here we will only look at UTF-8 text. These standards aim to encompass the characters required to represent all the world’s languages, and are variable-width encodings (i.e., the number of bytes per character depends on the character). UTF-8 is today the predominant universal encoding. The later UTF-16 (which we do not work with) is regarded as an alternative, not an improvement over UTF-8.

* data: Everything not covered by the previous categories is considered data.

Write a self-contained (one-file) C program, which accepts a single argument.
If the given argument is a path to a file that exists, and the type of that 
file can be determined, write the determined file type to stdout. More in 
depth definitons of the different file types are presented below. You can use
the provided data in the exercises/test_data directory to test on.

## empty
This file type must be reported if the file contains no bytes.

## ASCII text
This file type must be reported if all bytes belong to the following set:

  {0x07, 0x08, . . . 0x0D}∪{0x1B}∪{0x20, 0x21, . . . , 0x7E}


## ISO-8859 text
This file type should be reported if the file composed of ISO-8859-1-like
bytes. These include all ASCII-like bytes (see above), and also decimal
values 160–255. The decimal values 128–159 are not part of ISO-8859-
1, and their appearance might indicate that the file really is a UTF-8-
encoded text file. (Why?)

## UTF-8 Unicode text
This file type should be reported if the file is composed of UTF-8-like
characters. UTF-8 is a variable-length encoding where each subsequent
byte of a character begins with a designated bit-sequence. The following
table summarises the encoding:
Number of Bytes Byte 1 Byte 2 Byte 3 Byte 4
1 0xxxxxxx
2 110xxxxx 10xxxxxx
3 1110xxxx 10xxxxxx 10xxxxxx
4 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx

## data
This file type must be reported in case no other type matche
