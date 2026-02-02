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

# create socket
s = socket.socket()

# connect to server
s.connect(('localhost', 8000))

while True:
    msg = input("Enter data: ")
    s.send(msg.encode())
    ack = s.recv(1024).decode()
    print("Server:", ack)
```
SERVER
```
import socket
# create socket
s = socket.socket()
# bind IP and port
s.bind(('localhost', 8000))
# listen for client
s.listen(1)
print("Server waiting for connection...")
# accept client
c, addr = s.accept()
print("Connected from", addr)
while True:
    data = c.recv(1024).decode()
    if not data:
        break
    print("Client:", data)
    c.send("ACK received".encode())
c.close()
```

##OUTPUT

Client.py
<img width="799" height="334" alt="Screenshot 2026-02-02 205243" src="https://github.com/user-attachments/assets/36b35084-098b-4466-aa06-59d653b5486f" />


Server.py
<img width="816" height="325" alt="Screenshot 2026-02-02 205402" src="https://github.com/user-attachments/assets/9cb066df-ceb0-4434-ac3a-711eea4e2d7b" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
