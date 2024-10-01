# NamedPipes-Explorer-Windows

Polish version [here](./README.md)

# What is this program?

This tool is designed to simplify working with Named Pipes on Windows. It is a wrapper for the console program [PipeList](https://learn.microsoft.com/en-us/sysinternals/downloads/pipelist), from the [Sysinteranls](https://learn.microsoft.com/en-us/sysinternals/) suite, created using the Julia language. It uses the Blink and PowerShell libraries.

# How to run the program?

Here is the download link: [link]()

Additionally, you will need PowerShell; the version included with the system is sufficient.

And of course: [PipeList](https://learn.microsoft.com/en-us/sysinternals/downloads/pipelist)

By default, I assume it is registered as a system path, but you can also add it in the config.yaml file.

# Why was it created?

Because I couldn't find a suitable tool to facilitate working with named pipes. I wanted a graphical and free tool.

# What are named pipes?

Named Pipes are one of the inter-process communication (IPC) techniques available in Windows operating systems. They allow processes (even on different machines) to exchange data securely and efficiently. Unlike Anonymous Pipes (which are not associated with a named object), Named Pipes have unique names that allow processes to easily find and connect with each other.

How do Named Pipes work?

Named Pipes can be used in communication scenarios:

- Local (between processes running on the same computer)
- Network (between processes running on different computers in a network)

Each Named Pipe is represented as a resource in the file system with a unique name, e.g.:

pwsh

    \\.\pipe\pipe_name

Named Pipes operate based on a client-server mechanism, where one process acts as a server (creates and listens on the pipe), and another process acts as a client (connects and sends/receives data). Operating principles:

- Creation: The server creates a Named Pipe and assigns it a name.
- Listening: The server waits for a client to connect.
- Connection: The client opens the pipe and connects to the server.
- Communication: Data can be sent in both directions – bidirectional (Full Duplex) or unidirectional (Half Duplex).
- Closure: Once the data is processed, both sides close their connections.

### Advantages of Named Pipes

- Support for bidirectional communication: They allow data exchange in both directions (i.e., both the server and the client can send data simultaneously).
- Process independence: Processes communicating via Named Pipes can be independent of each other. They don't have to be parent-child processes.
- Multithreading: Named Pipes support multiple simultaneous connections, allowing the handling of many clients at once.
- Network compatibility: They enable easy communication between processes running on different computers in a network, which is important for distributed applications.
- Security: Windows implements Named Pipes with built-in Access Control List (ACL) mechanisms, allowing for secure access control and specifying which processes can use a particular pipe.
- Stream support: Named Pipes support data streams (byte streams), allowing for the transmission of various data types (including binary and text).

### Speed and efficiency of Named Pipes

Named Pipes in Windows are considered one of the most efficient forms of inter-process communication. In the context of same-computer communication, they work very quickly because the operating system can manage buffering and data transfer without involving the network or disks, minimizing delays.

### Factors affecting performance:

- Process location: If both processes run on the same machine, Named Pipes have performance similar to shared memory, as the operating system can buffer data without using network stacks.
- Buffering: Windows automatically buffers data in Named Pipes, minimizing delays when transmitting small pieces of data.
- Network usage: If Named Pipes are used in network scenarios, performance depends on network bandwidth and latency, though they still provide simplicity and ease of configuration.

Compared to other IPC methods, such as sockets, Named Pipes are usually faster in local scenarios, but in network scenarios, they may be outperformed by TCP sockets, which are more optimized for long-distance communication.
Use cases for Named Pipes

- Client-server applications: In scenarios where the server must handle multiple clients simultaneously (e.g., file servers, database servers).
- Communication between services: In applications where different services need to communicate (e.g., Windows system services).
- Network applications: Named Pipes can be used for data exchange between applications running on different machines in a network, making it easier to create distributed applications.