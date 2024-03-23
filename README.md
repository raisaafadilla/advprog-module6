# advprog-module6

1. `handle connection` takes a mutable reference to a TCP stream. It sets up a buffered reader to read from the stream, reads lines from it until an empty line is encountered (indicating the end of the HTTP request headers), and collects these lines into a vector. Finally, it prints out the collected HTTP request. Essentially, it's a basic HTTP request parser for a server.
   
2. In the updated `handle_connection` method, we've discovered a crucial detail about how the server handles the `Content-Length` header. This header is adjusted based on the length of the response file content, particularly the content of `hello.html`. By employing `fs::read_to_string()`, the file's content is converted into a string, and its length is determined using the len() function. This adjustment ensures that the server accurately communicates the size of the response to the browser. If there are any issues reading the file, the program execution is halted. This approach ensures that when the program runs, it effectively retrieves, renders, and sends the content of `hello.html` as a response.
<img width="1400" alt="Screenshot 2024-03-23 at 11 51 47 PM" src="https://github.com/raisaafadilla/advprog-module6/assets/134634814/28cd58f7-5da8-4c67-9c3d-e6272764a8ad">

3. This updated code refines the `handle_connection` function to handle distinct types of HTTP requests. Initially, it sets up a buffered reader to process data from the TCP stream and extracts the first line of the request, assuming it's the request line. Then, it checks if the request is a GET request for the root path ("/"). If it is, the server responds with a 200 OK status and serves the content of `hello.html`. Conversely, if the request is anything else, indicating a resource not found, it responds with a 404 NOT FOUND status and serves the content of `404.html`. This refactoring was necessary to adjust responses based on the specific request received, improving the server's functionality and ensuring appropriate feedback to clients depending on their requests.
<img width="1401" alt="Screenshot 2024-03-24 at 12 25 17 AM" src="https://github.com/raisaafadilla/advprog-module6/assets/134634814/ec91859f-dd06-441b-9c3e-b5f78058c3fd">
   
4. The updated code in the `handle_connection` function uses a match statement to handle different HTTP requests. It responds with different status lines and serves different files based on the request. For the root path ("/"), it serves `hello.html` with a 200 OK status. For "/sleep", it delays the response before serving `hello.html`. This setup demonstrates how the server manages requests based on their types, ensuring appropriate responses for different scenarios.
   
5. A ThreadPool creates a fixed number of worker threads to handle tasks from a shared channel. The `ThreadPool::new` function establishes communication between the sender (the thread pool) and the receiver (worker threads) via a channel. When a task is ready, `ThreadPool::execute` sends it through the channel. Inside each worker thread's loop, they continuously await tasks from the channel, executing them upon reception. This efficient distribution enables parallel execution without thread creation overhead, enhancing performance by managing thread resources effectively. With this setup, servers can handle multiple requests concurrently, optimizing throughput and responsiveness, even with diverse task requirements such as potential delays from "/sleep" requests.
