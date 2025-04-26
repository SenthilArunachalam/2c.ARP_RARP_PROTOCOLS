# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
## server
~~~
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter logical Address: ")
    s.send(ip.encode())
    mac = s.recv(1024).decode()
    print("MAC Address:", mac)
~~~
## client
~~~
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connected to {addr}")

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()
    if not ip:
        break  # if connection is closed
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
~~~
## OUPUT - ARP
## Server
![2c-server-output](https://github.com/user-attachments/assets/0be3c217-0376-430b-b3d3-28e17fa18789)
## Client
![2c-client-output](https://github.com/user-attachments/assets/5aa8b3d5-6d34-4624-ba7f-1600c95704bb)

## PROGRAM - RARP
## server
~~~
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA"};
while True:
    mac=c.recv(1024).decode()
    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())

~~~
## client
~~~
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    mac=input("Enter logical address: ")
    s.send(mac.encode())
    print("MAC Address",s.recv(1024).decode())
~~~
## OUPUT -RARP
## server
![server2cr](https://github.com/user-attachments/assets/d4ba1ce1-a34c-411f-a845-9e665dd18f2f)

## client
![client 2cr](https://github.com/user-attachments/assets/5e7e188a-cd55-4773-9e73-cae555d8923b)

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
