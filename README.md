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
```
Client:
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Waiting for client connection...")
c, addr = s.accept()
print("Connected to:", addr)
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:   
        break
    print("Requested IP:", ip)
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
s.close()

Server:
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    ip = input("Enter Logical Address: ")
    if ip.lower() == "exit":
        break
    s.send(ip.encode())
    mac = s.recv(1024).decode()
    print("MAC Address:", mac)
s.close()
```
## OUPUT - ARP
<img width="997" height="501" alt="image" src="https://github.com/user-attachments/assets/233207dc-f213-4f51-92a7-6983d5346117" />

## PROGRAM - RARP
```
Client:
import socket
s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("Waiting for client connection...")
c, addr = s.accept()
print("Connected to:", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}
while True:
    mac = c.recv(1024).decode()
    if not mac: 
        break
    print("Requested MAC:", mac)
    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
s.close()

Server:
import socket
s = socket.socket()
s.connect(('localhost', 9000))
while True:
    mac = input("Enter MAC Address: ")
    if mac.lower() == "exit":
        break
    s.send(mac.encode())
    print("Logical Address:", s.recv(1024).decode())
s.close()
```
## OUPUT -RARP
<img width="1006" height="262" alt="image" src="https://github.com/user-attachments/assets/818e99ad-1e82-470d-a4b5-8af1a4a5c61c" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
