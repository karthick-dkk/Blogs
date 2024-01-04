---
title: "TLS Encryption for XRDP on Linux"
seoTitle: "TLS Encryption for XRDP on Linux"
seoDescription: "XRDP Encryption"
datePublished: Thu Jan 04 2024 13:28:56 GMT+0000 (Coordinated Universal Time)
cuid: clqz8txwa000c09jz1m0a7vvk
slug: tls-encryption-for-xrdp-on-linux
tags: ssl, ubuntu, linux, security, devops, tls, centos, xrp

---

![](https://miro.medium.com/v2/resize:fit:1250/1*PGsdteasOyyJCAMNkVxJyw.png align="left")

XRDP — Login Screen

# What is XRDP?

Remote Desktop Protocol (RDP) is a widely used protocol that allows users to connect to a remote server or desktop environment. XRDP is an open-source implementation of RDP for Linux-based systems like Ubuntu and CentOS. While XRDP provides convenient remote access, it is essential to prioritize security to protect sensitive data and prevent unauthorized access. One effective way to achieve this is by implementing SSL/TLS encryption to secure XRDP connections. In this blog, we’ll explore the process of setting up SSL/TLS encryption for XRDP on Ubuntu and CentOS, enhancing the overall security of your remote desktop environment.

In this blog we will look into how to Secure XRDP on Ubuntu/CentOS with SSL/TLS Encryption and how to install XRDP on Linux machines.

# **Requirements:**

1. Xrdp
    
2. Openssl
    
3. SSL Certificate ( .cert , .key )
    

# **Install required packages**

## **For Ubuntu /Debian based**

```bash
sudo apt update -y 
sudo apt install xrdp openssl -y 
```

## **For Centos/ Red hat/ Rocky**

```bash
sudo yum update -y
sudo yum install xrdp openssl -y
```

### **Copy your cert and key file to the /etc/xrdp/**

Change the permission to the cert and key file

```bash
sudo chmod 600 /etc/xrdp/example.key
sudo chmod 600 /etc/xrdp/example.crt
```

> Note: Generate Self Signed SSL Certificate Key [checkout here](https://medium.com/@karthidkk123/how-to-generate-self-signed-ssl-certificate-1fafc7f05685)

### **Edit the config file of XRDP**

(Use your own comfortable editor like, nano)

Here modify the setting like below in \[Globals\]

```bash
vim /etc/xrdp/xrdp.ini  
[Globals]

tls_ciphers=HIGH # set to high
ssl_protocols=TLSv1.2,TLSv1.3
key_file=/etc/xrdp/example.key # add your SSL key path
certificate=/etc/xrdp/example.crt # add your SSL crt path
crypt_level=high # set to High
security_layer=rdp,tls # You can use tls,rdp or tls
```

Save the config.

## **Enable and Restart the XRDP services**

```bash
sudo systemctl enable xrdp
sudo systemctl restart xrdp 
sudo systemctl status xrdp
```

### **Connect your system by using RDP clients:**

**(RDP default port 3389)**

*For Windows Connect via Remote Desktop connection*

*For Linux Connect via Remmina*

![](https://miro.medium.com/v2/resize:fit:693/1*jBxRF3B9YB5MsXkldIjc-A.png align="left")

**Ubuntu Cinnamon Desktop**

![](https://miro.medium.com/v2/resize:fit:1250/1*qTiix6wR8Y4Z-UAz4R9ksg.png align="left")

---

Thanks for the time!

Follow for more ! @[Karthick D](@karthick02)

👍Like and share ✅

Follow for More 👉  
Medium — [https://karthidkk123.medium.com/](https://karthidkk123.medium.com/)  
Linked In — [https://www.linkedin.com/in/karthick-dkk/](https://www.linkedin.com/in/karthick-dkk/)  
Instagram — [https://www.instagram.com/karthick\_dkk\_dk/](https://medium.com/@karthidkk123)