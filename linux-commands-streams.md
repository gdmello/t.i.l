# I/O Streams
A file descriptor is a number which represents a file or a stream. 
An I/O stream in Linux is one of - stdin, stdout or stderr.
Processes use streams to collect input and return output.

## I/O Stream Operators

`>` - redirects output to stdout, overwriting the output destination.
```
  echo 'Heaven is real' > myfile.txt
  cat myfile.tx
    Heaven is real
```    
`>>` - similar to the redirect operator above, but appends instead of overwriting.
`<` - collects input from other sources like devices (keyboard, mouse), files, other processes
`2>` - the stderr redirect operator.
I/O streams have a static file descriptor number -
* stdin - 0
* stdout - 1
* stderr - 2

`2>&1` - redirect stderr `2>` to the what stdout is currently pointing to (a reference)

# Source
[LinuxJouney.com](https://linuxjourney.com/lesson/stderr-standard-error-redirect)
