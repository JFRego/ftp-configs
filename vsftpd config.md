#vsftpd config debian base


- install vsftpd;

        apt install vsftpd 
        
- get your certs signed as server type and place;

        .cert file inside /etc/ssl/certs
        .key file inside /etc/ssl/private
                run chmod 640 .key - to change permission
                    chgrp ssl-cert .key - Note u may need to install ssl-cert;

- now open /etc/vsftpd.conf;

        - change no to yes in this line;
                
                listen=YES
                
        - change yes to no;
        
                listen_ipv6=NO
                
        - uncomment and change no to yes;
        
                write_enable=YES
                
        - now edit the cert and key file to your own files and change no to yes;
        
                rsa_cert_file=/etc/ssl/certs/ftpinova.crt
                rsa_private_key_file=/etc/ssl/private/ftpinova.key
                ssl_enable=YES
                
        - add the following lines to the bottom of the file for implicit ssl;
        
                pasv_enable=YES
                pasv_min_port=10000
                pasv_max_port=10100

                allow_anon_ssl=NO
                force_local_data_ssl=YES
                force_local_logins_ssl=YES
                ssl_tlsv1=YES
                ssl_sslv2=NO
                ssl_sslv3=NO
                require_ssl_reuse=NO
                ssl_ciphers=HIGH

                implicit_ssl=YES
                listen_port=990
        
        - for explicit ssl just remove the last two lines;
        
- now just restart vsftpd;
        
        systemctl restart vsftpd
        
- and its done;

