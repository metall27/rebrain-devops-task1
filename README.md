# Конфигурационный файл Nginx.
  This project contains the ** nginx ** configuration file 

## Getting Started
  This guide will help clarify the use of this configuration file for Nginx

### Dependencies
1. Linux OS
2. Nginx

### Configuration
  By default the file is named nginx.conf and for NGINX Plus is placed in the /etc/nginx directory

### Directives
  The configuration file consists of directives and their parameters. Simple (single‑line) directives each end with a semicolon. Other directives act as “containers” that group together related directives, enclosing them in curly braces ( {} ); these are often referred to as blocks. Here are some examples of simple directives.

### Feature-Specific Configuration Files
  To make the configuration easier to maintain, we recommend that you split it into a set of feature‑specific files stored in the /etc/nginx/conf.d directory and use the include directive in the main nginx.conf file to reference the contents of the feature‑specific files.

### Contexts
  A few top‑level directives, referred to as contexts, group together the directives that apply to different traffic types:

  * `events` – General connection processing
  * `http` – HTTP traffic
  * `mail` – Mail traffic
  * `stream` – TCP and UDP traffic

  Directives placed outside of these contexts are said to be in the main context.

### Virtual Servers
  In each of the traffic‑handling contexts, you include one or more server blocks to define virtual servers that control the processing of requests. The directives you can include within a server context vary depending on the traffic type.

  For HTTP traffic (the http context), each server directive controls the processing of requests for resources at particular domains or IP addresses. One or more location contexts in a server context define how to process specific sets of URIs.

  For mail and TCP/UDP traffic (the mail and stream contexts) the server directives each control the processing of traffic arriving at a particular TCP port or UNIX socket.

### Sample Configuration File with Multiple Contexts
  The following configuration illustrates the use of contexts.

    user nobody; # a directive in the 'main' context
    events {
        # configuration of connection processing
    }
    http {
        # Configuration specific to HTTP and affecting all virtual servers  
        server {
            # configuration of HTTP virtual server 1       
            location /one {
                # configuration for processing URIs starting with '/one'
            }
            location /two {
                # configuration for processing URIs starting with '/two'
            }
        } 
        
        server {
            # configuration of HTTP virtual server 2
        }
    }
    stream {
        # Configuration specific to TCP/UDP and affecting all virtual servers
        server {
            # configuration of TCP virtual server 1 
        }
    }

### Reloading Configuration
  For changes to the configuration file to take effect, it must be reloaded. You can either restart the **nginx** process or send the **reload** signal to upgrade the configuration without interrupting the processing of current requests. For details, see Controlling NGINX Processes at Runtime.

  With NGINX Plus, you can dynamically reconfigure load balancing across the servers in an upstream group without reloading the configuration. You can also use the NGINX Plus API and key‑value store to dynamically control access, for example based on client IP address.