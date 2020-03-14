# mod_pascal

Apache 2.4 module implementation which is capable to execute Pascal program just like scripting language.

## Requirement

- [Free Pascal compiler](https://www.freepascal.org)
- [Apache 2.4](https://httpd.apache.org/docs/2.4/)

## Setup

### TL;DR

```
$ git clone https://github.com/zamronypj/mod_pascal.git
$ cd_mod_pascal
$ ./build.sh
$ sudo ./install.sh
```

### Clone this repository

```
$ git clone https://github.com/zamronypj/mod_pascal.git
```

### Compile mod_pascal

```
$ fpc mod_pascal
```
or with optimization level 3

```
$ fpc -O3 mod_pascal
```

### Add Apache configuration to load module

For example in Debian,

Create `pascal.conf` file in `/etc/apache2/mods-available` directory with content as follows,

```
<IfModule pascal_module>
    # handle all files having .pas extension
    AddHandler pascal-handler .pas
</IfModule>
```

Create `pascal.load` file in `/etc/apache2/mods-available` directory with content as follows,

```
LoadModule pascal_module /path/to/libmod_pascal.so
```
### Enable mod_pascal

Create symlink to `pascal.conf` and `pascal.load` in `/etc/apache2/mods-enabled` directory

```
$ cd /etc/apache2/mods-enabled
$ sudo ln -s /etc/apache2/mods-available/pascal.conf
$ sudo ln -s /etc/apache2/mods-available/pascal.load
```
Alternatively, you can also use `a2enmod` command to enable mod_pascal.

```
$ sudo a2enmod pascal
```

### Restart Apache

```
$ sudo systemctl restart apache2
```

## Execute Pascal program

Create Pascal program, for example  `/var/www/html/test.pas` with content as follows,

```
begin
    writeln('Hello from Pascal');
end.
```

Open URL http://localhost/test.pas from Internet browser, you should see text `Hello from Pascal` printed in browser.
