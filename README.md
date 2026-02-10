# Odoo 17 Local Installation

Ce dépôt contient une version locale d’Odoo 17 prête à installer et à configurer sur Ubuntu 22.04/24.04.

---

## 1️⃣ Prérequis système

Installez les paquets essentiels :

```bash
sudo apt update
sudo apt install -y git python3 python3-pip python3-venv python3-setuptools postgresql postgresql-contrib build-essential libxml2-dev libxslt1-dev libjpeg-dev zlib1g-dev libpq-dev libldap2-dev libsasl2-dev libffi-dev wkhtmltopdf nodejs npm

git clone https://github.com/omarnebi/odoo17.git
cd odoo17
python3 -m venv venv --upgrade-deps
source venv/bin/activate

which python
# /home/username/odoo17/venv/bin/python
pip install --upgrade pip
pip uninstall -y setuptools
pip install "setuptools<70" wheel

pip install -r requirements.txt
sudo -u postgres createuser -s odooevent
sudo -u postgres psql
\password odooevent
puis \q pour quitter postgres
créer avec nano odoo.conf
puis ajouter ces lignes dans odoo.conf
----
[options]
admin_passwd = admin
db_host = False
db_port = False
db_user = odooevent
db_password = odoo17
addons_path = addons,custom_addons
xmlrpc_interface = 0.0.0.0
xmlrpc_port = 8069
longpolling_port = 8072
logfile = odoo.log
log_level = info
workers = 0
limit_memory_soft = 640000000
limit_memory_hard = 760000000
limit_time_cpu = 600
limit_time_real = 1200
---
cd ~/odoo17
./odoo-bin -c odoo.conf







