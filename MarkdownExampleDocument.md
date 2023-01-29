# Test

1.  Note1
2. lksdfjlsj
3. sdfasdf 


**bold text**

> **bold text**dssdfa  
> **bold text**dssdfa  

``` json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```



# [TCPCopy](https://github.com/session-replay-tools/tcpcopy) - A TCP Stream Replay Tool

TCPCopy is a TCP stream replay tool to support real testing of Internet server applications. 


## Description
Although the real live flow is important for the test of Internet server applications, it is hard to simulate it as online environments are too complex. To support more realistic testing of Internet server applications, we develop a live flow reproduction tool - TCPCopy, which could generate the test workload that is similar to the production workload. Currently, TCPCopy has been widely used by companies in China.   

TCPCopy has little influence on the production system except occupying additional CPU, memory and bandwidth. Moreover, the reproduced workload is similar to the production workload in request diversity, network latency and resource occupation.


## Scenarios
* Distributed stress testing
  - Use tcpcopy to copy real-world data to stress test your server software. Bugs that only can be produced in high-stress situations can be found
* Live testing
  - Prove the new system is stable and find bugs that only occur in the real world
* Regression testing
* Performance comparison


## Architecture 

![tcpcopy](https://raw.github.com/wangbin579/auxiliary/master/images/tcpcopy.GIF)

As shown in Figure 1, TCPCopy consists of two parts:  *tcpcopy* and *intercept*. While *tcpcopy* runs on the online server and captures the online requests, *intercept* runs on the assistant server and does some assistant work, such as passing response info to *tcpcopy*. It should be noted that the test application runs on the target server. 

*tcpcopy* utilizes raw socket input technique by default to capture the online packets at the network layer and does the necessary processing (including TCP interaction simulation, network latency control, and common upper-layer interaction simulation), and uses raw socket output technique by default to send packets to the target server (shown by pink arrows in the figure).

The only operation needed on the target server for TCPCopy is setting appropriate route commands to route response packets (shown by green arrows in the figure) to the assistant server. 

*intercept* is responsible for passing the response header(by default) to *tcpcopy*. By capturing the response packets, *intercept* will extract response header information and send the response header to *tcpcopy* using a special channel(shown by purple arrows in the figure). When *tcpcopy* receives the response header, it utilizes the header information to modify the attributes of online packets and continues to send another packet. It should be noticed that the responses from the target server are routed to the assistant server which should act as a black hole.


## Quick start

Two quick start options are available for *intercept*:

* [Download the latest intercept release](https://github.com/session-replay-tools/intercept/releases).
* Clone the repo: `git clone git://github.com/session-replay-tools/intercept.git`.

Two quick start options are available for *tcpcopy*:

* [Download the latest tcpcopy release](https://github.com/session-replay-tools/tcpcopy/releases).
* Clone the repo: `git clone git://github.com/session-replay-tools/tcpcopy.git`.


## Getting intercept installed on the assistant server
1. cd intercept
2. ./configure 
   - choose appropriate configure options if needed
3. make
4. make install


### Configure Options for intercept
    --single            run intercept at non-distributed mode
    --with-pfring=PATH  set path to PF_RING library sources
    --with-debug        compile intercept with debug support (saved in a log file)