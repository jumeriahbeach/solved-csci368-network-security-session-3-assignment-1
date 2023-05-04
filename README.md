Download Link: https://assignmentchef.com/product/solved-csci368-network-security-session-3-assignment-1
<br>
<h1>Objectives</h1>

On completion of this assignment you should be able to:

<ul>

 <li>Understand some basic techniques for building a secure channel.</li>

 <li>Perform some basic security analysis for secure communication protocols.</li>

</ul>

<strong><em> </em></strong>

<h1>Programing Task</h1>

Write (Java or C/C++) UDP programs allowing two parties to mutually authenticate each other and establish a secure communication channel. For simplicity, let us call the programs “Host” and “Client”, which are executed by Alice and Bob, respectively.

Alice and Bob share a common password PW, which contains 6 alphanumeric characters. Alice also has a public and privacy key pair (pk, sk) for the RSA encryption scheme. They want to establish a secure communication channel that can provide data confidentiality and integrity. This will be done via the following steps: (1) perform a mutual authentication and key exchange protocol; and (2) use the shared session key derived from the first step to secure the real communication.

<strong>Step 1</strong> is done via the following mutual authentication and key exchange protocol:

1: B → A: NB

2:  A → B: pk, NA

3:  B → A: C1 = PKE<sub> pk</sub>(K), C2 = SKE<sub>K</sub>(Username||PW)

Alice decrypts C1 using sk to get K, and then decrypts C2 to get Username and PW. Alice checks Username and PW and accepts the connection if and only if they are correct. Alice sends either “Successful” or “Failed” to Bob to indicate whether the connection is successful or not.

4: A → B: Authentication Successful/Failed

In the above protocol, NB and NA denote 128-bit nonces chosen by Bob and Alice, respectively; PKE denotes the RSA encryption; SKE denotes the RC4 stream cipher and || denotes string concatenation. K is a random string selected from the message space of the PKE. Alice and Bob then compute the shared session key as ssk = H(K||NB||NA) where H denotes the SHA-1 hash algorithm.

After establishing the session key, <strong>step 2</strong> is achieved as follows:

<ol>

 <li>whenever Alice wants to send a message m to Bob, Alice first computes an integrity check value h = H(ssk||m||ssk), and then computes C = SKE<sub>ssk</sub>(m||h) and sends C to Bob;</li>

 <li>upon receiving a ciphertext C, Bob first runs the decryption algorithm to obtain m||h. After that, Bob computes h’ = H(ssk||m||ssk) and checks if h = h’. If the equation holds, then Bob accepts m; otherwise, Bob rejects the ciphertext;</li>

 <li>the same operations are performed when Bob sends a message to Alice.</li>

</ol>

<strong>Implementation guidelines </strong>

<ul>

 <li>Place Host and Client in two separate directories: Alice and Bob. Alice also stores a password file in her directory. The password file contains all the user records, e.g., (Bob, PW).</li>

 <li>Generate a public and private key pair for Alice, and store the generated public and private key pair in a key file under Alice’s directory. The key generation can be done using a separate program.</li>

 <li>Alice executes Host.

  <ul>

   <li>Host is running and listening to the opened port (you need to select a port for your code).</li>

  </ul></li>

 <li>Bob executes Client.

  <ul>

   <li>Client asks for input (username and PW) from Bob via keyboard.</li>

   <li>Client sends the first message (i.e., NB) to Host.</li>

  </ul></li>

 <li>Alice and Bob perform the authentication and key exchange protocol as outlined above.</li>

 <li>If Alice cannot successfully authenticate Bob, then Alice quits the program after sending “Authentication Failed” to Bob. Bob also quits the program after receiving the message from Alice.</li>

 <li>If the connection is successfully established,

  <ul>

   <li>Either Alice or Bob can send a message encrypted and authenticated by the session key ssk. They type the message on their own terminal. The message is processed by their code according to step 2 given above.</li>

   <li>The received message is printed on the screen if decryption is successful. Otherwise, print “Decryption Error” on the screen.</li>

   <li>To quit the programs, Bob should type “exit”.</li>

  </ul></li>

</ul>

<strong>You can choose to use existing library functions or open source code to implement UDP sockets, RSA, RC4 and SHA-1. You should provide a reference if you use any downloaded code.  </strong>

<strong>How to run?</strong>

Your programs should run according to the protocol. Host and Client should be executed on different windows. For convenience of marking, please use the local IP: 127.0.0.1 for the submitted version. For simplicity, there is no GUI required in this assignment. That is, messages are simply typed on the window and printed on the receiver’s window.

Mark distribution:

<ol>

 <li>RSA key generation and storage: 2 marks</li>

 <li>Key Establishment (Step 1): 8 marks</li>

 <li>Data Encryption/Decryption (Step 2): 8 marks</li>

 <li>Proper and clear message display: 2 marks</li>

</ol>

<strong>Note: code that cannot be compiled or executed will receive a zero mark. </strong>







<strong>Files to be submitted:</strong>

All source codes (Do not submit any executable).

A readme file (text/ACSII only): instructions about how to compile and run your code.





