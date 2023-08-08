![image](https://github.com/falahatme/ceph/assets/7458874/5d776b72-8f2d-4dd3-8a9a-18c9e40d05a9)

![image](https://github.com/falahatme/ceph/assets/7458874/788d19ad-a9ec-4757-be2d-17ce78b5dccc)

# Nodes:

====================================

    Ceph Admin:     192.168.182.128 (hostname: ceph-admin)
    Ceph Monitor1:  192.168.182.130 (hostname: mon1)
    
    Ceph Object Storage Devices: 3
                    192.168.182.131 (hostname: osd1)
                    192.168.182.132 (hostname: osd2)
                    192.168.182.133 (hostname: osd3)

    Ceph Client:    192.168.182.134

====================================

# Define Hosts:

in All nodes:

```

# modify /etc/selinux/config
# set SELINUX=disabled

cat <<EOF >> /etc/hosts

192.168.182.128 ceph-admin
192.168.182.130 mon1
192.168.182.131 osd1
192.168.182.132 osd2
192.168.182.133 osd3

EOF

```

# Generate SSH in Admin

on ceph-admin:

```

cat <<EOF >> ~/.ssh/config

Host  ceph-admin
        Hostname    ceph-admin
        User        cephuser

Host  mon1
        Hostname    mon1
        User        cephuser

Host  osd1
        Hostname    osd1
        User        cephuser

Host  osd2
        Hostname    osd2
        User        cephuser

Host  osd3
        Hostname    osd3
        User        cephuser

Host  client
        Hostname    client
        User        cephuser

EOF

sudo chmod 644 ~/.ssh/config

sudo ssh-keyscan osd1 osd2 osd3 mon1 client >> ~/.ssh/known_hosts

ssh-keygen

sudo ssh-copy-id -i ~/.ssh/id_rsa.pub osd1
sudo ssh-copy-id -i ~/.ssh/id_rsa.pub osd2
sudo ssh-copy-id -i ~/.ssh/id_rsa.pub osd3
sudo ssh-copy-id -i ~/.ssh/id_rsa.pub mon1
sudo ssh-copy-id -i ~/.ssh/id_rsa.pub client




```
