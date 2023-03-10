# Distributed Health Record System
This project was part of the course CI-0123 "Proyecto Integrador de Sistemas Operativos y Redes de 
Comunicación de Datos". It consists of a distributed system to save and retrieve patients' medical records. The infrastructure involves various nodes written in Python. 

The final user (medical staff) can access the system using a computer through a simple website. This website is running in a node called the Frontend Node. It has to communicate through the network with a second node, the Storage Interface, which is connected to a structure of different nodes working as a distributed storage system to allow redundancy and availability of the information; we named it the Backend.

The Frontend Node does not use a web server like Django or Flask, but uses our implementation of a web server that parses HTTP. The Frontend communicates with the distributed storage system using a custom text-based protocol that we created for the purpose of the course. 

All the nodes in the Backend infrastructure works in pairs and communicate with each other using a custom UDP protocol. When a new code is added to the network, it tries to find a new partner by broadcasting UDP messages through the network. If there is another node without a partner, they started to interchange messages to confirm that they are both available and then start to work together. If one of them already had information stored, it shares all of it with the other node. In case one of the nodes stops unexpectedly, the other has a full copy of the data. Therefore, the system continues working properly.

Each node in the backend has a simple file system built from scratch. This implementation contains a virtual memory and TLB systems. All the medical records are store in Byte Arrays buffers.

All the communication between the Frontend, Storage Interfaces and the Backend Nodes is done though web sockets with encrypted connections.

## Documentation
In the root folder of the project, you can find a file named "Docs" that contains a detail explanation of the protocols that we implemented.