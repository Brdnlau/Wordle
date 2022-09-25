# Design Document


## Purpose
*The purpose of this program is to implement the popular word guessing game, Wordle.*


## Structure
*The structure of this program will be as follows:*


#### 1. `score_guess`
This function returns true if the guess is an exact match with the secret word. It fills the string result with an x for letters in guess but not in secret, y for letters in guess and secret, but not at the correct spot, and g for letters in guess and secret and at the correct spots.

Using an if statement, strncmp is called to check if the guess and secret word are an exact match. If it is equal to zero, then it is an exact match, and strncpy is used to set result as 'ggggg', returning true after. A for loop is then used to iterate the guess, with a bool to see if a match is found. An inner for loop is used to iterate through the secret word. If the current letter in guess is also aletter in secret, then the indexes are checked with an if statement to see if they are the same. If they are, that index in result is set to 'g' and if they aren't, it is set to 'y'. In both cases, matchis set to true and the inner for loop is broken. If the bool is false, then we set the current index to 'x'. The 5th index of result is set to the null terminator after both loops, and false is returned. 

#### 2. `valid_guess`
This function returns true if the guess is a word in the vocabulary input and false if it is not. It uses a binary search algorithm inspired by section.

Ints start, end and mid are initialized as zero, the number of words in the input, and (end - start)/2 + start, respectively. While the start is less than or equal to the end, 3 conditions are checked with if statements. The guess is checked to see if it is after or before the mid with strncmp. If it is less than zero, then end is set to 1 less than mid and if it is greater, start is set to 1 more than mid. If it is zero, true is returned. Mid is then reset using the initial equation after the if statements. False is then returned.


#### 3. `cmp_string`
This function is inspired by the man page, it takes 2 strings and compares them, returning a value compatible with qsort.


#### 4. `**load_vocabulary`
This function reads an input file and adds all the 5 letter words in it into a dynamically allocated array that is returned. 

The output array is first initialized and memory for 10 elements is allocated using calloc. The number of words is kept track of with a `size_t` and set to 0. To keep track of how many elemenets are allocated, an int is set to 10. The input file is opened and a while loop is used with fgets to read every line. Using strnup, the buffer is copied to the index of the output array using the number of words as reference. The int holding the number of words is incremented up by 1. Then, and if statement will be used to check if the number of words is equal to or greater than the amount allocated. If it is, realloc is used to add another 10 elements to the output array. After this loop, the file is closed and the output array is returned.

#### 5. `free_vocabulary`
This function frees all the memory used by the function `**load_vocabulary`.

Using a for loop, each element in input array is freed. The array is then freed afterwards. 
