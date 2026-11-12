# PA1 Capture Analysis

## How I captured it

File Size: 262144 bytes

```
mkdir -p server-files evidence scratch
head -c 262144 /dev/urandom > scratch/photo.bin
./etp-server --port 5000 --root server-files
sudo tshark -i lo -s 200 -f "tcp port 5000" -w /tmp/pa1-capture.pcap
C="./etp-client --host 127.0.0.1 --port 5000 --name Thepigeon0516"
$C put scratch/photo.bin photo.bin
$C get photo.bin scratch/copy.bin
ss -tan state time-wait '( sport = :5000 or dport = :5000 )' > evidence/time-wait.txt
sudo mv /tmp/pa1-capture.pcap evidence/
sudo chown $USER evidence/pa1-capture.pcap
```

## Facts

```etp-facts
server_port: 5000
client_port: 34392
client_isn: 1069284391           # raw sequence number in the client's SYN
server_isn: 3606832780           # raw sequence number in the server's SYN/ACK
client_mss: 65495                # MSS option value in the client's SYN, in bytes
server_to_client_payload_bytes: 262189 # all TCP payload bytes the server sent in this session (HELLO_OK + GET_OK + BYE_OK)
server_to_client_data_segments: 9 # server-to-client frames with payload, across all three responses, counted as captured
first_fin_from: server                  # server or client
```

## Q1. The handshake

Segment 1: Frame Number: 25, Flag: SYN, Raw Sequence Number: 1069284391, Acknowledgment Number: 0.
Segment 2: Frame Number: 26, Flag: SYN/ACK, Raw Sequence Number: 3606832780, Acknowledgment Number: 1069284392.
Segment 3: Frame Number: 27, Flag: ACK, Raw Sequence Number: 1069284392, Acknowledgment Number: 3606832781.
The acknowledgment number in the third segment is 3606832781 because it is based off of the SYN flag from the server. It is found by incrementing the sequence number by 1.
The client advertised a MSS of 65495. This is the max that Linux allows.

## Q2. Your protocol on the wire

GET request frame: 32. First 8 Payload Bytes: 01 03 00 00 00 00 00 09. VERSION: 01, TYPE: 03, STATUS: 00, RESERVED: 00, LENGTH: 00 00 00 09.
GET_OK frame: 33. First 8 Payload Bytes: 01 83 00 00 00 04 00 00. VERSION: 01, TYPE: 83, STATUS: 00, RESERVED: 00, LENGTH: 00 04 00 00.
GET_OK's equals the size of the file. 0x00040000 = 262144 in decimal.
Arithmetic: We have a total of 262189 bytes. The HELLO_OK has an 8 byte header and a 21 byte payload = 29 bytes. GET_OK also has an 8 byte header and a 262144 byte payload = 262152 bytes. BYE_OK has an 8 byte header and a 0 byte payload = 8 bytes. Total: 29 + 262152 + 8 = 262189 bytes.

## Q3. A byte stream, not messages

There were 7 GET_OK Segments. Their sizes were: 32768, 32768, 61440, 47360, 22272, 47360, 18184. 
They were not all the same size. 
None of them exceeded the MSS (65495). 
The one message spanned several segments. 
This means that a message cant rely on just one recv() function call. This is why we have the while len(buffer) < n loop in transport_tcp.py. 

## Q4. Teardown and TIME-WAIT

The server sent the first FIN. The specification says that the server closes after replying to a BYE with BYE_OK. 
Relevant Line: Recv-Q Send-Q Local Address:Port Peer Address:Port 
                0      0          127.0.0.1:5000    127.0.0.1:34392
The server end is in time wait because it sent the first FIN. Linux keeps it there for about 60 seconds. 
Because of this we are using SO_REUSEADDR because if we didnt, the server wouldnt be able to restart until the timer ends.

## Q5. What an observer learns

If someone got this file, they would learn the ip addresses, the port numbers, the protocol version, the sequence of messages, the name of the requested file, the size, and all the timing information.
Using a 200 byte snap length would hide the payload contents but not any of the headers.
Using TLS would stop someone from seeing things like the file name and contents but it would still not hide things like the IP addresses and the port numbers.