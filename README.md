![image](https://github.com/falahatme/ceph/assets/7458874/5d776b72-8f2d-4dd3-8a9a-18c9e40d05a9)

![image](https://github.com/falahatme/ceph/assets/7458874/788d19ad-a9ec-4757-be2d-17ce78b5dccc)


Production nodes recommendation:

## Mon-Mgr:
```
  Processor:        Processor with four logical cores
  RAM:              24GB+ per daemon
  Disk Space:       60 GB per daemon SSD with RAID1
  Network:          Two network interfaces (1GbE+) bonded to multiple switches
```

## Ceph OSD Node:
```
  Processor:        1 core per 1000-3000 IOPS
  RAM:              4GB+ per daemon (more is better) 16GB per OSD host
  DB/WAL:           1x SSD partition per daemon (optional)
  Volume Storage    1x storage driver per daemon
  Nodes             Minimum of three nodes required
  Network           1x 1GbE+ NICs (10GbE+ recommended)
```

## Metadata Server Node:
```
  Processor         2.5 GHz CPU with at least 2 cores
  RAM               3GB for each Metadata Server daemon
  Disk Space        2MB per daemon
  Network           Two network interfaces (1GbE+) bonded to multiple switches
```

## Rados Gateway:
```
  Processor         8 cores
  RAM               64GB
  Disk Space        5GB SSD with RAID1
  Network           Two network interfaces(1GbE+) bonded to multiple switches
```

## ISCSI Gateway Node:
```
  Processor         8 cores
  RAM               16GB
  Disk Space        SSD with RAID1
  Network           Two network interfaces(1GbE+) bonded to multiple switches
```


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
