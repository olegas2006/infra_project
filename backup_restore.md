# Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

## Restore MySQL data from the backup:

1. Get root previleges `sudo -i`, use `whoami` to check
2. Download backup: `sudo -u backup duplicity --no-encryption restore rsync://olegas2006@backup.infroha.ro/mysql /home/backup/restore/mysql`
3. Put backup data in agama database: `sudo mysql agama < /home/backup/restore/mysql/agama.sql` 

Check if backups were restored:
1. Check if MySQL is running: `service mysql status`
2. Check if data form backup was parsed in database: `mysql -e "SELECT * FROM agama.item"`
3. Check the agama page

## Restore InfluxDB data from the backup:

1. Get root previleges `sudo -i`, use `whoami` to check
2. Download backup: `sudo -u backup duplicity --no-encryption restore rsync://olegas2006@backup.infroha.ro/influxdb /home/backup/restore/influxdb`
3. Stop Telegraf: `service telegraf stop` 
4. Delete old Telegraf database: `influx -execute 'DROP DATABASE telegraf'` 
5. Put backup data in telegraf database: `influxd restore -portable -db telegraf /home/backup/restore/influxdb` 
6. Start Telegraf: `service telegraf start` 

Check if backups were restored:
1. Check if Telegraf is running: `sudo service telegraf status`
2. Check if data form backup was parsed in database(50 rows, can modify the statement for more): `influx -database 'telegraf' -execute "SELECT * FROM syslog LIMIT 50"`
3. Check the syslog page in grafana