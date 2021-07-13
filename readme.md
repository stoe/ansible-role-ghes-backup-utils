# ansible-role-configure-backup-utils

> Configure [backup-utils](https://github.com/github/backup-utils) for GitHub Enterprise Server.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see [`defaults/main.yml`](defaults/main.yml)).

```yml
github_host: github.example.com
```

GitHub Enterprise Server (primary) hostname.

```yml
backup_utils_repo_url: https://github.com/github/backup-utils.git
backup_utils_version: master
```

GitHub Enterprise Server Backup Utilities repository source and version to download.

```yml
backup_utils_home_dir: /home/admin
```

Server home directory.

```yml
backup_utils_dir: /home/admin/backup-utils
```

GitHub Enterprise Server Backup Utilities home directory.

```yml
backup_utils_data_dir: /home/admin/backup-utils/data
```

Path to where backup data is stored.
By default this is the `data/` directory within `backup_utils_dir`, but can be set to an absolute path elsewhere for backing up to a separate partition / mount point.

```yml
backup_utils_create_data_dir: 'yes'
```

If set to `no`, `GHE_DATA_DIR` will not be created automatically

```yml
backup_utils_retention: 10
```

The number of backup snapshots to retain.

Old snapshots are pruned after each successful ghe-backup run.
This option should be tuned based on the frequency of scheduled backup runs.
If backups are scheduled hourly, snapshots will be available for the past `N` hours; if backups are scheduled daily, snapshots will be available for the past `N` days...

```yml
backup_utils_log_name: backup-verbose.log
```

Filename within `backup_utils_dir` to write extra log output to.

```yml
backup_utils_es_audit_logs: 'no'
```

Backup Elasticsearch audit log indices? If set to `no` (default), Elasticsearch audit log indices will not be backed up.

> Note that they will still be backed up from MySQL.
> This will reduce the time and size of the backup process but it will take longer for the audit log entries to be searchable as they need to be reindexed in Elasticsearch.

## Dependencies

None.

## Example Playbook

```yml
- hosts: backup
  roles:
    - role: configure_backup_utils
      github_host: github.example.com
```
