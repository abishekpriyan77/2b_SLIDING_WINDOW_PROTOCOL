# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

# client.py
```
import socket
s = socket.socket()
s.connect(('localhost', 8970))
print("Connected to Server")

while True:
    data = s.recv(1026).decode()
    if not data:
        break
    print("Received:", data)
    s.send("Acknowledgement received from Client".encode())
```
# server.py
```
import socket
s = socket.socket()
s.bind(('localhost', 8970))
s.listen(5)
print("Server is waiting for connection...")
c, addr = s.accept()
print("Connected with: ", addr)
size = int(input("Enter number of frames to send: "))
frames = list(range(size))
window_size = int(input("Enter Window Size: "))
start = 0
i = 0

while True:
    while i < len(frames):
        end = start + window_size
        data = str(frames[start:end])
        c.send(data.encode())
        print("Sent:", data)
        ack = c.recv(1026).decode()
        if ack:
            print("Client:", ack)
        start += window_size
        i += window_size
```
## OUPUT
<img width="1206" height="325" alt="image" src="https://github.com/user-attachments/assets/da1d5796-e770-48d7-bdab-c66ec882426d" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
