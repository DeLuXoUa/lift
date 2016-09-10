# Elevator test work.

**Setup:**<br>
First you need get rights to write folder 'tmp' on root of project; Easy way is 'chmod 777 ./tmp' from you console.
Please edit your web server config, and change root directory to /path/you/server/elevator/www.<br>
Add www on end of line server root.<br><br><br>
Nginx config sample:<br>


server {<br><br>

server_name elevator.lc<br><br>
root /var/www/elevator/wwws;<br><br>
rewrite ^/(.*)/$ /$1 permanent;<br>
index index.html index.htm index.php;<br><br>
location ~ \.php$ {<br>
try_files $uri = 404;<br>
include fastcgi_params;<br>
fastcgi_pass   127.0.0.1:9000;<br>
fastcgi_index index.php;<br>
fastcgi_split_path_info ^(.+\.php)(.*)$;<br>
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;<br>
fastcgi_ignore_client_abort on;<br>
}<br><br>

location / {<br>
 try_files $uri $uri/ /index.php;<br>
}<br><br>

}



**Start work:**<br>

If you user non graphic UI (gui = false in config.ini), you can use next methods:
<br><br>
\cabin\cabin_class::instance()->touchPanel(3);<br>
touchPanel(3) - use for add floor in stack from cabin interface. In example argument 3 is floor.
<br><br>

\callpanel\call_class::instance()->callClick(4);<br>
callClick(4) - use for outside elevator call. In example 4 - is floor from which cause.


<br><br>
\cabin\cabin_class::instance()->run();<br>
\callpanel\call_class::instance()->run();<br>
run() - methods to start elevator move according to call stack.


---
