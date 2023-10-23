MYSQL_USER=root
MYSQL_PASS=root
MYSQL_HOST=localhost
slow_query_on:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'ON'; SET GLOBAL slow_query_log_file = '/tmp/slow-query.log'; SET GLOBAL long_query_time = 0.001;"
slow_query_off:
	mysql -u$(MYSQL_USER) -p$(MYSQL_PASS) -e "SET GLOBAL slow_query_log = 'OFF';"