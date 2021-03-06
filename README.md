# Multithreading Applications



## Text Processing with Multithreading

### Main Objective:

Count the number of words, words starting with vowels and words ending in consonants, efficiently,  by splitting processing load for worker threads.

### Multithreaded Implementation:

- Main thread processes the command line arguments.
- Main thread initializes the shared region array of structures with the given file names.
- Main thread creates the worker threads.
- Workers fetch one chunk at a time from a file to process in the shared region.
- Workers then save the results of the processing of the chunk.
- Finally, the main thread prints the final results.


### How to compile:

	gcc -Wall -g -O3 -o prog1 main.c sharedRegion.c textProcUtils.c

### How to run:

Arguments:

	-h --- print usage
	-f --- filename to process
	-n --- number of threads
	-m --- maximum number of bytes per chunk

Example:

	./prog1 -f texts/text0.txt -f texts/text1.txt -n 8 -m 2000



## Matrix Determinant Calculation with Multithreading

### Main Objective 
Given a file with matrices, calculate the determinant of each one, efficiently, by splitting processing load for worker threads.

### Multithreaded Implementation:
- Main thread processes the command line arguments.
- Main thread creates the worker threads.
- Main thread reads each matrix of each file.
- Each matrix is inserted in a Shared Memory in a FIFO.
- Workers retrieve and process the matrix, calculating the determinant.
- Workers insert results in the Shared Memory.
- When all files have been processed, the main thread retrieves and presents the results.

### How to compile:

	gcc -Wall -g -O3 -o prog2 main.c matrixutils.c sharedregion.c -pthread -lm

### How to run:

Arguments:

	-h --- print usage
	-f --- filename to process
	-n --- number of threads
	-k --- size of fifo queue in monitor

Example:

	./prog2 -f shortMatrix/mat128_64.bin -f shortMatrix/mat128_32.bin -k 8 -n 4
