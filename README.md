# docker-scm-manager
Docker container for SCM-Manager (http://www.scm-manager.org/). Image ready for OpenMediaVault Docker plugin.

## Port
This image expose port 8080.

## Volume
You can save your data by mapping them to the volume /var/lib/scm.

## Usage
Set permission to the scm folder mapping
  mkdir /var/lib/scm
  chown 1000:1000 /var/lib/scm
  
Then start the image
  docker run -v /var/lib/scm:/var/lib/scm -p 8030:8080 sdorra/scm-manager

## Nginx redirection for OMV

Create a configuration file in /etc/nginx/openmediavault-webgui.d/ named scm-manager.conf wich contains :

  location /scm {
         proxy_pass         http://localhost:8030/scm;
         proxy_set_header   Host localhost:8030;
          proxy_redirect    default;
  }
Then reload nginx configuration :
  service nginx reload
