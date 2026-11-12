# PA1 Design — ETP/1 Client and Server

## 1. Architecture

etp.py has the encode/decode protocol. 
Transport_tcp.py has the transport seam. 
Server.py has the session logic. 
Client.py has the client logic.

## 2. The transport seam

Transport_tcp.py is the transport seam.
 
The six operations that were implemented are as follows: listen, accept, connect, send_all, recv_exact, and close.

No other file imports socket or calls any of the socket functions.

For PA2, all the other functions should stay the same. transport_tcp.py will need to be changed to UDP and transport.py will also need to import the UDP file.

## 3. Framing

It reads a message from a byte stream by first unpacking the header which determines how many bytes will be in the payload. 

A header that arrives in pieces is handled in transport_tcp.py with a while loop. This makes sure that the whole message is received and not into the next.
 
VERSION and LENGTH are checked in etp.py in the read_message function. This is done before reading a payload because it needs to know if the version is valid and how many bytes to read next.

## 4. Concurrency

The threading module is being used so when there is a stall, it is only that specific module that is paused.

There is no state shared and right now if two clients tried a PUT and a GET at the same time it would most likely cause data corruption.

## 5. Errors and disconnects

Non-fatal errors are handled by an ERROR message and still keeps the connection open. Fatal Errors will throw an exception which will close the connection.

If a client disconnects in the middle of a large file request, Python will raise a BrokenPipeError or ConnectionResetError because that portion of the code is wrapped in a try except block.

It exits 0 on success, 1 if an ERROR, 2 if anything else that went wrong: bad arguments, cannot connect, the connection ended early, a response that fails the checks above, a local file that cannot be read or written, 3  if the PUT_OK digest hash doesn’t match the SHA-256 of the data sent.   

## 6. Threat model

Anyone connecting over the network could attack this server. This is because there is no authentication. The server resists path traversal attacks because it uses the section 7 rules. An attack that it doesn’t resist is packet tampering. An attacker could alter the payload in the middle of a send. It also doesn’t resist resource exhaustion. If someone wanted to they could overwhelm the server with PUT requests.

## 7. Testing

_What did you test beyond `etp_selfcheck.py`? How? Name one bug your testing
found, how you found it, and the fix._
