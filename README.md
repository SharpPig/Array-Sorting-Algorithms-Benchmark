# Array Sorting Algorithms Benchmark

This Java program benchmarks various sorting algorithms including Insertion Sort, Heap Sort, Merge Sort, and Quick Sort with and without cutoffs. It generates arrays of different sizes, sorts them using the mentioned algorithms, and measures the execution time for each algorithm.

## Usage

1. Clone the repository or download the `ArraySorting.java` file.
2. Compile the Java file using `javac ArraySorting.java`.
3. Run the compiled class file using `java ArraySorting`.

## Sorting Algorithms

### Insertion Sort

Insertion sort is a simple sorting algorithm that builds the final sorted array one item at a time.

### Heap Sort

Heap sort is a comparison-based sorting algorithm that builds a heap from the input array and then repeatedly extracts the maximum element from the heap.

### Merge Sort

Merge sort is a divide and conquer algorithm that divides the input array into two halves, recursively sorts each half, and then merges the sorted halves.

### Quick Sort

Quick sort is a divide and conquer algorithm that picks an element as a pivot and partitions the array around the pivot.

### Quick Sort with Cutoff

This variation of quick sort incorporates a cutoff mechanism where if the subarray size is below a certain threshold, it switches to insertion sort to improve performance.

## Benchmark Results

The program prints the execution time of each sorting algorithm for various array sizes. The output includes the array size followed by the execution time for each algorithm.

## Note

- You can adjust the range of random numbers generated in the array by modifying the `generateRandomArray` method.
- The cutoff values for Quick Sort with Cutoff can be adjusted by modifying the `cutoff` array in the main method.

## Contributors

Feel free to contribute by enhancing the code or adding more sorting algorithms!
