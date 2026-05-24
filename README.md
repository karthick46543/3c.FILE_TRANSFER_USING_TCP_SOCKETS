# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
```
SERVER

import socket

port = 60000
s = socket.socket()

host = socket.gethostname()

# Bind socket
s.bind((host, port))

# Listen for client
s.listen(5)

print("Server waiting for connection...")

while True:
    conn, addr = s.accept()
    print("Connected by:", addr)

    data = conn.recv(1024)
    print('Server received:', repr(data))

    filename = 'mytext.txt'

    # Open file in binary mode
    f = open(filename, 'rb')

    l = f.read(1024)

    # Send file data
    while l:
        conn.send(l)
        print('Sent:', repr(l))
        l = f.read(1024)

    f.close()

    print('Done sending')

    conn.send('Thank you for connecting'.encode())

    conn.close()

CLIENT

import socket

s = socket.socket()

host = socket.gethostname()
port = 60000

# Connect to server
s.connect((host, port))

# Send request message
s.send("Hello server!".encode())

# Receive file
with open('mytext.txt', 'wb') as f:

    while True:
        print('Receiving data...')

        data = s.recv(1024)

        print('data =', data)

        if not data:
            break

        f.write(data)

print('Successfully received the file')

s.close()

print('Connection closed')
```

## OUPUT

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c1e55ff2-23b0-415f-8484-de107f9e691e" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was successfully created and executed.
