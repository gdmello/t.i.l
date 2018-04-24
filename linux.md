Basics
======
Pipes
-----
Transfer output from one program to another. Good source - http://www.linfo.org/pipes.html

Reaping
=======
* Linux kernel boots an init process on startup, i.e. a process which has no parent process.
* Each parent process might spawn one or more child processes, similar to a tree structure.
* When each child process terminates after completion, the parent process must wait on the child process to collect information like it's exit code.
* If the child process has terminated, but not been waited on by it's parent, it's referred to as a `zombie` process.
* The process of calling `waitpid()` on a child to avoid it being a zombie is called 'reaping'.
ref - https://blog.phusion.nl/2015/01/20/docker-and-the-pid-1-zombie-reaping-problem/

