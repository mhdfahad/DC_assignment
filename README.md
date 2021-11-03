**<u>Name</u>** : Mohammed Fahad 
<u>**BITS ID**</u>             : 2021MT12151
<u>**Subject Name**</u>: Distributed Computing
<u>**Subject Code**</u>  : SSZG526



# Ricart-Agrawala Algorithm for Distributed Mutual Exclusion

The aim of this assignment is to gain hands-on experience regarding the implementation of Ricart-Agrawala algorithm using any programming language.

## Overview

Ricart-Agrawala algorithm assumes the communication channels are FIFO. The algorithm uses two types of messages: REQUEST and REPLY.

* A process sends a REQUEST message to all other processes to request their permission to enter the critical section. A process sends a REPLY message to a process to give its permission to that process.

* Processes use Lamport-style logical clocks to assign a timestamp to critical section requests and timestamps are used to decide the priority of requests.

* Each process pi maintains the Request-Deferred array, RDi, the size of which is the same as the number of processes in the system.

* Initially, ∀i ∀j: RDi[j]=0. 

  Whenever p~i~ defer the request sent by p~j~, it sets RD~i~[j]=1 and after it has sent a REPLY message to p~j~
  it sets RD~i~[j]=0.

## Implementation Details

#### **Requesting the critical section:**

* When a site Si wants to enter the CS, it broadcasts a timestamped REQUEST message to all other sites.
* When site S~j~ receives a REQUEST message from site S~i~, it sends a REPLY message to site S~i~if site S~j~
  is neither requesting nor executing the CS, or if the site S~j~ is requesting and S~i~’s request’s
  timestamp is smaller than site S~j~’s own request’s timestamp.Otherwise, the reply is deferred and S~j~ sets RD~j~[i]=1

#### **Executing the critical section:**

* Site S~i~ enters the CS after it has received a REPLY message from every site it sent a REQUEST message to.

#### **Releasing the critical section:**

* When site S~i~ exits the CS, it sends all the deferred REPLY messages: ∀~j~ if RD~i~[j]=1, then send a REPLY message to S~j~ and set RD~i~[j]=0.

## Performance

* For each CS execution, Ricart-Agrawala algorithm requires (N − 1) REQUEST messages and (N − 1) REPLY messages.
* Thus, it requires 2(N − 1) messages per CS execution.
* Synchronization delay in the algorithm is T.



## Assumptions during the Implementation

* The nodes do not fail

* The number of nodes are known and defined before-hand



## Programming Requirements

The algorithm is implemented in java programming language. The requirements for implementation are:

* **Operating System**: Ubuntu 16.04
* **Programming language**:  Java
* **Java Version**: 1.8.0_161
* **Java SE Runtime Environment**: 1.8.0_161-b12
* **Java VM**: 64-bit Server (build 25.161-b12)



## Run Details

* Define the number of nodes `N` in the `config.txt` file along with their IP and port addresses.

  **content of config.txt**

  3
  0 127.0.0.1 4051
  1 127.0.0.1 4061
  2 127.0.0.1 4071

* Compile the program by typing `javac RA_Main.java`

* Set up nodes in `N` different terminals, type

   `java RA_Main <node_number> <number_of_times_to_enter_critical_section>` in each terminal.

* Example
```
java RA_Main 0 2
```
```
java RA_Main 1 2
```
```
java RA_Main 2 2
```

## Result Snapshots

Node 0 is trying to execute 2 times

![RA_Main_0_2.jpeg](https://github.com/FaizalSandanampusi/fai/blob/master/Images/RA_Main_0_2.jpeg?raw=true)



Node 1 executes 2 times

![RA_Main_1_2.jpeg](https://github.com/FaizalSandanampusi/fai/blob/master/Images/RA_Main_1_2.jpeg?raw=true)

Node 2 executes 2 times

![RA_Main_2_2.jpeg](https://github.com/FaizalSandanampusi/fai/blob/master/Images/RA_Main_2_2.jpeg?raw=true)



