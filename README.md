# nextcloud-fail2ban

WIP

Examples are also located in this repositories `config-examples` directory.

## Nextcloud

Add the following to Nextcloud's config file:

### config/config.php
```
'logtimezone' => 'TIMEZONEHERE',
'log_type' => 'owncloud',
'logfile' => 'nextcloud.log',
```

See a complete list of [valid PHP timezones](http://php.net/manual/en/timezones.php).

## Fail2ban

Add the following to Nextcloud's config files. Remember to restart `fail2ban`
after adding the below. With Debian/Ubuntu this is done with
`/etc/init.d/fail2ban reload`

### filter.d/owncloud.conf

Note: Nextcloud support is pending for the release of the 'nextcloud' log type

```
[INCLUDES]
before = common.conf

[Definition]
failregex = Login failed.*Remote IP.*'<HOST>'
ignoreregex =
```

### jail.local

Add the following to your jail.local file. Note: do not edit your jail.conf
file as changes may be discarded on updates instead, copy jail.conf to
jail.local and make edits there.

```
[owncloud]

enabled  = true
port     = http,https
filter   = owncloud
logpath  = /var/www/nextcloud/nextcloud.log
```
