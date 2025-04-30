# Centralized Calculation System in Java

This project implements a centralized calculation system that supports both TCP and UDP communication protocols. The system is designed to handle client requests for basic arithmetic operations and provides real-time statistics about the operations performed.

## Features

- **TCP Server**: Handles arithmetic operation requests from clients over TCP.
- **UDP Server**: Responds to discovery requests from clients over UDP.
- **Arithmetic Operations**: Supports addition, subtraction, multiplication, and division.
- **Statistics Tracking**: Tracks the number of valid and invalid operations, unique clients, and the sum of results.
- **Concurrency**: Uses multithreading to handle multiple client requests simultaneously.

## Project Structure

### Main Components

1. **`CCS.java`**  
   The entry point of the application. Starts both the TCP and UDP servers on the specified port.

2. **TCP Components**:
   - **`TCPServer.java`**: Listens for incoming TCP connections and spawns a new thread for each client.
   - **`TCPTaskHandler.java`**: Processes client requests, performs arithmetic operations, and sends responses.
   - **`TCPHandler.java`**: Manages low-level TCP communication (sending and receiving messages).
   - **`TCPStatisticsHandler.java`**: Tracks and prints statistics about operations and clients.

3. **UDP Components**:
   - **`UDPServer.java`**: Listens for incoming UDP packets and spawns a new thread to handle each packet.
   - **`UDPTaskHandler.java`**: Responds to discovery requests from clients.
   - **`UDPHandler.java`**: Manages low-level UDP communication (sending messages).

### File Overview

- **`CCS.java`**: Main class to start the system.
- **`TCPServer.java`**: TCP server implementation.
- **`TCPTaskHandler.java`**: Handles TCP client requests.
- **`TCPHandler.java`**: Utility for TCP communication.
- **`TCPStatisticsHandler.java`**: Tracks and prints statistics.
- **`UDPServer.java`**: UDP server implementation.
- **`UDPTaskHandler.java`**: Handles UDP client requests.
- **`UDPHandler.java`**: Utility for UDP communication.

## How to Run

1. **Compile the Project**:

    ```bash
    javac -d out src/*.java
    ```

2. **Run the Application**:

    ```bash
    java -cp out CCS <port>
    ```

- Replace \<port\> with the desired port number (1-65535).

3. **Client Interaction**:

- UDP: Send a "`CCS DISCOVER`" message to the server to receive a "`CCS FOUND`" response.
- TCP: Send arithmetic operation requests in the format:

    ```bash
    <OPERATION> <NUMBER1> <NUMBER2>
    ```

- Supported operations: `ADD`, `SUB`, `MUL`, `DIV`.

### Example Usage

UDP Discovery

1. Client sends: `CCS DISCOVER`
2. Server responds: `CCS FOUND`

TCP Arithmetic Operations

1. Client sends: `ADD 5 3`
2. Server responds: `8`

Invalid Operation

1. Client sends: `INVALID 5 3`
2. Server responds: `ERROR`

### Statistics

The system tracks the following statistics:

- Total and unique clients.
- Number of valid and invalid operations.
- Count of each operation type (ADD, SUB, MUL, DIV).
- Sum of all valid operation results.
- Statistics are printed every 10 seconds.

### Concurrency

The system uses multithreading to handle multiple clients simultaneously:

- Each TCP client connection is handled in a separate thread.
- Each UDP packet is processed in a separate thread.

### Error Handling

- Invalid port numbers or arguments result in an error message.
- Invalid or malformed client requests are responded to with `ERROR`.

### Dependencies

This project uses only standard Java libraries and does not require any external dependencies.
