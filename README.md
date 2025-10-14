# DNA Sequence Analysis Project

- This project processes DNA sequence data and calculate the pair frequencies (A,T,C,G) and visualize the results with a graph. The project utilizes two distinct file processing strategies to handle different levels of data complexity.

## Task 1 : Single-Line Sequence Data (task_1.ipynb)

Input File: data/dna_raw.txt

Solution : Pythonic List Slicing and zip()

### A. File Reading

- The file is read using file.readlines()

### B. Data Processing and Counting

- I am using this as zip() is a built-in Python function that takes multiple iterables (like lists, tuples, or strings) and aggregates elements from each of them.

- Slicing Headers: dna_data_list[::2] extracts lines at indices 0, 2, 4, etc. (all headers).

- Slicing Sequences: dna_data_list[1::2] extracts lines at indices 1, 3, 5, etc. (all sequences).

- Paired Iteration: The zip() function combines these two slices, ensuring the loop processes a perfect pair in each iteration: (header_id, sequence_letters).

- Cleaning : Strips newline characters and converts all to lowercase, to complete the case-insensitivity requirement.

- (Counting Loop) for char in sequence: if char in frequency_dict: => Iterates over every character in the clean sequence. The if condition acts as a filter, only incrementing the count for bases present in the predefined dna_letters list (A,T,C,G) and ignoring invalid characters (like N).

- final_result.append(...) => It stores the final, structured dictionary of counts for every sequence.

- Source for the zip() : https://www.geeksforgeeks.org/python/python-separate-odd-and-even-index-elements/

### Visualization

- Converting the structured data (final_result) into clear Bar Charts using matplotlib.pyplot.

- for result in final_result: => Ensures that the entire block of code is executed exactly once for every sequence (seq1, seq2, seq3, etc.), creating multiple charts.

- List Comprehension: Converts the dictionary (frequency_dict) into a list of numerical heights (frequencies). It uses the elements of dna_letters (A,T,C,G) as ordered keys for dictionary lookup (frequency_dict[l]).

- plt.figure(figsize=(6, 4)) => Creates a brand new, empty canvas with dimensions 6 inches wide by 4 inches tall. It prevents the data from seq2 from being plotted on the same figure as seq1.

- By including plt.yticks(range(0, max_freq + 2, 2)), I am telling Matplotlib " my ticks appear only on even integers.

- Source for the graph : https://www.geeksforgeeks.org/python/graph-plotting-in-python-set-1/, https://www.geeksforgeeks.org/python/plotting-multiple-bar-charts-using-matplotlib-in-python/, https://matplotlib.org/stable/
