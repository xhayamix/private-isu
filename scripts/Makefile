MYSQL_USER=root
MYSQL_PASS=root
MYSQL_HOST=localhost
MYSQL_SLOW_QUERY_LOG=/var/log/mysql/mysql-slow.log

NGINX_CONF=/home/centos/private-isu/webapp/etc/nginx/conf.d/default.conf
MYSQL_CONF=/home/centos/private-isu/webapp/etc/my.cnf

slow_query_on:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'ON'; SET GLOBAL slow_query_log_file = '$(MYSQL_SLOW_QUERY_LOG)'; SET GLOBAL long_query_time = 0.001;"
	sudo chmod 777 $(MYSQL_SLOW_QUERY_LOG)
slow_query_off:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'OFF';"
show_slow_query:
	sudo mysqldumpslow -s t $(MYSQL_SLOW_QUERY_LOG)

pull:
	git pull origin master
	sudo rm -rf /etc/my.cnf
	sudo rm -rf /etc/nginx/conf.d/default.conf
	sudo cp -r $(MYSQL_CONF) /etc/
	sudo cp -r $(NGINX_CONF) /etc/nginx/conf.d/

.PHONY: restart
restart:
	sudo systemctl restart mysql.service
	sudo systemctl restart nginx.service

