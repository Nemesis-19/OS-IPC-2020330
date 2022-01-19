Using FIFO :

1) fp1.c : This file implements the P1 portion of the question. After declaring the appropriate headers, we first declare an fd. Then we declare the path of our fifo and enque the mkfifo command to create our pipe. (A FIFO special file (a named pipe) is similar to a pipe, except that it is accessed as part of the filesystem. When processes areexchanging data via the FIFO, the kernel passes all data internally without writing it to the filesystem.  Thus, the FIFO special file has no contents on the filesystem; the filesystem entry merely serves as a reference point so that processes can access the pipe using a name in the filesystem.) Next we declare the length of the string, then using write function (openning in write mode), we first write the length of the string decided(this will then be read by the p2 portion). Next there is the code to generate random strings of fixed length(it uses rand function to generate random numbers which are then divided by 26 and used as index to get the number from the alphabet array). Then there are 2 nested loops. The interior loop runs 5 times, signfying the sending of 5 strings at a time, and the outer loop runs 10 times as we have to send 50 strings. Inside the interior loop we use the write command to send the string, then we use write again to send the id(index of the string). Then after exiting the interior loop there is the command to read the max id(using read mode) and print it on the screen. And then after exiting the outer loop the code terminates.

2) fp2.c : This file implements the P2 portion of the question. After declaring the appropriate headers, we first declare an fd1. Then we declare the path of our fifo and enque the mkfifo command to create our pipe. Then we declare an int num1, next we use the read command to read our fifo and get the integer written in it(it is the kengh of the fixed strings passed from P1). Next we declare the 2d array, which stores the 50 incoming string of fixed length. Then there are 2 nested loops. The interior loop runs 5 times, signfying the reading of 5 strings at a time, and the outer loop runs 10 times as we have to read 50 strings. Inside the interior loop we use the read command to read the string and store in the previously made arrays, then we use read again to read the id(index of the string), then we print the recieved data on the screen. Then after exiting the interior loop there is the command to send the max id(calculated using a comparing for loop, and sent using write mode). And then after exiting the outer loop the code terminates.

Using Message Passing Queues :

1) mp1.c : This file implements the P1 portion of the question. A message queue is a linked list of messages stored within the kernel and identified by a message queue identifier. A new queue is created or an existing queue opened by msgget(). New messages are added to the end of a queue by msgsnd(). Every message has a positive long integer type field, a non-negative length, and the actual data bytes (corresponding to the length), all of which are specified to msgsnd() when the message is added to a queue. Messages are fetched from a queue by msgrcv(). After declaring the appropriate headers, under this code we first declare a struct for message buffer which has 3 elements, the array, the type, and the id. Under the main function we declare 2 messages(1 will be used for sending message and 1 will be used for reading). Next we declare the length of the string, then there is the code to generate random strings of fixed length(it uses rand function to generate random numbers which are then divided by 26 and used as index to get the number from the alphabet array). Then there are 2 nested loops. The interior loop runs 5 times, signfying the sending of 5 strings at a time, and the outer loop runs 10 times as we have to send 50 strings. Inside the interior loop we intiate the first message structure, set its key using ftok funciton then use msgget to generate the id. Then we assign values to messages element(array takes string, type takes type, id takes index),  and we finally send the signal using the msgsnd command. Then after exiting the internal loop there is the code reading the max id sent from p2 using the message. Here we use the msgrcv command and to recieve and assign we values to the second message struct. Finally we print the max id recieved. After exiting the external loop the code terminates.

2) mp2.c : This file implements the P2 portion of the question. After declaring the appropriate headers, under this code we first declare a struct for message buffer which has 3 elements, the array, the type, and the id. Under the main function we declare 2 messages(1 will be used for sending message and 1 will be used for reading). Next we declare an integer array to store the ids coming from the messagesfrom p1(to get max id later). Then there are 2 nested loops. The interior loop runs 5 times, signfying the sending of 5 strings at a time, and the outer loop runs 10 times as we have to read 50 strings. Inside the interior loop we intiate the first message structure, set its key using ftok funciton then use msgget to generate the id. Then we use the msgrcv command to recieve the incoming message from p1(carrying the string and the id) and assign it to the first message struct. Next we store the id in the array and print the recieved data on the screen. Then after exiting the internal loop there is the code sending the max id sent from p2 using the message. Here we use the msgsnd command and  and assign the id inside the second message struct to max id and finally send it using msgsnd command to p1. After exiting the external loop the code terminates.

Using Unix Domain Sockets :

1) server.c : This file implements the P1 portion of the question. Socket programming is a way of connecting two nodes on a network to communicate with each other. One socket(node) listens on a particular port at an IP, while other socket reaches out to the other to form a connection. Server forms the listener socket while client reaches out to the server. After declaring the appropriate headers, the next 2 blocks of code are used in intializing and initiating the server socket. sockfd: socket descriptor, an integer (like a file-handle), domain: integer, communication domain e.g., AF_UNIX , pattern used: initialization->setting path family->bind->listen->accept. Then there are 2 nested loops. The interior loop runs 5 times, signfying the sending of 5 strings at a time, and the outer loop runs 10 times as we have to send 50 strings. Next, we declare a char buff array which will be used to store the incoming strings from the client socket. Next we initialize an char id array to store the ids coming fromm the server socket. Then there are 2 nested loops. The interior loop runs 5 times, signfying the sending of 5 strings at a time, and the outer loop runs 10 times as we have to send 50 strings. Inside the internal loop we intiate a pointer to char array, next we allocate sufficient space to 2 char arrays. First array is used for the string and next pointer is used to store the id but after a time gap of 1 second using the sleep(1) command. Next we print the input recieved/max id recieved from the client socket on the screen. After exiting the internal loop, there is the command to send the maximum id sent by the client to back to the client using the input coming from the client socket using the command write(), this id is assinged to a character array and sent. After exiting the external loop the code terminates.

2) client.c : This file implements the P2 portion of the question. After declaring the appropriate headers, under this code we first under this code we first use the code to generate random strings of fixed length(it uses rand function to generate random numbers which are then divided by 26 and used as index to get the number from the alphabet array). Then we intialize and initaite the client socket using the socket command, and after setting the correct address. As we have provided the path that is same as the server, after setting clients path, we connect it to the server using connect command. Iniside the internal loop we first read the strings coming from the ans[][] 2d array and copy it to the socket using the valread command and assign it to a str char array and send it to the server using the write() command, next we again assiggn the id(index of the string) to snum char array and send it again to the server using the the write() command but after a time gap of 1 second using the sleep(1) command. After exiting the internal loop there is the command to read the  max ids coming from the server socket using the read() command and assinging it to the id char array. Then we print the recieved data on the screen. After exiting the outer loop the code terminates.