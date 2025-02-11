# Backup SLA

## Coverage

We back up services that satisfy at least one of these criteria:
 - are primary source of truth for particular data
 - contain customer and/or client data
 - are not feasible (or very costly) to restore by other means

Services that are backed up:
 - MySQl
 - InfluxDB
 - GitHub repository


## Schedule

MySQL backups are created every 24 hours; it takes up to 15 minutes to create and store the backup.

InfluxDB backups are created every 24 hours; it takes up to 15 minutes to create and store the backup.

GitHub repository backups are created every 30 minutes; it takes up to 1 minute to create and store the backup.

All backups are started automatically by crontab.

Backup RPO (recovery point objective) is:
 - 24 hours for MySQL
 - 24 hours for InfluxDB
 - 30 minutes for Github repo


## Storage

MySQL and InfluxDB backups are uploaded to the backup server.

GitHub repository is mirrored to the internal Git server.

Backup data from both servers will be synchronized to encrypted AWS S3 bucket in future (work in progress).


## Retention

MySQL backups are stored for 7 days; 7 versions (recovery points) are available to restore.

InfluxDB backups are stored for 7 days; 7 versions are available to restore.

Repository backups are stored for 180 days; 180 versions are available to restore.


## Usability checks

MySQL backups are verified every 7 minutes by backup exporter.

InfluxDB backups are verified every 7 minutes by exporter.

Repository backups are verified every 30 minutes by a script.


## Restore process

Service is recovered from the backup in case of an incident, and when service cannot be restored in any other way.

RTO (recovery time objective) is:
 - 5 minutes for MySQL
 - 5 minutes for InfluxDB
 - 15 minutes for Repository

Detailed backup restore procedure is documented in the [backup_restore.md](./backup_restore.md).