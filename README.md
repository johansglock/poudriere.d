# Poudriere

## Setup
Install poudriere with:
```
pkg install poudriere
```

After installation, modify the configuration with:
```
ZROOTFS=/poudriere
FREEBSD_HOST=http://ftp.nl.freebsd.org
```

Setup all package and make configurations by downloading this repo:
```
git clone https://github.com/johansglock/poudriere.d.git /usr/local/etc/poudriere.d
```

Create ports tree:
```
poudriere ports -c
```

Create a jail to build packages:
```
poudriere jail -c -j 10amd64 -v 10.0-RELEASE -a amd64
```

## Running
Update the ports tree with:
```
poudriere ports -u
```

Build all packages with:
```
poudriere bulk -j 10amd64 -f /usr/local/etc/poudriere.d/10amd64-plist
```
