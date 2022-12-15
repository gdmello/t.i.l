# Big-O Notation

* Measure the time and space complexities of an algorithm.
* Represents the algorithms worst case complexity

Major types of complexities:
* Constant: O(1) - good
* Linear time: O(n) - good
* Logarithmic time: O(n log n) - ok
* Quadratic time: O(n^2) - bad
* Exponential time: O(2^n) - bad
* Factorial time: O(n!) - very bad

# High/Low Order Bytes
In a number, usually the digit farthest to the left is the most significant (think salary number, the number to the left has the biggest impact to the whole number).

The high order byte is the byte that contains the largest portion of the number. e.g - a char in C is usually one byte and so is the High order byte, while an int is four bytes in size and the high order byte would be the one containing the largest value. [Source](https://stackoverflow.com/a/47117552/594083).

# Most Significant Bit (MSB)
The bit in a binary number with the largest value, usually the number farthest to the left, as the High order byte (above). e.g - in the binary number 10001, the MSB is 1, while the LSB is the 1 (the 1 farthest to the right). In this binary number 100100, the MSB is 1 while the LSB is 0.


# References
* [Big O Cheat Sheet – Time Complexity Chart - Joel Olawanle](https://www.freecodecamp.org/news/big-o-cheat-sheet-time-complexity-chart/)
* [most significant bit (MSB) - Robert Sheldon](https://www.techtarget.com/whatis/definition/most-significant-bit-or-byte)
