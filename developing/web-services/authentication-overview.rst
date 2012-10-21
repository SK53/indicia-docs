Authentication Overview
=======================

When a client website makes a read or write request to the warehouse's web 
services, it is necessary to authenticate the request. In an ideal world a 
secure connection would be used so that the password can be passed between the 
client and server to authenticate. Secure communications over the internet are
normally dependent on using a secure socket layer (SSL) - this is the technology
in use when you visit online payment sites with the website's protocol set to
*https*. This type of connection requires additional configuration on the server
so, in Indicia, we cannot rely on it being an option. Therefore we had to design
the web services so that they are secure even across an insecure connection.

Therefore, Indicia uses digest authentication which is a protocol for 
authentication that does not require the password to be sent from the client to 
the server. This involves the following steps.

#. The client requests a public token from the server, known as a nonce.
#. The server generates the public token and returns it to the client.
#. The client combines the public token with the password and then hashes this 
   combined token using a non-reversible algorithm.
#. The client sends this hashed token with the public token when performing the
   web-services request which is to be kept secure.
#. The server receives the request and combines the public token with the 
   expected password, then hashes it using the same algorithm as the client.
#. This hashed token is compared with the one sent from the client to determine
   if the client has sent the correct token and therefore knows the password. 
   Note that at no point does the password get sent across the connection so this
   approach is safe for insecure connections to web services.