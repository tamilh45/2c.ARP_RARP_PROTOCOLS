# 2c.SIMULATING ARP /RARP PROTOCOLS
### NAME   : V RAKSHA DHARANIKA
### REF NO : 212223230167
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
```PY
import socket

# Mock MAC address database
ARP_TABLE = {
    "192.168.1.1": "00:1A:2B:3C:4D:5E",
    "192.168.1.2": "00:1A:2B:3C:4D:5F",
    "192.168.1.3": "00:1A:2B:3C:4D:5G",
}

def start_server():
    # Create a socket object
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    server_socket.bind(('localhost', 12345))  # Bind to localhost and port 12345
    print("Server is running...")

    while True:
        # Receive data from client
        data, addr = server_socket.recvfrom(1024)
        ip_address = data.decode('utf-8')
        print(f"Received IP address: {ip_address} from {addr}")

        # Lookup MAC address
        mac_address = ARP_TABLE.get(ip_address, "Not Found")
        server_socket.sendto(mac_address.encode('utf-8'), addr)

if __name__ == "__main__":
    start_server()
```
## OUPUT - ARP
![image](https://github.com/user-attachments/assets/0d33598e-856f-49a3-baae-ff8f57fb1e61)

## PROGRAM - RARP
```PY
import socket

def request_mac_address(ip_address):
    # Create a socket object
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

    # Send IP address to server
    client_socket.sendto(ip_address.encode('utf-8'), ('localhost', 12345))

    # Receive MAC address from server
    mac_address, _ = client_socket.recvfrom(1024)
    print(f"MAC address for {ip_address} is: {mac_address.decode('utf-8')}")

if __name__ == "__main__":
    ip_to_lookup = input("Enter the IP address to convert to MAC address: ")
    request_mac_address(ip_to_lookup)
```
## OUPUT -RARP

![image](https://github.com/user-attachments/assets/506d8ac3-6c87-409a-be76-06a6f619d910)


## RESULT

Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
