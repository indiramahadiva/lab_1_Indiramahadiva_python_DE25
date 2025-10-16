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

### C. Visualization

- Converting the structured data (final_result) into clear Bar Charts using matplotlib.pyplot.

- for result in final_result: => Ensures that the entire block of code is executed exactly once for every sequence (seq1, seq2, seq3, etc.), creating multiple charts.

- List Comprehension: Converts the dictionary (frequency_dict) into a list of numerical heights (frequencies). It uses the elements of dna_letters (A,T,C,G) as ordered keys for dictionary lookup (frequency_dict[l]).

- plt.figure(figsize=(6, 4)) => Creates a brand new, empty canvas with dimensions 6 inches wide by 4 inches tall. It prevents the data from seq2 from being plotted on the same figure as seq1.

- By including plt.yticks(range(0, max_freq + 2, 2)), I am telling Matplotlib " my ticks appear only on even integers.

- Source for the graph : https://www.geeksforgeeks.org/python/graph-plotting-in-python-set-1/, https://www.geeksforgeeks.org/python/plotting-multiple-bar-charts-using-matplotlib-in-python/, https://matplotlib.org/stable/

## Task 2: Multi-Line Sequence Data (task_2.ipynb)

Input File: data/dna_raw_complicated.txt

The Solution : "Process the Previous" (The main idea behind my code is to only process and save a completed sequence when you find the starting line of the next one. The header line (>seq...) acts as a trigger )

Description

- This code parses a DNA data file (dna_raw_complicated.txt) where genetic sequences can be split across multiple lines. It reads the file, groups the lines for each sequence, counts the frequency of the nucleotides (A, T, C, G), and generates a bar chart for each sequence to visualize the results.Counter for frequency counting (the collections module, which is part of the Python Standard Library. It comes included with Python, so I don't need to install it. Counter is a specialized dictionary subclass for counting hashable objects.) Matplotlib for creating graphs and visualizations in Python. I have to install it separately (e.g., using pip install matplotlib).

### A. File Reading

- The file is read using file.readlines()

### B. Function Definition and Execution

1. Initialization
   Before the loop starts, I set up :

   - final_result = []: An empty list to hold your final, completed results.

   - seq_id = None: A variable to hold the name of the sequence you're currently collecting. It's empty because it hasnt started yet.

   - current_sequence_lines = []: A temporary list to gather all the DNA fragments for the current sequence.

2. The Main Loop

   - If the line is a header (>): This is the trigger. It's time to process the previous sequence. The code joins all the fragments it has gathered in current_sequence_lines, counts the letters, and appends the final dictionary to final_result. Then, it resets seq_id and current_sequence_lines to start fresh for the new sequence.

   - If the line is a DNA line : The code simply adds this line to the current_sequence_lines list. It doesn't do any counting yet; it just collects the piece and waits for the next one.

3. The Final Cleanup
   - After the loop finishes, the very last sequence is still sitting in current_sequence_lines. It was never processed because no new > header came after it to act as a trigger.My code block after the loop handles this specific case. It runs the same counting and saving logic one last time to ensure the final sequence isn't forgotten.

Sources : https://www.geeksforgeeks.org/python/counters-in-python-set-1/, https://www.w3schools.com/python/ref_string_join.asp, https://www.w3schools.com/python/python_lists_comprehension.asp
