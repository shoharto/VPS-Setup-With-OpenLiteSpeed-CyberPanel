# VPS Setup With OpenLiteSpeed & CyberPanel

This server setup guidline for the very begginers VPC Lover.

## Installation OpenLiteSpeed

Use the package manager [openlitespeed](https://openlitespeed.org/kb/) to install OpenLiteSpeed.

```bash
pip install OpenLiteSpeed
```

## Installation CyberPanel

Use the package manager [openlitespeed](https://openlitespeed.org/kb/) to install CyberPanel.

```bash
pip install OpenLiteSpeed
```
## Install OLS from LiteSpeed Repositories
1. Add the Repository

```
wget -O - http://rpms.litespeedtech.com/debian/enable_lst_debian_repo.sh | bash
```

2. Install OpenLiteSpeed

```
apt-get install openlitespeed
```

3. Install PHP

```
apt-get install lsphp73
ln -sf /usr/local/lsws/lsphp73/bin/lsphp /usr/local/lsws/fcgi-bin/lsphp5
```

4. Getting Started

- Run Server

```
/usr/local/lsws/bin/lswsctrl start
```

- Stop Server

```
/usr/local/lsws/bin/lswsctrl stop
```
- The default port for the WebAdmin console is 7080
- Reset OpenLiteSpeed Admin Password And Username

```
Use the following to reset: /usr/local/lsws/admin/misc/admpass.sh
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
