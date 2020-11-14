# pgpool


Master node

yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
yum install -y postgresql96-server
yum install -y pgpool-II-96.x86_64
yum install -y wget

cd /etc/pgpool-II-96/
wget -qO pgpool.conf  https://raw.githubusercontent.com/RomanGorokhov/pgpool/main/pgpool.conf
wget -qO pool_passwd https://raw.githubusercontent.com/RomanGorokhov/pgpool/main/pool_passwd

cd /var/lib/pgsql/9.6/data/
wget -qO pg_hba.conf https://raw.githubusercontent.com/RomanGorokhov/pgpool/main/pg_hba.conf
wget -qO postgresql.conf  https://raw.githubusercontent.com/RomanGorokhov/pgpool/main/postgresql.conf

/usr/pgsql-9.6/bin/postgresql96-setup initdb
systemctl start postgresql-9.6
systemctl start pgpool-II-96

su postgres -c 'psql'

\password postgres


Slave node

yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
yum install -y postgresql96-server

/usr/pgsql-9.6/bin/postgresql96-setup initdb
systemctl start postgresql-9.6

su postgres -c 'psql'

\password postgres

