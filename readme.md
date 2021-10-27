Note:- here your_desired_domain.ext is my desired domain.

note another:-
--------------------------------
we will repalce or add the doamin in 3 files
C:\Windows\System32\drivers\etc\hosts
C:\xampp\apache\conf\extra\httpd-vhosts.conf
C:\xampp\apache\crt\cert.conf

and run 1 file 
C:\xampp\apache\crt\make-cert.bat

1- create a folder in with name "crt" in C:\xampp\apache folder and place the make-cert.bat and cert.conf file in C:\xampp\apache\crt
2- now for setup the vertual host(your_desired_domain.ext) put the given content in C:\xampp\apache\conf\extra\httpd-vhosts.conf

```
 <VirtualHost *:80>
     DocumentRoot "C:/xampp/htdocs"
     ServerName your_desired_domain.ext
     ServerAlias *.your_desired_domain.ext
	 
	<Directory "C:/xampp/htdocs">
        Require all granted
	AllowOverride All
    </Directory>
	ErrorLog "logs/your_desired_domain.ext-error.log"
    CustomLog "logs/your_desired_domain.ext-access.log" combined
	
    RewriteEngine on
    RewriteCond %{SERVER_NAME} =www.your_desired_domain.ext [OR]
    RewriteCond %{SERVER_NAME} =your_desired_domain.ext
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
 </VirtualHost>
 <VirtualHost *:443>
     DocumentRoot "C:/xampp/htdocs"
     ServerName your_desired_domain.ext
     ServerAlias *.your_desired_domain.ext
	 <Directory "C:/xampp/htdocs">
        Require all granted
		AllowOverride All
     </Directory>
	
    ErrorLog "logs/your_desired_domain.ext-error.log"
    CustomLog "logs/your_desired_domain.ext-access.log" combined
     SSLEngine on
     SSLCertificateFile "crt/your_desired_domain.ext/server.crt"
     SSLCertificateKeyFile "crt/your_desired_domain.ext/server.key"
 </VirtualHost>
```

3- point the ip on yourdomain in C:\Windows\System32\drivers\etc\hosts file
```
127.0.0.1 your_desired_domain.ext
```

4- replace the your_desired_domain.ext with your desired domain in cert.conf


5- double click on make-cert.bat
now Enter Domain: your_desired_domain.ext
then just press the enter key till Common Name
now enter the value of 
```
Common Name (e.g. server FQDN or Your name) [your_desired_domain.ext]:your_desired_domain.ext
```
then just press the enter key to finish

6- double click the server.crt and Install Certificate -> Local Machine -> Place all certificates in the following store -> Browse -> Trusted Root Certification Authorities -> Ok -> Next -> Finish

7- restart the xampp and test

now your_desired_domain.ext have ssl binding
