DATE:=$(shell date +%Y%m%d-%H%M%S)

MYSQL_USER=root
MYSQL_PASS=root
MYSQL_HOST=localhost
MYSQL_SLOW_QUERY_LOG=/var/log/mysql/mysql-slow.log

NGINX_ACCESS_LOG=/opt/log/nginx/access.log
NGINX_ERROR_LOG=/opt/log/nginx/error.log

NGINX_DEFAULT_CONF=/home/centos/private-isu/webapp/etc/nginx/conf.d/default.conf
NGINX_CONF=/home/centos/private-isu/webapp/etc/nginx/nginx.conf
MYSQL_CONF=/home/centos/private-isu/webapp/etc/my.cnf

.PHONY: slow_query_on
slow_query_on:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'ON'; SET GLOBAL slow_query_log_file = '$(MYSQL_SLOW_QUERY_LOG)'; SET GLOBAL long_query_time = 0.001;"
	sudo chmod 777 $(MYSQL_SLOW_QUERY_LOG)

.PHONY: slow_query_off
slow_query_off:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'OFF';"

.PHONY: show_slow_query
show_slow_query:
	sudo mysqldumpslow -s t $(MYSQL_SLOW_QUERY_LOG)

.PHONY: pull
pull:
	git pull origin master
	sudo rm -rf /etc/my.cnf
	sudo rm -rf /etc/nginx/conf.d/default.conf
	sudo rm -rf /etc/nginx/nginx.conf
	sudo cp -r $(MYSQL_CONF) /etc/
	sudo cp -r $(NGINX_DEFAULT_CONF) /etc/nginx/conf.d/
	sudo cp -r $(NGINX_CONF) /etc/nginx/

.PHONY: restart
restart:
	sudo systemctl restart mysqld.service
	sudo systemctl restart nginx.service

.PHONY: log-reset
log-reset:
	mkdir -p ~/logs/$(DATE)
	-sudo mv -f $(MYSQL_SLOW_QUERY_LOG) ~/logs/$(DATE)/slow-query.txt
	-sudo mv -f $(NGINX_ACCESS_LOG) ~/logs/$(DATE)/access.txt
	-sudo mv -f $(NGINX_ERROR_LOG) ~/logs/$(DATE)/error.txt


.PHONY: alp-%
alp-%:
	alp -f $(NGINX_ACCESS_LOG) --aggregates=$(patsubst alp-%,%,$@)

.PHONY: alp
alp:
	alp -f $(NGINX_ACCESS_LOG)
