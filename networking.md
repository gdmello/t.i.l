Basics
======
Bits are basic units of computing storage. 0 or 1 can be the two values of a bit.
 * Bit patterns can be computed from the number of bits
 * 1 bits yield 2 patterns, i.e. 0 or 1
 * 2 bits yield 00, 01, 10, 11 or 4 patterns
 * In general n bits yield 2<sup>n</sup> patterns
 
A Byte is a collection of 8 bits.
 * one byte can store a single character

Great Read - https://web.stanford.edu/class/cs101/bits-bytes.html

IP Addresses
============
An IPv4 address is of the form - `XXX.XXX.XXX.XXX`
or `0.0.0.0` to `255.255.255.255` or yet still `[0-255].[0-255].[0-255].[0-255]`
To be able to store the numbers 0-255 as bits would require a bit pattern of at least 256. 
8 bits yields 2<sup>8</sup> or 256 bit patterns. Perfect! So each number in an IPv4 address is 8 bits of storage.

So, a single IPv4 address, consisting of 4 numbers, would require `4*8` or 32 bits of storage.
Taking this further, 32 bits gives us 2<sup>32</sup> patterns, which is the total number of IP addresses possible in the IPv4 range.
