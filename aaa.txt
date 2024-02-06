import java.util.Arrays;
import java.util.Random;

public class ArraySorting {
		public static void main(String[] args) {
				int[] arraySizes = {100, 50, 500, 1000, 2000, 5000, 10000};

				System.out.println("Array Size | Insertion | Heap | Merge | Quick");
				System.out.println("--------------------------------------------------");

				for (int size : arraySizes) {
						int[] randomArray = generateRandomArray(size);

						long startTime, endTime;

						// Insertion Sort
						startTime = System.nanoTime();
						insertionSort(Arrays.copyOf(randomArray, randomArray.length));
						endTime = System.nanoTime();
						long insertionTime = endTime - startTime;

						// Heap Sort
						startTime = System.nanoTime();
						heapSort(Arrays.copyOf(randomArray, randomArray.length));
						endTime = System.nanoTime();
						long heapTime = endTime - startTime;

						// Merge Sort
						startTime = System.nanoTime();
						mergeSort(Arrays.copyOf(randomArray, randomArray.length));
						endTime = System.nanoTime();
						long mergeTime = endTime - startTime;

						// Quick Sort without CUTOFF
						startTime = System.nanoTime();
						quickSort(Arrays.copyOf(randomArray, randomArray.length));
						endTime = System.nanoTime();
						long quickTimeWithoutCutoff = endTime - startTime;

						// Quick Sort with CUTOFF options (10, 50, 200)
						for (int cutoff : new int[]{10, 50, 200}) {
								startTime = System.nanoTime();
								quickSortWithCutoff(Arrays.copyOf(randomArray, randomArray.length), cutoff);
								endTime = System.nanoTime();
								long quickTimeWithCutoff = endTime - startTime;

								System.out.printf("%-12d%-12d%-8d%-8d%-8d%-8d%-8d\n",
												size, insertionTime, heapTime, mergeTime, quickTimeWithoutCutoff, quickTimeWithCutoff, cutoff);
						}
				}
		}

		// Method to generate a random integer array
		private static int[] generateRandomArray(int size) {
				int[] array = new int[size];
				Random random = new Random();
				for (int i = 0; i < size; i++) {
						array[i] = random.nextInt(1000); // You can adjust the range based on your requirements
				}
				return array;
		}

		// Insertion Sort
		private static void insertionSort(int[] array) {
				int n = array.length;
				for (int i = 1; i < n; ++i) {
						int key = array[i];
						int j = i - 1;

						while (j >= 0 && array[j] > key) {
								array[j + 1] = array[j];
								j = j - 1;
						}
						array[j + 1] = key;
				}
		}

		// Heap Sort
		private static void heapSort(int[] array) {
				int n = array.length;

				// Build heap
				for (int i = n / 2 - 1; i >= 0; i--) {
						heapify(array, n, i);
				}

				// Extract elements from heap one by one
				for (int i = n - 1; i > 0; i--) {
						// Move current root to end
						int temp = array[0];
						array[0] = array[i];
						array[i] = temp;

						// Call max heapify on the reduced heap
						heapify(array, i, 0);
				}
		}

		private static void heapify(int[] array, int n, int i) {
				int largest = i;
				int left = 2 * i + 1;
				int right = 2 * i + 2;

				if (left < n && array[left] > array[largest]) {
						largest = left;
				}

				if (right < n && array[right] > array[largest]) {
						largest = right;
				}

				if (largest != i) {
						int swap = array[i];
						array[i] = array[largest];
						array[largest] = swap;

						heapify(array, n, largest);
				}
		}

		// Merge Sort
		private static void mergeSort(int[] array) {
				if (array.length > 1) {
						int mid = array.length / 2;
						int[] leftArray = Arrays.copyOfRange(array, 0, mid);
						int[] rightArray = Arrays.copyOfRange(array, mid, array.length);

						mergeSort(leftArray);
						mergeSort(rightArray);

						merge(array, leftArray, rightArray);
				}
		}

		private static void merge(int[] array, int[] leftArray, int[] rightArray) {
				int i = 0, j = 0, k = 0;

				while (i < leftArray.length && j < rightArray.length) {
						if (leftArray[i] <= rightArray[j]) {
								array[k++] = leftArray[i++];
						} else {
								array[k++] = rightArray[j++];
						}
				}

				while (i < leftArray.length) {
						array[k++] = leftArray[i++];
				}

				while (j < rightArray.length) {
						array[k++] = rightArray[j++];
				}
		}

		// Quick Sort
		private static void quickSort(int[] array) {
				quickSort(array, 0, array.length - 1);
		}

		private static void quickSort(int[] array, int low, int high) {
				if (low < high) {
						int pi = partition(array, low, high);

						quickSort(array, low, pi - 1);
						quickSort(array, pi + 1, high);
				}
		}

		private static int partition(int[] array, int low, int high) {
				int pivot = array[high];
				int i = low - 1;

				for (int j = low; j < high; j++) {
						if (array[j] <= pivot) {
								i++;

								int temp = array[i];
								array[i] = array[j];
								array[j] = temp;
						}
				}

				int temp = array[i + 1];
				array[i + 1] = array[high];
				array[high] = temp;

				return i + 1;
		}

		// Quick Sort with CUTOFF
		private static void quickSortWithCutoff(int[] array, int cutoff) {
				quickSortWithCutoff(array, 0, array.length - 1, cutoff);
		}

		private static void quickSortWithCutoff(int[] array, int low, int high, int cutoff) {
				if (high - low <= cutoff) {
						insertionSort(Arrays.copyOfRange(array, low, high + 1));
						return;
				}

				int pi = partition(array, low, high);

				quickSortWithCutoff(array, low, pi - 1, cutoff);
				quickSortWithCutoff(array, pi + 1, high, cutoff);
		}
}
