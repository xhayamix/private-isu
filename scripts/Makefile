MYSQL_USER=root
MYSQL_PASS=root
MYSQL_HOST=localhost
MYSQL_SLOW_QUERY_LOG=/var/log/mysql/mysql-slow.log
slow_query_on:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'ON'; SET GLOBAL slow_query_log_file = '$(MYSQL_SLOW_QUERY_LOG)'; SET GLOBAL long_query_time = 0.001;"
	sudo chmod 777 $(MYSQL_SLOW_QUERY_LOG)
slow_query_off:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'OFF';"
show_slow_query:
	sudo mysqldumpslow -s t $(MYSQL_SLOW_QUERY_LOG)
