Types of computing environments:
1. Distributed System : comp takes place over network over diff hosts 
2. Heterogenous Systems 
# Communication
1. Socketbased (java.net): endpoints of two way connections between two distributed components that can communicate 
2. RMI(Remote Method Invocation) (java.rmi) : allows distributed components to be manipulated as if they were on the same host 
# Socket Based Communication 
- Server Socket : waits for request from client 
- Client Socket : used ot send or recieve data 
## Ports
- Server socket listens at a specific port 
- port is a +ve integer kless than or equal to 65565
- ports 1 to 1023 are reserved for admin purposes ( 23 telnet , 25 email , 80 HTTP)
## Typical use of sockets
```java
try{
	Socket socket = new Socket(host,port);
	BufferedReader in = new BufferedReader(
		new InputStreamReader(
			socket.getOutputStream()
		));
		//send and recieve al data 
		in.close();
		out.close();
		socket.close();
}catch(IOException e){
	e.printStackTrace();
}

```
