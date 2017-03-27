# IPC_file_system

 1，一个简单的两个进程通过写入文件系统信息来通信。
 
 UNIX中进程间的通信的一种方式：即穿过内核，通过文件系统来传信息。
 
 2，通过 pipe来通信，两个进程通过 两个管道（因为一个管道是单向的，需要两个，来达到双向的沟通）。
     父进程通过管道1传递文件名给子进程，子进程读出文件名，打开文件，把文件内容通过管道2发送给父进程。
     父进程打印出文件内容。
     
 3, 在有些系统里面，pipe是全双共的，但是你不能指望它，如果想要全双共的，建议用sockepair。
    全双工：即在一个管道里面，一个描述符既可以读也可写，且他们不会冲突，例如，进程0通过fd0写入数据，然后通过fd0读出数据 ，这时候是不会读出自己写入的数据的，只会读出从fd1写入的数据。
    同理，fd1也只会读出从fd0写入的数据。
    简单来说就是：fd0/fd1 既可以读出也可写入数据，但是从fd0/fd1读出的数据一定是从fd1/fd0 写入的。
    
    socketpair可以达到这个要求（在有些系统的pipe中可以，有些不可).

 4，简单的用tcp socket来传递文件（client发送文件名给server，server打开后，传给client），功能和2一样，只是在不同主机
 上面的通信。 （server_send.c client_recv.c)