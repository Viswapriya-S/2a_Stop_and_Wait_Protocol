# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
First, establish a connection between the sender and the receiver.
The sender transmits one data frame to the receiver.
After sending the frame, the sender stops and waits for an acknowledgment (ACK) from the receiver.
The receiver receives the frame and checks it for errors.
If the frame is received correctly, the receiver sends an ACK to the sender.
Upon receiving the ACK, the sender sends the next data frame.
If the sender does not receive an ACK within a specified time, it assumes the frame was lost or damaged.
The sender then retransmits the same frame.
This process continues until all frames are successfully transmitted and acknowledged.
Finally, the connection between sender and receiver is terminated.
## CODE
CLIENT
```
import socket
import time
client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)  
while True:
    msg = input("Enter a message (or type 'exit' to quit): ")
    client.send(msg.encode())  
    if msg.lower() == 'exit':  
        print("Connection closed by client")
        client.close()
        break
    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        continue
```
SERVER
```
import socket
server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")
conn, addr = server.accept()
print(f"Connected with {addr}")
while True:
    data = conn.recv(1024).decode()

    if data:
        print(f"Received: {data}")
        conn.send("ACK".encode())

        if data.lower() == 'exit':  
            print("stop and wait protocol implemented successfully")
            conn.close()
            break
```

##OUTPUT

Client.py
<img width="1080" height="544" alt="image" src="https://github.com/user-attachments/assets/a0a689e7-f162-4b7c-ac8c-7c5cd24ddddf" />


Server.py

<img width="936" height="543" alt="image" src="https://github.com/user-attachments/assets/5d81c187-15a4-4697-a333-92b51b446756" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
