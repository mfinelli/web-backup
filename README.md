# Web Backup

Backup public upload directory to S3.

## Dependencies

### s3cmd

[s3cmd](https://github.com/s3tools/s3cmd) is used to actually interact with
s3 and upload the files, so you need to install and configure it first.
Install it with your preferred package manager and then configure:

```shell
$ s3cmd --configure
```

## Configuration

### Backup

Configuration for the backup is saved in your home directory in the
`.webbackup` file. It is essentially just another bash script that defines
variables used for the backup. It simply gets sourced before the backup runs.

You need to define the encryption password, s3 bucket and the paths that need
to be backed up.

```shell
# Choose a long, strong password to encrypt the backups.
PASSPHRASE="AReallyGoodPassword"

# List of paths to backup:
WEBPATHS=('/srv/http/site1/uploads', '/srv/http/site2/uploads')

# List of "folders" for each backup path:
PREFIX=('site1' 'site2')

# List your buckets with `s3cmd ls`.
BUCKET="your-backup-bucket"
```

### Sync

Configuration for the sync is saved in your home directory in the `.websync`
file. It is essentially just another bash script that defines variables used
for the sync. It then gets sourced before the sync runs.

You need to define the S3 bucket, and all of the paths that will be saved.

```shell
# List of paths to backup:
WEBPATHS=('/srv/http/site1/uploads', '/srv/http/site2/uploads')

# List "folders" for each backup path:
PREFIX=('site1' 'site2')

# List your buckets with `s3cmd ls`.
BUCKET="your-backup-bucket"
```

## Usage

### Backup

Running the backup is easy! Just run the `webbackup` script!

To restore from the backup you will need to run the sync in reverse (see
below) and then decrypt the files with `gpg` and your passphrase.

### Sync

Running the backup is easy! Just run the `websync` script!

To restore a backup to a folder you can just run the sync command in reverse:

```shell
$ s3cmd sync s3://your-bucket/prefix/ ./
```
