# how to install postgre on debian 11
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get -y install postgresql
systemctl status postgresql

### create a DB 
passwd postgres
su - postgres 

By default, access to PostgreSQL database server is only from localhost.
check ss -tunelp | grep 5432


vim /etc/postgresql/15/main/postgresql.conf # 15 is my version
listen_addresses = '*' -- Don't do this if your server is on public ne
                       -- or u IP address
                       -- I used localhost 

sudo systemctl restart postgresql

Add a admin database user:
createuser mm_user

createdb mattermost -O mm_user

postgres@great-unicorns-2:~$ psql
postgres=# alter user mm_user with password '123456';
ALTER ROLE
postgres=# exit
postgres@great-unicorns-2:~$ 


