# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
# NAME : Ragupathi P
# REGISTER NO : 212221040135

## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
### CLIENT
```
import socket

s = socket.socket()
port = 60000
s.connect(('localhost', port))
s.send("Hello server!".encode())

with open('received_file', 'wb') as f:
    while True:
        print('receiving data...')
        data = s.recv(1024)
        print('data=%s' % (data))
        if not data:
            break
        f.write(data)

print('Successfully get the file')
s.close()
print('connection closed')
```
### SERVER
```
import socket

port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind(('localhost', port))
s.listen(5)

while True:
    conn, addr = s.accept()
    data = conn.recv(1024)
    print('Server received', repr(data))

    filename = 'myfile.txt'
    f = open(filename, 'rb')
    l = f.read(1024)
    while l:
        conn.send(l)
        print('Sent', repr(l))
        l = f.read(1024)
    f.close()

    print('Done sending')
    conn.send('Thank you for connecting'.encode())
    conn.close()

```
## OUTPUT
### CLIENT
![image](https://github.com/NaliniG007/3c.FILE_TRANSFER_USING_TCP_SOCKETS/assets/143526042/0761e361-bc54-4364-81cb-456689ff2e8c)



### SERVER
![image](https://github.com/NaliniG007/3c.FILE_TRANSFER_USING_TCP_SOCKETS/assets/143526042/b555dbdd-a1d2-4c48-9c5c-882f8fbfc9ad)

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
