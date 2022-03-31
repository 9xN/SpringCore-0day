# SpringCore-0day

A Chinese security researcher user shared, and then deleted the information that by sending crafted requests to JDK9+ SpringBeans-using applications, *under certain circumstances*, that they can remotely:

* Modify the logging parameters of that application to achieve an arbitrary write.
* Use the modified logger to write a valid JSP file that contains a webshell.
* Use the webshell for remote execution tomfoolery.

Praetorian and others (ex. [@testanull](https://twitter.com/testanull/status/1509185015187345411)) publicly confirmed that they have replicated the issue, and several hours later, demo applications (linked below) were released so others could easily verify on their own and learn about this vulnerability. This is being described as a bypass for CVE-2010-1622 - and it is currently *unpatched*. Please read over Praetorian's guidance [here](https://www.praetorian.com/blog/spring-core-jdk9-rce/) which includes detailed identification and mitigation steps.

## Resources

Go check out vx-underground's archive here: https://share.vx-underground.org/SpringCore0day.7z

## PoC / Testing the exploit

The following non-malicious request can be used to test susceptibility to the SpringCore 0day RCE. An HTTP 400 return code indicates vulnerability.

`$ curl host:port/path?class.module.classLoader.URLs%5B0%5D=0`

A few sample applications have been made so you can validate the PoC works, as well as learn more about what cases are exploitable. Tthe **simplest** example of this I can find is courtesy of @freeqaz of LunaSec, who developed [github.com/lunasec-io/spring-rce-vulnerable-app](https://github.com/lunasec-io/spring-rce-vulnerable-app/blob/main/src/main/java/fr/christophetd/log4shell/vulnerableapp/MainController.java).

Additional demonstration apps are available with slightly different conditions where this vulnerability would be exploitable:

* https://github.com/Retrospected/spring-rce-poc


## Note: I will be uploading translations and further explanation of the exploit shortly, feel free to create a pull request!
