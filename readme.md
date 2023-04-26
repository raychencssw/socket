# Description:  
This project consist of 3 parts, client, main server, and the two backend servers.
1.client.cpp: the user interface that accepts inputs and use them to send request to serverM, presents the corresponding time interval result. 
Please notice that the client will always get response from serverM no matter there exist available time interval or not. The client will receive 
a 'F' and it'll know no valid result within these user names and it'll print out corresponding message.  

2.serverM.cpp(main server): the central server that manages every thing. Send the response to the client accordingly. Please notice that serverM exchange message
with backend servers with char[], and to expedit the search algorithm, the message will be passed into a function stoVector() to change to vector. 
The result will then be changed back to char[] by function vectortoChar(). The search algorithm I write here is to compare two users at a time. 
ServerM also holds an unordered_map<string, string> to store key=user name and value=server for fast lookup. It is used to tell in which backend 
server are the received user names located.  

3.serverA.cpp & serverB.cp(backend server)p: the backend server that store user information. Holds an unordered_map<string, string> to store key=user name 
and value=available time for fast lookup. The algorithm and transformation between char[] and vector is the same as severM.  


# Process Flow  
1.The main server and the two backend servers boot-up first. After the backend server read the input file that contains the user name and available time, 
both of them will send  a list of user names to the main sever. Then the main server will maintain a lookup table indicating which user name is on
which backend server. Hence, the sensitive user data is keeping at backend server only.  
  
2.Client boots up after the main server and the backend servers finshed booting up. Then user can input user names and then the user names will be passed 
to the main server.   
  
3.Main server will decide which user name should be forwarded to which backend server. If there is invalid user name, the main server will send a message 
back to the client to let user know.  
  
4.When receving user name from the main server, both backend servers will execute searching algorithm to find the available time that works for every user
whose information is stored on this backend server.  
  
5.When the main server recived feedback from backend servers, it will execute same algorithm again to find available that works for both group of users on 
both backend servers and send the information back to the user. 

6.The user will then get the feedback and have the information either there exist available time works for everyone or not.  
