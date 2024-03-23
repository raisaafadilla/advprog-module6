# advprog-module6

1. `handle connection` takes a mutable reference to a TCP stream. It sets up a buffered reader to read from the stream, reads lines from it until an empty line is encountered (indicating the end of the HTTP request headers), and collects these lines into a vector. Finally, it prints out the collected HTTP request. Essentially, it's a basic HTTP request parser for a server.
