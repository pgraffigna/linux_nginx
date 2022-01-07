# linux_nginx

Repo con notas para la instalación de un servidor NGINX.

Testeado con Ubuntu 18.04.

---

instalación:
```bash
apt install nginx -y
```

configuración de sitios disponibles:
```bash
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/testing.page
nano /etc/nginx/sites-available/testing.page
```
activando los sitios disponibles:
```bash
ln -s /etc/nginx/sites-available/testing.page .
```

recargamos el servicio nginx:
```bash
nginx -s reload
```

mostramos contenido en la pagina:
```bash
mkdir /var/www/test 
touch /var/www/test/index.html
echo "esto es una prueba" > /var/www/test/index.html
```

agregando soporte para PHP a los sitios:
```bash
apt install -y php-fpm
```
validar los cambios en la configuración:
```bash
nginx -t 
systemctl reload nginx	
```

configurando certificados con let's encrypt:
```bash
apt install -y certbot
certbot --nginx
certbot renew --dry-run #para chequear el estado del certificado
```

balanceo de carga entre apps con nginx proxy reverso:
```bash
nano /etc/nginx/nginx.conf

http {
	upstream backend {
		server app1:8080 weight=5; # mas carga de trabajo a este servidor
		server app2:8080;
	}
}
```
