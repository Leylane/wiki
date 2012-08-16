These are contents of a couple of internal emails which are dumped here in case they're useful.

# Create Debian package and install

    cp -rf /mnt/hgfs/bhavana/git/DataStage/* /root/DataStage
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
