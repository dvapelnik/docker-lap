#Readme

This is Docker Debian based image for web development with php5.6.4

##Usage

Check your nonprivileged for regular developing user and group id before image building 

```bash
# check user id
id -u 
# check group id
id -g
```

If user id and group id not equivalent 1000 then you must change this value in Dockerfile:

```bash
sed -i "s/-g 1000/-g `id -g`/g" Dockerfile
ser -i "s/-u 1000/-u `id -u`/g" Dockerfile
```

Build image firstly

```bash
sudo docker build --rm -t `whoami`/debian:jessie.php56 .
```

Start your container with share local folder

```bash
echo "<?php phpinfo(); ?>" > /tmp/index.php
sudo docker run -d --name web -p 80:80 -v /tmp/index.php:/var/www/index.php jdoe/debian:jessie.php56
```

And browse: [http://localhost/index.php](http://localhost/index.php). You must see phpinfo() as result.
