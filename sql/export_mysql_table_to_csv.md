select * from hotels
into outfile '/home/derby/temp_csv/test.csv'
FIELDS ENCLOSED BY '"'
terminated by ';'
escaped by '"'
lines terminated by '\r\n';


TABLE dingdandao.hotels 
INTO OUTFILE '/home/derby/temp_csv/test.csv'
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
ESCAPED BY ''
LINES TERMINATED BY '\n';

TABLE dingdandao.hotels
into outfile '/home/derby/temp_csv/test.csv'
FIELDS ENCLOSED BY '"'
terminated by ';'
escaped by '"'
lines terminated by '\r\n';

mysqldump dingdandao hotels --fields-terminated-by ',' \
--fields-enclosed-by '"' --fields-escaped-by '\' \
--no-create-info --tab /home/derby/temp_csv -u root -p \
-h bps-ddd-bi-uat.cluster-c3siuwdqpqse.rds.cn-northwest-1.amazonaws.com.cn


 mysql -B -u root -p  --database dingdandao -h bps-ddd-bi-uat.cluster-c3siuwdqpqse.rds.cn-northwest-1.amazonaws.com.cn \
  -e "SELECT * FROM hotels;" \
 | sed "s/\"/\"\"/g;s/'/\'/;s/\t/\",\"/g;s/^/\"/;s/$/\"/;s/\n//g" > outfile.csv

mysql -B -u root -p  --database dingdandao \
-h bps-ddd-bi-uat.cluster-c3siuwdqpqse.rds.cn-northwest-1.amazonaws.com.cn \
-e "SELECT * FROM aggregated_orders;" \
| sed "s/\"/\"\"/g;s/'/\'/;s/\t/\",\"/g;s/^/\"/;s/$/\"/;s/\n//g" > aggregated_orders.csv