### Copy File 
> Repostory'de bulunan tüm dosyaları /etc/docker altına kopyalayalım. # All files copy /etc/docker
```
cp -R * /etc/docker/
```
### Reminding

> Benim local ip adresim 192.168.203.130 olduğu için nginx conf'larımda bu ip adresi yazmaktadır. Build etmeden önce kendinize göre değiştirebilirsiniz.
My local ip adress 192.168.203.130 Change ip address in nginx conf file before build

#### Change file
vi default_LBreserver/default.conf
```
server {
    listen       80;
    server_name  local2.com;
    root /var/www;
    location / {
        proxy_pass http://mylocalip:9080;
}
}
server {
    listen      80;
    server_name  local1.com;
    root /var/www;
    location / {
        proxy_pass http://mylocalip:9081;

}
}
```
### Docker Build
> Dockerfile'ları sırasıyla kopyalayıp build edeceğiz # Dockerfile one by one  copy  to build
```
 cp dockerfileLB dockerfile >> docker buid -t nginxlb:01 .
 cp dockerfileWEB1 dockerfile >> docker buid -t nginxweb1:01 .
 cp dockerfileWEB2 dockerfile >> docker buid -t nginxweb2:01 .
```
### Docker run komutları # Docker run command
```
 docker run -ti -d -p 80:80 nginxlb:01
 docker run -ti -d -p 9081:80 nginxweb1:01
 docker run -ti -d -p 9080:80 nginxweb2:
```
### AFTER
> kendi host dosyamızı editleyeceğiz # Edit own host file
###### Linux/MAC
sudo vi /etc/hosts
```
mylocalipadres local1.com
mylocalipadres local2.com
```
######  Windows
C:\Windows\System32\drivers\etc\hosts
```
mylocalipadres local1.com
mylocalipadres local2.com
```

###### test Website templates: http://www.os-templates.com/free-basic-html5-templates/basic-90
