# 2a_Stop_and_Wait_Protocol

### NAME  : RAMPRASATH R
### REF NO: 212223220086
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

### Server Code :
```PY
import socket

def start_server():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    server_socket.bind(('localhost', 12345))
    print("Server is listening on port 12345")

    while True:
        data, client_address = server_socket.recvfrom(1024)
        print(f"Server received frame: {data.decode()}")
        
        # Send ACK
        ack = "ACK"
        server_socket.sendto(ack.encode(), client_address)
        print("Server sent ACK")

if __name__ == "__main__":
    start_server()
```
### Client Code :
```PY
import socket
import time

def start_client(frame_size):
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    server_address = ('localhost', 12345)

    for i in range(5):  
       
        frame = f"Frame {i + 1}: " + 'X' * (frame_size - len(f"Frame {i + 1}: ")) 
        print(f"Client sending: {frame}")

        # Send the frame to the server
        client_socket.sendto(frame.encode(), server_address)

        # Wait for ACK
        ack, _ = client_socket.recvfrom(1024)
        print(f"Client received: {ack.decode()}")

        # Simulate Stop and Wait behavior
        time.sleep(1)  

    client_socket.close()

if __name__ == "__main__":
    frame_size = int(input("Enter the frame size: "))
    start_client(frame_size)
```



## OUTPUT
### Server :
![image](https://github.com/user-attachments/assets/bb424cb0-e7f7-422c-94c1-a0a713fa2a0e)

### Client Code :
![image](https://github.com/user-attachments/assets/49f89eb6-8dd2-4e7e-8fc9-f705a6efc64f)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
