# docker-compose-lb-scaling-non-swarm
Scaling the docker containers in non swarm mode and load balancing the requests using HaProxy.

In this article i am presenting how to scale containers in single node and with load balancing 
requests across the containers using haproxy.

- Loadbalancing the containers having different ports.
- Loadbalancing the containers having the same ports.


### HAPROXY

- Haproxy is offen called as a High Availability proxy .
- Its one of open source solution for providing the load balancing of the requests.
- It is one of the popular load balancer.
- It uses a single process ,event driven model.
- Haproxy hanldes a large number of concurrent requests like nginx.
- Haproxy provides a dashboard to monitor the requests.
- Haproxy is TCP/Http Loadbalancer (Layer 4) Loadbalancer.
- Layer 4 Loadbalancer simply transfer the packets to the server with out veirfying the 
  content.
- TCP is the layer4 Protocol for Http traffic on the internet.
- Layer 4 makes the limitied routing decesion on the packets.
- Haproxy distributes the workload between multiple servers /or multiple docker containers.
- Haproxy also prvovides the reverse proxy solution.

## No Load Balancing - What will happnen

- Consider the bleow diagram

![No Loadbalncer](https://user-images.githubusercontent.com/5623861/56404534-d388ff80-6299-11e9-91e3-30185ac31d52.png)

- There is no load balancing between the servers.
- Alwayas request will goes to the one server.
- if that server getting overloaded and will impact the performance of the application.
- When server gets down there is no availability of the application.

## Types of loadbalancing

- Layer 4 Load balancing
- Layer 7 Load balancing

## Layer 4 Loadbalancing

- Also refered as Transport layer Loadbalancing.
- This loadbalancer doesnot inspect the packets contenct.
- Loadbalancing will happend based on the ip range or domain URL or using port.
- Haproxy provides the layer 4 loadbalancing .
- Below diagram explains the how layer4 load balancing.
- Here we are not going to expose the IP Address of the servers to any of the the users

![Layer 4 load balancing](https://user-images.githubusercontent.com/5623861/56405776-6331ac80-62a0-11e9-887f-434bc9449f15.png)

![Layer4_Typeii](https://user-images.githubusercontent.com/5623861/56408528-8a3fac80-62a7-11e9-9708-43025f9d5c3a.png)

- Loadbalancing will be happend between servers.
- If any server down all the requests will be routed to other two servers.
- Load balancer will uses the different load balancing algorithoms to route the requests.

## Layer 7 Load balancing

- Also referred as Application Layer Load balancing.
- This load balancer inspect the what content user sending .
- Routing of the requests totally based on the content 
- In this users will run the multiple web servers on the same domain and port.

![Layer7_Type_II](https://user-images.githubusercontent.com/5623861/56408505-6bd9b100-62a7-11e9-9917-d8080b53327f.png)

- Multiple servers will run same domain URL.

### Introduction to HAPROXY and Terminology 

 ## ACL 
 
 -  Offently refered as Access Control List.
 -  This one is used to verify the conditiona and Perform the actions.
 -  ACL contains the Operators : AND ,OR ,Negate(!).
 -  Using ACL operators we can perepare conditions (if ,unless ,eq).
 - 
 ## backend
 -  backend refers the servers which recieves forwarded requests from frontend.
 -  backend consist of two parameters.
        - List of servers and ports.
        - Load balancing algorithioms.
 -  backend contains the group of servers which receives the reqests form the frontend.
 -  requests will load balanced by using the load balancing algorithoms.
 -  all this information will be mentiong haproxy configuration file.
  
  ```      
        backend applicationserver
            balance roundrobin
            mode http
            server app1 com.study.pattern:80 check 
            server app2 com.study.pattern:80 check
 ```
 
 ## frontend
 
 - frontend defines how requests should be forwarded to backend
 - frontend contains the 
      1.set of IP address and port
      2.ACL's
      3.Backend rule which is already defined in backend
      4.Also we can define the 
         Transport layer loadbalancer.
         Application layer loadbalancer.
    
### Haproxy Load balancer algorithoms

    - Round Robin
    - Least connection - 
    - Source - Dependson user/Source IP
    - Sticky Sessions -
    - Health Check
    
    
 
        
        
        
 

