
- confiugre hosts

        192.168.147.135 node1
        192.168.147.136 node2
        92.168.147.137 node3

- add authorized_keys

        ssh-copy-id -i ~/.ssh/id_rsa.pub postgres@node1
        ssh-copy-id -i ~/.ssh/id_rsa.pub postgres@node2
        ssh-copy-id -i ~/.ssh/id_rsa.pub postgres@node3

- install build env

        yum install gcc bison flex perl-ExtUtils-Embed perl python-devel tcl-devel readline-devel openssl-devel krb5-devel e2fsprogs-devel libxml2-devel libxslt-devel pam-devel libuuid-devel openldap-devel openjade opensp docbook-dtds libicu-devel gettext systemd-devel glib2-devel

- build

        git clone git@github.com:jinyyu/postgres-xl.git
        cd postgres-xl
        ./build.sh

- configure  ~/.bashrc

        export PGUSER=postgres
        export PGHOME=/usr/local/pgsql
        export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$PGHOME/lib
        export PATH=$PATH:$PGHOME/bin
        export TEMP=/tmp
        export TMPDIR=/tmp

- pgxc_ctl 

        pgxc_ctl
        PGXC prepare 
        PGXC exit

- edit vim pgxc_ctl.conf

- init cluster

        pgxc_ctl  -c  ~/pgxc_ctl/pgxc_ctl.conf init all

- start cluster

        pgxc_ctl  -c  ~/pgxc_ctl/pgxc_ctl.conf start all

- stop cluster

        pgxc_ctl  -c  ~/pgxc_ctl/pgxc_ctl.conf stop all


- test 

        psql -p 20008
        create database test;
        \c test;
        create table test(id int,name text);
        insert into test(id, name) values(1, 'abc');
        insert into test(id, name) values(2, 'def');
        insert into test(id, name) values(3, 'kkk');
