Download Link: https://assignmentchef.com/product/solved-networkprogramming-homework-1
<br>
In this homework, you are required to write two programs, a client and a server, to build a chat room system. The clients talk to one another through the server. The server accepts connections from the clients and processes the command from the clients.

<strong>Hint:</strong>It is suggested that you use <strong>select()</strong> for constructing the client and the server programs.

<h2>Specification</h2>

<h3>Server</h3>

<ul>

 <li>The command to start the server./server &lt;SERVER PORT&gt;</li>

</ul>

If the number of arguments is not one, the server program should terminates.The server can serve multiple clients simultaneously. Once a connection is established, the server will send a hello message to the client and give the client a username anonymous. The client can send different commands to the server. The messages transmitted between clients and the server are shown below.

<h4>Hello Message</h4>

When a client connects to the server, the server will send a hello message to the client and then broadcasts this user’s presence to other clients.

<ul>

 <li>Client output format

  <ul>

   <li>To the newly connected client[Server] Hello, anonymous! From: &lt;Client IP&gt;:&lt;Client Port&gt;</li>

   <li>To existing clients[Server] Someone is coming!</li>

  </ul></li>

</ul>

<h4>Offline Message</h4>

When a client disconnect from the server, the server will send an offline message to all the other online clients to tell them someone has been offline.

<ul>

 <li>Client output format[Server] &lt;USERNAME&gt; is offline.</li>

</ul>

<h4>Who Message</h4>

A client can type command below to list all online users.

<ul>

 <li>Client input formatwho</li>

</ul>

The server will reply to sender a list of online users and tag the sender client. For N user, Server will send N lines. Each of them shows details of a user.

<ul>

 <li>Client output format

  <ul>

   <li>If the user is not the client itself[Server] &lt;USERNAME&gt; &lt;CLIENT IP&gt;:&lt;CLIENT PORT&gt;</li>

   <li>If the user is the client itself[Server] &lt;SENDER USERNAME&gt; &lt;CLIENT IP&gt;:&lt;CLIENT PORT&gt; -&gt;me</li>

  </ul></li>

</ul>

<h4>Change Username Message</h4>

A client can type the command below to change his/her username.

<ul>

 <li>Client input formatname &lt;NEW USERNAME&gt;</li>

</ul>

The server has to verify if the new name is valid which means the input name is

<ol>

 <li>not anonymous,</li>

 <li>unique, and</li>

 <li><strong>2~12</strong> English letters.</li>

</ol>

It will reject user’s request if this name cannot fit the rule.

<ul>

 <li>Client output format</li>

</ul>

<ul>

 <li>If the new name is anonymous.[Server] ERROR: Username cannot be anonymous.</li>

 <li>If the new name is not unique.[Server] ERROR: &lt;NEW USERNAME&gt; has been used by others.</li>

 <li>If the new name does not consist of <strong>2~12</strong> English letters.[Server] ERROR: Username can only consists of 2~12 English letters.</li>

</ul>

The server will reply some messages to all users once a user changes his/her name.

<ul>

 <li>Client output format

  <ul>

   <li>To user which changed his/her name[Server] You’re now known as &lt;NEW USERNAME&gt;.</li>

   <li>To other users[Server] &lt;OLD USERNAME&gt; is now known as &lt;NEW USERNAME&gt;.</li>

  </ul></li>

</ul>

<strong>Note:</strong>A user can be rename as itself, that is, when <strong>userA</strong> wants to rename as <strong>userA</strong>, server should not return error messages.

<h4>Private Message</h4>

A client can send a private message to a specific client.

<ul>

 <li>Client input formattell &lt;USERNAME&gt; &lt;MESSAGE&gt;</li>

</ul>

The server will send an error message back to the sender if either the sender’s name or the receiver’s name is anonymous.

<ul>

 <li>Client output format</li>

</ul>

<ul>

 <li>If the sender’s name is anonymous[Server] ERROR: You are anonymous.</li>

 <li>If the receiver’s name is anonymous[Server] ERROR: The client to which you sent is anonymous.</li>

 <li>If the receiver doesn’t exist[Server] ERROR: The receiver doesn’t exist.</li>

</ul>

Otherwise, the server sends the private message to the specific client and sends back a notification to the sender.

<ul>

 <li>Client output format</li>

</ul>

<ul>

 <li>To the sender: If the message is sent[Server] SUCCESS: Your message has been sent.</li>

 <li>To the receiver: If both client’s name are not anonymous[Server] &lt;SENDER USERNAME&gt; tell you &lt;MESSAGE&gt;</li>

</ul>

<h4>Broadcast Message</h4>

A client can send a broadcast message to all clients.

<ul>

 <li>Client input formatyell &lt;MESSAGE&gt;</li>

</ul>

While receiving the command from a user, the server will add &lt;SENDER’s USERNAME&gt; at the head of it and broadcasts to all users including the sender.

<ul>

 <li>Client output format[Server] &lt;SENDER’s USERNAME&gt; yell &lt;MESSAGE&gt;</li>

</ul>

<h4>Error Command</h4>

Commands which haven’t been declared above are invalid commands. When a server receives an invalid command, it should send an error message back to the sending client.

<ul>

 <li>Client output format[Server] ERROR: Error command.</li>

</ul>

<h3>Client</h3>

A client cannot connect to more than one server at the same time.Users should give the server IP and the port as the arguments of the client program.If the number of arguments is not two, the client program should terminates.

<ul>

 <li>The command to start the client./client &lt;SERVER IP&gt; &lt;SERVER PORT&gt;</li>

</ul>

<h4>Exit Command</h4>

The user can type the command below to terminate the process at any time.

<ul>

 <li>Command Formatexit</li>

</ul>

<strong>Note:</strong>This command should be process by the client locally. That is, the client should close the connection and terminate the process while it receives the <strong>exit</strong> command.

<h4>Receive &amp; Display Format</h4>

The clients keep receiving commands from stdin and, except for “exit” command, send those to the server directly without any modification.

<strong>Note:</strong>For messages received from stdin, client can only process the exit command, others should be sent to the server without modification. All commands received from stdin (except exit command) should be sent to server directly.