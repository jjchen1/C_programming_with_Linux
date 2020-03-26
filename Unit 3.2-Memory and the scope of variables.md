

# 1 Understanding computer memory

## 1.1 Discover the Von Neumann architecture

### 1.1.1 Princeton architecture
John von Neumann was part of a group of people who created a model that describes the insides of a computer. He was a physicist and mathematician born in 1903 in Budapest, Hungary. The von Neumann architecture, used in all modern computers,
is named after him. There still exists a controversy around the naming of this architecture,
however. John William Mauchly and John Eckert used this concept already in their work
on the big ENIAC computer.

To give a good tribute to everyone, we speak about the **Princeton architecture**.

![image-20200326131507444](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326131507444.png)

1. arithmetic logic unit (ALU)
Its role is to perform basic operations, such as plus, minus, times, division, as well as logical operations, such as and, or, and not.

2. control unit
It coordinates the operation and sequence of data movements between the other parts of the architecture.

**CPU = arithmetic logic unit + control unit**

3. memory
It serves both data and programs.
Memory comes in two flavors, temporary memory, also called **RAM**, short for random access memory, and lasting memory, such as hard drives.
4. input and output
This enables communication between the computer and the external world, such as the user, peripherals, and even other computers.

Most computers conceived of between the 1940s and the early 1970s were designed according to this model.

### 1.1.2 New ideas
As computers started evolving more rapidly in the 1970s, new ideas emerged.

For example, computer memory can now communicate directly with input and output, bypassing the CPU entirely.

![image-20200326132314526](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326132314526.png)

But let's keep it simple for now.

The architecture we just described provides a good if somewhat simplified overview of what are still the main concepts in modern computer information technology.



## 1.2 Memory representation, RAM, cells, word, byte, bit, memory address

## 1.2.1 two different types of memory

1. RAM (short for Random Access Memory)

It is temporary memorythat is easy and quick to access and, for example, used to execute programs.

We also call this type of storage volatile memory.

![image-20200326140325032](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326140325032.png)



2. nonvolatile, or lasting memory

It is for more permanent storage of data, for example, used to store files on the hard drive.

![image-20200326140335656](/Users/chenjiajia/Library/Application Support/typora-user-images/image-20200326140335656.png)