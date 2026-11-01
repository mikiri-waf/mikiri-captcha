1. Install as needed depending on:

```bash
apt update && apt install -y nginx python3 python3-venv python3-pip memcached git
python3 -m venv /var/www/mikiri-captcha/venv
/var/www/mikiri-captcha/venv/bin/python3 -m pip install --upgrade pip
/var/www/mikiri-captcha/venv/bin/python3 -m pip install -r /var/www/mikiri-captcha/requirements.txt
```

2. Download Mikiri CAPTCHA from the GitHub repository and configure it:

```bash
cd /var/www/
git clone https://github.com/mikiri-waf/mikiri-captcha
mkdir -p /var/log/mikiri-waf/captcha
chmod -R 0750 /var/log/mikiri-waf/captcha
chown -R www-data:www-data /var/log/mikiri-waf/captcha
cp /var/www/mikiri-captcha/misc/mikiri-captcha /etc/logrotate.d/
cp /var/www/mikiri-captcha/misc/mikiri-captcha.service /lib/systemd/system/
```

3. Run the application:

```bash
systemctl enable mikiri-captcha
systemctl start mikiri-captcha
```

4. Check status and log for errors:

```bash
systemctl status mikiri-captcha
cat /var/log/mikiri-waf/captcha/api.log
netstat -nlp | grep 8080
```

5. Keep your environment up to date. Run this command to update pip:

```bash
/var/www/mikiri-captcha/misc/pip_update.sh
```
