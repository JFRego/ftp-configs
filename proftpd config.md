#proftpd config red hat based


- install proftpd;

        sudo amazon-linux-extras install epel
        
        yum install proftpd
        
- place your certificates signed as server type inside;

        .crt in /etc/ssl/certs
        .key in /etc/ssl/private
                run chmod 600 .key to change permissions;
                
-  now open /etc/proftpd.conf file;

        - define passive ports for ftp passive mode;

                PassivePorts    6000    6100

        - then look for this following line and comment it;

                #<IfDefine TLS>
                
        - edit tls crt and key file for your own files;

                TLSRSACertificateFile         /etc/ssl/certs/ftpenta.crt
                TLSRSACertificateKeyFile      /etc/ssl/private/ftpenta.key            

        - uncomment this line;

                TLSRenegotiate                ctrl 3600 data 512000 required off timeout 300
                
        - then comment this 4 following lines;

                #  <IfModule mod_tls_shmcache.c>
                #    TLSSessionCache            shm:/file=/var/run/proftpd/sesscache
                #  </IfModule>
                #</IfDefine>

        - now just save the file;

- after that enable and start proftpd;

        systemctl enable --now proftpd
        
- and its done;
        
