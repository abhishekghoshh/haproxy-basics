haproxy playlist:

    https://www.youtube.com/playlist?list=PLfnwKJbklIxwxXKiPv5nAgWwmaUvDjW_t 

Sample haproxy config:

    https://github.com/hnasr/javascript_playground/blob/master/proxy/test.cfg#L8

To implement https in haproxy:

    frontend https-in
        bind *:80
        bind *:443 ssl crt server-cert.pem ca-file ssl-min-ver TLSv1.1 alpn h2,http/1.1
        http-request redirect scheme https unless { ssl_fc }


To implment client certificate refference link:

    haproxy.com/blog/restrict-api-access-with-client-certificates-mtls
    https://www.loadbalancer.org/blog/client-certificate-authentication-with-haproxy/
    
code:

    frontend mysite
        bind *:80
        bind *:443  ssl crt server-cert.crt verify required ca-file intermediate-client-ca.crt ca-verify-file client-root-ca.crt
        http-request redirect scheme https unless { ssl_fc }
        default_backend apiservers