# Private CA Template

Getting an SSL certificate these days has become much easier than it was in the past, with the availability of free Certificate Authorities (CAs) like Let's Encrypt. But even so, there are scenarios when you need a certificate that couldn't be issued by them: longer term certificates, complex wildcards, local addresses within your environment, and even routers that are accessed by IP instead of a dns name. Some of these could be issued by a paid CA, others aren't even an option. Code signing certificates are also great, but not cheap, while encryption and authentication certs are generally only issued in enterprise environments.

Getting a self-signed certificate is pretty easy - most routers will generate their own certificates, and it's pretty straightforward to create your own certificate using openssl or similar tools. The problem with self-signed certificates is that they won't be trusted by default. You still get the benefit of your connection being encrypted, but there won't be a guarantee that nobody intercepted your data, altered it and signed it with their own untrusted cert, unless you check the certificate every time. You could always add your certificate to your local trust store, but you'd have to do that for every single certificate you create, on every device you access them, which will quickly become cumbersome.

The solution is simple - you can create your own private CA and add it to your trust store. Any certificates created by that CA would be trusted as well, which makes managing this considerably easier! You wouldn't use these certs on your public website, but they'd be perfect for internal services or your home lab.

Taking one step further, you could also create intermediary CAs, creating a trust chain - the end device certificates would be created by your intermediary CA. If your intermediary CA keys get compromised, you could just revoke them and create a new intermediary, and won't need to update the trust store on your machines.

In these articles I'll put down what I learned while creating my own CA. I've decided to break this down into several parts, to make it easier to digest and manage:

* Part 1: [Building your own root and intermediate certificate authorities](https://www.flexlabs.org/2019/07/private-ca-1-building-root-and-intermediate-ca)
* Part 2: [Issuing certificates](https://www.flexlabs.org/2019/07/private-ca-2-issuing-certificates)
* Part 3: Storage and security
* Part 4: Additional options and features
