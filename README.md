![image](https://github.com/falahatme/ceph/assets/7458874/5d776b72-8f2d-4dd3-8a9a-18c9e40d05a9)

![image](https://github.com/falahatme/ceph/assets/7458874/788d19ad-a9ec-4757-be2d-17ce78b5dccc)

====================================
Nodes:

    Ceph Admin:     192.168.182.128
    Ceph Monitor1:  192.168.182.130
    
    Ceph Object Storage Devices: 3
                    192.168.182.131
                    192.168.182.132
                    192.168.182.133

    Ceph Client:    192.168.182.134

====================================

# Hosts:

in All nodes:

```

cat <<EOF > print.sh
192.168.182.128 ceph-admin
192.168.182.130 mon1
192.168.182.131 osd1
192.168.182.132 osd2
192.168.182.133 osd3
EOF

```

