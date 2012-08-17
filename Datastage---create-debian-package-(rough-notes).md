(Work in progress)

# Required packages from apt-repo.bodleian.ac.uk.uk and elsewhere

## Ubuntu base system

(Using on Ubuntu 12.04 64-bit server default base install)

Don't forget:

    sudo apt-get update
    sudo apt-get upgrade

Add the following packages to get going

1. build-essential 
2. linux-headers-$(uname -r)
3. vmware-tools (from VMWare host - tried apt package, didn't work for me - neither did vmware tools work: problems with driver builds)
4. openssh-server
5. python-setuptools

(For fixing IP addresses in VMWare Fusion environment, see http://nileshk.com/2009/06/24/vmware-fusion-nat-dhcp-and-port-forwarding.html)


## dataflow-datastage package depenencies

    python-django-conneg
    python-django-longliving
    python-django-pam
    python-rdflib
    python-lxml
    python-redis
    python-oauth2
    python-flup
    python-tz
    python-libmount
    python-sword-client
    redis-server
    postgresql
    postgresql-client
    python-psycopg2
    python-xattr
    python-webdav
    apache2
    chkconfig
    libapache2-mod-scgi
    pwgen
    samba
    python-pylibacl

## From apt-repo.bodeian

See http://apt-repo.bodleian.ox.ac.uk/ datastage link for details.

    sudo apt-get install python-django-conneg
    sudo apt-get install python-django-longliving
    sudo apt-get install python-django-pam
    sudo apt-get install python-sword-client
    sudo apt-get install python-libmount

## From public repos

    sudo apt-get install python-webdav
    sudo apt-get install python-pylibacl
    sudo apt-get install python-rdflib
    sudo apt-get install python-lxml
    sudo apt-get install python-redis
    sudo apt-get install python-oauth2
    sudo apt-get install python-flup
    sudo apt-get install python-tz
    sudo apt-get install redis-server
    sudo apt-get install postgresql
    sudo apt-get install postgresql-client
    ###sudo apt-get install python-psycopg2
    sudo apt-get install python-xattr
    sudo apt-get install apache2
    sudo apt-get install chkconfig
    sudo apt-get install libapache2-mod-scgi
    sudo apt-get install pwgen
    sudo apt-get install samba

# Create Debian package and install

    apt-get install debhelper
    apt-get install python-all
    apt-get install python-django

    ##cp -rf (git-workspace)/DataStage/* /root/DataStage
    rm -rf debian-package/
    make debian-package
    dpkg -i  debian-package/*.deb
    /etc/init.d/datastage stop
    /etc/init.d/datastage start


# Installation from existing package (short form)

    ssh-keygen -t rsa -C "your_email@youremail.com"
    less /root/.ssh/id_rsa.pub 
    copy the conteensts and add to git hub (admin ssh keys)
    git clone git@github.com:dataflow/DataStage.git
    cd  DataStage
    git checkout remotes/origin/UIChanges
    apt-get install make
    apt-get install python-all
    apt-get install debhelper
    cd Datastage ( root directory)
    dpkg -i  debian-package/*.deb
 
Then type datastage-config (command-line admin tool)  to run the services and get started.

# Installation from existing package (long form)

    apt-get install  python-rdflib 
    apt-get install  python-lxml 
    apt-get install  python-redis 
    apt-get install  python-oauth2 
    apt-get install  python-flup 
    apt-get install  python-tz 
    apt-get install  redis-server 
    apt-get install  postgresql 
    apt-get install  postgresql-client
    apt-get install  python-psycopg2 
    apt-get install  python-django (>= 1.3) 
    apt-get install  python-xattr 
    apt-get install  apache2
    apt-get install  chkconfig 
    apt-get install  libapache2-mod-scgi 
    apt-get install  pwgen 
    apt-get install  samba 
    apt-get install  python-pylibacl 
    pip install pywebdav


    wget http://apt-repo.bodleian.ox.ac.uk/datastage/pool/main/p/python-django-conneg/python-django-conneg_0.7.3~20120314112126_all.deb
    dpkg -i python-django-conneg_0.7.3~20120314112126_all.deb


    wget http://apt-repo.bodleian.ox.ac.uk/datastage/pool/main/p/python-django-longliving//python-django-longliving_0.5-20120227121126_all.deb

    dpkg -i python-django-longliving_0.5-20120227121126_all.deb

    wget http://apt-repo.bodleian.ox.ac.uk/datastage/pool/main/p/python-django-pam/python-django-pam_1.0_all.deb
    dpkg -i python-django-pam_1.0_all.deb

    wget http://apt-repo.bodleian.ox.ac.uk/datastage/pool/main/p/python-libmount/python-libmount_0.9_all.deb
    dpkg -i  python-libmount_0.9_all.deb

    apt-get install make
    apt-get install python-all
    apt-get install python-setuptools
    apt-get install debhelper
    cd Datastage ( root directory)
    dpkg -i  debian-package/*.deb
 
Then type datastage-config (command-line admin tool)  to run the services and get started.
