# Notes

## This assumes local ip of 192.168.33.15

## How-to start Citrix ADC CPX in docker:

It turns out that the trick is not to use to many environment settings:

´´´bash
docker run -dt --privileged=true -e EULA=yes -e CPX_CORES=5 --name cpx_host -p 9080:9080 -p 443:9443 -p 9081:80 -P quay.io/citrix/citrix-k8s-cpx-ingress:13.0-83.27
´´´

To get the nsroot password:

´´´bash
docker exec cpx_host cat /var/random_id
´´´

To fix the /var/nstmp permissions problem

´´´bash
docker exec cpx_host chmod 777 /var/nstmp
´´´

## general commands

k apply -f app-httpd-v2.yaml
k apply -f example\guestbook\guestbook-ingress.yaml