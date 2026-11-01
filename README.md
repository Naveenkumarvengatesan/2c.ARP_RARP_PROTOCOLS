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

Server:
~~~
import socket

table = {"192.168.1.10": "00:1A:2B:3C:4D:5E", "192.168.1.20": "00:1A:2B:3C:4D:5F"}

with socket.socket() as s:
    s.bind(("localhost", 9000))
    s.listen(1)
    c, _ = s.accept()
    with c:
        while ip := c.recv(1024).decode():
            c.send(table.get(ip, "Not Found").encode())
~~~

Client:

~~~
import socket

with socket.socket() as s:
    s.connect(("localhost", 9000))
    while ip := input("Enter logical address: "):
        s.send(ip.encode())
        print("MAC address:", s.recv(1024).decode())
~~~


## OUPUT - ARP


<img width="1892" height="235" alt="image" src="https://github.com/user-attachments/assets/a0da8b8a-bac5-47a4-b8f5-ec6bf9dca621" />



## PROGRAM - RARP

Server:
~~~
import socket

table = {"00:1A:2B:3C:4D:5E": "192.168.1.10", "00:1A:2B:3C:4D:5F": "192.168.1.20"}

with socket.socket() as s:
    s.bind(("localhost", 6000))
    s.listen(1)
    c, _ = s.accept()
    with c:
        while mac := c.recv(1024).decode():
            c.send(table.get(mac, "Not Found").encode())
~~~

Client:
~~~
import socket

with socket.socket() as s:
    s.connect(("localhost", 6000))
    while mac := input("Enter MAC address: "):
        s.send(mac.encode())
        print("Logical address:", s.recv(1024).decode())
~~~


## OUPUT -RARP


<img width="1917" height="287" alt="image" src="https://github.com/user-attachments/assets/e74b5c82-0f63-4741-b0c3-70cccbd659df" />



## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
