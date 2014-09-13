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

Link the default patch location into this repository:
```
ln -s /usr/local/etc/poudriere.d/local-patches/ /usr/ports/distfiles/local-patches
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

After updating the plist, make configurations with:
```
poudriere options -j 10amd64 -f /usr/local/etc/poudriere.d/10amd64-plist
```

## Repository for pkgng
Nginx configuration within the host:
```
location /pkg-repo/ {
    alias   /usr/local/poudriere/data/packages/;
    index   index.html index.html;
    autoindex on;
}
```

pkgng configuration:
```
MyRepo: {
  url: "pkg+https://example.com/pkg-repo/10amd64-default",
  mirror_type: "srv",
  signature_type: "none",
  enabled: yes
}
```

## TODO
* Setup pkg signing
