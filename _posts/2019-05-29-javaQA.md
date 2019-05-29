#jAVA_Interview
##1 what difference between JDK and JRE?
  jdk> jre 
  jdk includes java runtime Envionment (JRE), an interpreter/loader (Java) ,a compiler(javac), an archiver(jar),
  a docunmentation generator(javaDoc) and other tools needed in java development.
  jre stands for java runtime environment , the java runtime environment provides the minimum requirements for executing a java application
  it consists of the java virtual machine(JVM) ,core classes ,and supporting files.
  
## 2 what difference between == and equals 
  == checks if both objects point to the same memory location whereas .equals evaluates to the comparison of values in the objects.
  
##3 hashcode the same equals? 
 so it is not necessary that two different object will have same hash code are equal. hashcode() returns a unieque integer id for each object
 ...on the other hand ,if the hash code is the same ,then you must execute the equals() method to datermine whether the values and fields 
 are the same.
 
## 4 what is effect of final in java ? 
 final keyword is used in different contexts,first of all, final is a non-access-modifier applicable only to a variable .a method or a class .
 Final variable  to create constant variables;
 Final Method    prevent Method Overringing;
 Final Classes   prevent Inheritance;
 
##5 java Math.round() method  
   the method is a built-in math function which returns the cloeest long to the agrument.
## 6 java String 
   String is a sequence of characters in java  objects of string are immuntable which means a constant and cannot be changed once created.
   
##7 waht difference betwwen StringBuffer StringBuilder  
  as a result,StringBUilder is faster than StringBUffer .StringBuffer is mutable.it can change in terms of length and content .
  StringBuffers are   thread-safe ,meaning that they have synchroized methods to control access so that only one thread can access  a StringBuffer objects synchronized code at a time.
  
## 8 what is difference between String str="i"  and String str=new String("i") 
 Both expression gives you String object, but there is subtle difference between them. When you create String object using new() operator, it always create a new object in heap memory. ... Otherwise it will create a new string object and put in string pool for future re-use.
 
## 9 how to reverse String  
 
## 10 String usually methods  
 
##11 Abstract must have abstract methods ? 
 no
## 12 what is difference between ordinary class and abtract class? 
 Image result for abstract class and method in javawww.youtube.com
Abstract classes cannot be instantiated, but they can be subclassed. In other words, a class that is declared with abstract keyword, is known as abstract class in java. It can have abstract(method without body) and non-abstract methods (method with body).
## 13 abstract classs can be  final 
 A method can never, ever, ever be marked as both abstract and final, or both abstract and private. Think about it—abstract methods must be implemented (which essentially means overridden by a subclass) whereas final and private methods cannot ever be overridden by a subclass.

##14 what is difference between abstract class and interface  
 Main difference is methods of a Java interface are implicitly abstract and cannot have implementations. A Java abstract class can have instance methods that implements a default behavior. Variables declared in a Java interface is by default final. An abstract class may contain non-final variables.
 
## 15 how many io in java ? 
 
## 16 what is difference between NIO AIO BIO ? 
 BIO, The synchronous blocking IO, simple to understand: a connection to a thread
NIO, Synchronous non blocking IO, simple to understand: a request a thread
AIO, Asynchronous non blocking IO, simple to understand: a valid request a thread
BIO
Before JDK1.4, written by Java network request, is the establishment of a ServerSocket, then, the client establishes Socket will ask if there are threads can process, if not, either wait for, or rejected. Namely: a connection request, Server corresponds to a processing thread.

NIO
Origin in Java, in the JDK1.4 and later provides a set of API to operate non blocking I/O, we can find the related classes and interfaces in the java.nio package and its subpackages. Because of this API is JDK new I/O API, therefore, also called New I/O, which is the origin of the package name NiO. The API consists of three main parts: buffer (Buffers), channel (Channels) formed the core class and non blocking I/O. The need to distinguish between when, understanding of NIO, say New I/O or non blocking IO, New I/O is the Java package, NIO is a non blocking IO concept. Here is a back.

The NIO itself is based on the idea of event driven to complete, mainly to solve the complicated problem of BIO is: in the network application using I/O, if you want to handle multiple client requests, or on the client to communicate with multiple servers, you must use multiple threads to process. That is to say, every client request is assigned to a thread separate processing. Although it can meet our requirements, but also bring another problem. Because each create a thread, will be allocated a certain amount of memory space for the thread (also called working memory), and the operating system itself but also on the total number of threads that have certain limitations. If the client requests the server program too much, may be because of heavy and refused the request of the client, and the server may therefore paralysis.

NIO based on the Reactor, when the socket flow readable or writable socket, operating system will be the corresponding notification reference procedure, application of the current read into the buffer or write operating system. 
That is to say, this time, is not a connection to a corresponding processing threads, but a valid request, corresponding to a thread, when the connection is used when there is no data, there is no a worker thread to handle.

AIO
Unlike NIO, when the read and write operation, can only directly call API read or write method. These two methods are asynchronous, for a read operation, when the stream can be read, the operating system will spread into the read buffer method and readable, and notify the application; for a write operation, when the operating system will write transmission stream to write is completed, the operating system to inform application program. 
That can be understood as, read/write methods are asynchronous, after completion will take the initiative to call the callback function. 
In JDK1.7, this part is called NIO.2, mainly in the java.nio.channels package adds the following four asynchronous channels:

AsynchronousSocketChannel
AsynchronousServerSocketChannel
AsynchronousFileChannel
AsynchronousDatagramChannel
The read/write method among them, will return with a callback object, when the execution of the read / write operation, direct calls the callback function.

The realization principle
Said the realization of the principle, but also from the IO model on an understanding of the operating system

In accordance with the "division" Unix network programming, IO model can be divided into: blocking IO, non blocking IO, IO multiplexing, signal driving IO and asynchronous IO, in accordance with the POSIX standard to divided only into two categories: synchronous and asynchronous IO IO. How to distinguish? First of all a IO operation is divided into two steps: IO request and IO operations, The difference between synchronous and asynchronous IO IO lies in the second steps is blocking, If the actual IO read and write blocking request process, So is the synchronization of IO, Therefore, blocking IO, non blocking IO, IO multiplexing, signal driving IO are synchronous IO, If no obstruction, But the operating system to help you finish the IO operation and return the results to you, It is the asynchronous IO. The difference between IO and non blocking IO lies in the first step, IO request will be blocked, if block until complete blocking IO it is traditional, if not blocked, it is non blocking IO.

Received IO model operating system, also have to mention select/poll/epoll/iocp, about the four understanding, not do more to explain, you still do not understand the place.

Can understand the explanation is: in Linux 2.6, Java NIO, is achieved through the epoll, this can be found by JDK source code. AIO, on the windows is realized by IOCP, in the Linux or epoll to achieve through.

Here to emphasize one point: AIO, this is I/O processing mode, and epoll is a realization of AIO programming model; in other words, AIO is an interface standard, the operating system can be achieved or not achieved. In different operating system in the high complicated circumstances are the best recommended operating system. No Linux to achieve real network AIO.

The underlying basis
When it comes to the bottom, say Linux system programming, here do not familiar with, to be later added. 
Only the general said a: AIO

In windows, the AIO is achieved through IOCP, see the JDK source code, can be found

WindowsAsynchronousSocketChannelImpl

Realization of interface:

implements Iocp.OverlappedChannel

Look at the implementation method: read0/write0 method is the native method, call the JVM implementation, the virtual machine technology is not familiar with, don't you.

In Linux, the AIO is achieved through epoll, see the JDK source code, can be found, the source code is:

UnixAsynchronousSocketChannelImpl

Realization of interface:

implements Port.PollableChannel

This is the difference between a and windows maximum, poll, in linux2.6, use the default epoll.

So you can understand.

Written in the last: Java development based, for the operating system underlying cognitive is not C based language is good, language determines the mode of thinking, the ancients did not cheat me

Finally, several papers explain the good article:

BIO NIO AIO
## 17 what method be use in java Files  
 
