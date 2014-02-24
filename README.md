nginx-ssl
=========

a nginx load balancer that strips the SSL off a web request and forwards it internally to a web cluster

This application serves up two different web sites on ports 8080 and 8081, both of which can be reached over http. If port 443 is hit, then the request is forwarded to the port 8081. 

## 1. Setup

Install xginx [install info](http://nginx.org/en/docs/install.html)

The way nginx and its modules work is determined in the configuration file. By default, the configuration file is named ***nginx.conf*** and placed in one of 
- /usr/local/nginx/conf
- /etc/nginx
- /usr/local/etc/nginx.

###Starting, Stopping, and Reloading Configuration

To start nginx, run the executable file. 

  sudo nginx

Once nginx is started, it can be controlled by invoking the executable with the -s parameter. Use the following syntax:

	nginx -s signal

Where signal may be one of the following:

- stop — fast shutdown
- quit — graceful shutdown
- reload — reloading the configuration file
- reopen — reopening the log files

For example, to stop nginx processes with waiting for the worker processes to finish serving current requests, the following command can be executed:

	nginx -s quit

### 2. Create the SSL self-signed sertificate

``` bash
#create the certificate
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 500

#check the certificate
openssl x509 -in cert.pem -text -noout

```

### 3. Configuration

 Update the nginx.conf with the correct /path/to/your/web/site

### 4. Testing

To verify that the HTTP site is working

  curl http://localhost:8080

The following verifies the SSL passthrough.

  curl https://localhost --insecure

# Troubleshooting

nginx-ssl
	sudo nginx -s stop && sudo nginx
	
	cat /usr/local/var/run/nginx.pid

