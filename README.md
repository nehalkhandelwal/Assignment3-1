# Assignment3
GITHUB Practice

SETTING UP SSL IN TOMCAT (HTTPS CONFIGURATION)
=====================

###To Create Certificate for SSL:-

1) Open Terminal and Type commmand : "cd JAVA_HOME" 

2) Type commmand _"keytool -genkey -alias clypper -keyalg RSA"_

3) When you type above command you will be asked some questions. Answer them to create 
```
[user]:bin [user] keytool -genkey -alias clypper -keyalg RSA
Enter keystore password:  [password]
Re-enter new password: [password]
What is your first and last name?
  [Unknown]: [Name]
What is the name of your organizational unit?
  [Unknown]: [organizational unit]
What is the name of your organization?
  [Unknown]:  [organization]
What is the name of your City or Locality?
  [Unknown]:  [City]
What is the name of your State or Province?
  [Unknown]:  [State]
What is the two-letter country code for this unit?
  [Unknown]:  [country code]
Is CN=[Name], OU=[organizational unit], O=[organization], L=[City], ST=[State], C=[country code] correct?
  [no]:  yes
 
Enter key password for
    (RETURN if same as keystore password):  [password]
Re-enter new password: [password]
```

4) Now, _".keystore"_ is created in root directory for user e.g _"Users/[user]/.keystore"_

###Configuration for Tomcat:-

1) Open Tomcat directory and open _"server.xml"_ from _"conf"_ e.g _"apache-tomcat-7.0.55/conf/server.xml"_

2) Find the below commented line from _"server.xml"_ and replace with given code in 3rd step
```
<!--
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
    maxThreads="150" scheme="https" secure="true"
    clientAuth="false" sslProtocol="TLS" />
-->
```

3) Change the code with this
```
<Connector SSLEnabled="true" acceptCount="100" clientAuth="false"
     disableUploadTimeout="true" enableLookups="false" maxThreads="25"
     port="8443" keystoreFile="/Users/[user]/.keystore" keystorePass="password"
     protocol="org.apache.coyote.http11.Http11NioProtocol" scheme="https"
     secure="true" sslProtocol="TLS" />
```
4) Make sure to change the location of _"keystoreFile"_ as per your location and set your password in _"keystorePass"_
