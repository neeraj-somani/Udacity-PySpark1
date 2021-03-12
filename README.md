# Udacity-PySpark1

This notebook will cover concepts learned in Udacity pySpark course -- https://classroom.udacity.com/courses/ud2002

Section 2 -
Power of Spark --

1. What is big data?
- When you can't use single machine and requires distributed systems to process your data.
- Mordern Hardware capabilities define 
  - CPU ? - How long does it take your CPU to perform a specific task
     - Brian of computer
     - The CPU can also store small amounts of data inside itself in what are called registers. These registers hold data that the CPU is working with at the moment.
     - The registers make computations more efficient: the registers avoid having to send data unnecessarily back and forth between memory (RAM) and the CPU.
     - 200x times faster than memory
     
  - Memory (RAM) ? - How quickly can you lookup some file that is cache in your systems memory, example "calender that is cached in system"?
      - When your program runs, data gets temporarily stored in memory before getting sent to the CPU. Memory is ephemeral storage - when your computer shuts down, the data in the memory is lost.
      - 15x times faster than SSD
      
  - SSD ? - How many seconds does it take to load data from SSD to app.
      - Cheap but relatively slow compared to cache memory
      - 20x times faster than network
      
  - Network ? - How much data can you download from networks in a min.
      - LAN or Internet - a gateway for other computer tasks
      - Which component is the biggest bottleneck when working with big data?
          - Transfering data across network!
          - Thats why in spark System Design, we use clusters (that conneted by a reliable network), to avoids these network bottleneck issues and even avoid (shuffeling) moving data back and forth between nodes of a cluster. Complete processing of each set of data happend with-in each node of cluster and then merge together before delivering.
          
 
 **That's correct! CPU operations are fastest. Operations in memory (RAM) are the second fastest. Then comes hard disk storage and finally transferring data across a network. Keep these relative speeds in mind. They'll help you understand the constraints when working with big data.**
 
 *Things to understand as well*
 
 - It seems like the right combination of CPU and memory can help you quickly load and process data.
 - Charachtersitics of Memory
    - Efficient
    - Ephemeral (loose data when you turn off)
    - Expensive
 - Beyond the fact that memory is expensive and ephemeral, we'll learn that for most use cases in the industry, memory and CPU aren't the bottleneck. Instead the storage and network.
 
  An interactive version of todays Hardware (https://colin-scott.github.io/personal_website/research/interactive_latency.html)


2. Review of the hardware behind big data
3. Introduction to distributed systems
4. Brief history of Spark and big data
5. Common Spark use cases
6. Other technologies in the big data ecosystem

 
 
