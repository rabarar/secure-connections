# secure-connections
Simple client and server for showing what's happening with certificates during TLS setup, as used at GopherCon 2018 and Velocity New York. 

* [Slide deck](https://speakerdeck.com/lizrice/a-go-programmers-guide-to-secure-connections)
* GopherCon video: [A Go Programmer's Guide to Secure Connections](https://youtu.be/kxKLYDLzuHA)


## ADDENDUM:

Not so simple, in order for this to work (at least on OSX Catalina go version go1.13.4 darwin/amd64) the following things must be done:

1. On the server, the server cert MUST BE THE The CHAIN, starting with the server cert and going all the way to the root CA Cert in one pem file.

2. The Certificate must be installed in the Apple keychain and marked as Trusted

3. Instead of using NewCertPool(), need to use SystemCertPool()


## More on adding the cert to the Keychain

There are two ways of adding the cert to the keychain

	- create a pkcs12 cert/key pair and add it 
	- install the CA.pem cert without the key

Regardless of how you wish to add the key, the key must be main to be trusted. The default trust status is Not Trusted.



## Notes on hostnames in the server Listen and Client Dial

Make sure to pay attention to the hostname in both the server Listen and the Client Dial
