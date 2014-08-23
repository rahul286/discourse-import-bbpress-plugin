Notes for mysql on mac.

Installing mysql locally and importing wordpress/bbpress database to speed up dev+tetsing.

## Install mysql

``` brew install mysql```

## Mysql notes

### To connect

After changing password

```
mysql -u root -p root
```

## Mysql start

```
mysql.server start
```

##To have launchd start mysql at login:

```
ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents

```

## Then to load mysql now:

```
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```
