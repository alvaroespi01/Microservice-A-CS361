# Microservice-A-CS361

### Prerequisites
To run the program, you will need to install some dependencies and prerequisites. 
* Install ZeroMQ.
  - Install via npm: 'npm install zmq'
    
* Install pandas
  - Install via pip: 'pip install pandas'
  - For further information: https://pandas.pydata.org/docs/user_guide/index.html
 
* Install CORS
  - Install via npm: 'npm install cors'
    
* The file must be in '.JSON' format before proceeding

## A. Request
To make a request, you will need to create a socket requesting ZeroMQ to communicate with the microservice. This file be sent to the microservice for processing. The microservice will then return a CSV file. 

```
 try {
        const socket = new zmq.Request();

        await socket.connect("tcp://localhost:5555"); 
        await socket.send(JSON.stringify(json_data)); 
    }
```

## B. Receive
Once the request is processed, a .CSV formatted file will be received from the microservice. You will need to implement a socket to receive the response and handle the received data.
Example code for receiving the processed CSV file. 
```
try {
    ...
    await socket.send(JSON.stringify(json_data));

    const [csv_data] = await socket.receive();

    res.setHeader('Content-Disposition', 'attachment; filename=data.csv');
    res.setHeader('Content-Type', 'text/csv');
    res.send(csv_data.toString());
} 
```

## C. UML Sequence Diagram


<img width="554" alt="UML Sequqnce Diagram" src="https://github.com/user-attachments/assets/355164b2-9fed-4ee8-9e90-5993259859b8" />


Note: Ensure your backend server is running on localhost:3000 and your Python microservice is listening on localhost:5555.
