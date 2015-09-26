# Web Backup

Backup public upload directory to S3.

## Configuration

Configuration for the backup is saved in your home directory in the
`.webbackup` file. It is essentially just another bash script that defines
variables used for the backup. It simply gets sourced before the backup runs.

You need to define the S3 bucket, and all of the paths that will be saved.

```shell
# List of paths to backup:
WEBPATHS=('/srv/http/site1/uploads', '/srv/http/site2/uploads')

# List your buckets with `s3cmd ls`.
BUCKET="your-backup-bucket"
```
