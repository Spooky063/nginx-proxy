When you want to have a dedicated address for tool, you can create a reverse proxy with the port of you tool and access by server name.

```
server {
        listen 80;
        listen [::]:80;

        server_name adminer.work.lab;

        location / {
                proxy_pass      http://localhost:8080;
                proxy_set_header    Host             $host;
                proxy_set_header    X-Real-IP        $remote_addr;
                proxy_set_header    X-Forwarded-For  $proxy_add_x_forwarded_for;
                proxy_set_header    X-Client-Verify  SUCCESS;
                proxy_set_header    X-Client-DN      $ssl_client_s_dn;
                proxy_set_header    X-SSL-Subject    $ssl_client_s_dn;
                proxy_set_header    X-SSL-Issuer     $ssl_client_i_dn;
                proxy_read_timeout 1800;
                proxy_connect_timeout 1800;
                chunked_transfer_encoding on;
                proxy_set_header X-NginX-Proxy true;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_http_version 1.1;
                proxy_redirect off;
                proxy_buffering off;
        }
}
```
