---
title: "Sent Email from Linux Command-Line"
seoTitle: "email from linux cmd"
seoDescription: "send email from linux cmd"
datePublished: Thu Nov 23 2023 06:05:13 GMT+0000 (Coordinated Universal Time)
cuid: clpashjaz001308jxbkpo04rx
slug: sent-email-from-linux-command-line
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/LPZy4da9aRo/upload/da37f65ad3a1d1f85ccfe269bae0fbf7.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1700719461915/6ba74123-8701-4451-8bb0-e076d6a9bdef.png
tags: cloud, linux, devops, mail

---

Hey Folks✌️ welcome to another post, Here we discuss about using postfix send email by command line.

**Wondering to send alerts from command line to Email, here we go …**

## **Introduction:**

Postfix is a popular and widely-used open-source mail transfer agent (MTA) software. An MTA is responsible for routing and delivering email messages within a computer network, whether that network is the internet or an internal network within an organization

## **👇Requirements:**

1. Email credentials (Microsoft 365/Gmail)
    
2. Linux Machine
    

## **Step 1 — Install required packages:**

```bash
$ sudo yum install postfix cyrus-sasl-plain mailx -y
```

## **Step 2 — Change the** [**main.cf**](http://main.cf)**:**

Open the **/etc/postfix/**[**main.cf**](http://main.cf) file using your favorite editor(Vim/nano/) and add the below lines:

vim **/etc/postfix/**[**main.cf**](http://main.cf)

```bash
relayhost = [smtp.office365.com]:587
mynetworks = 127.0.0.0/8
inet_interfaces = loopback-only
smtp_use_tls = yes
smtp_always_send_ehlo = yes
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options = noanonymous
smtp_sasl_tls_security_options = noanonymous
smtp_tls_security_level = encrypt
smtp_generic_maps = hash:/etc/postfix/generic
smtp_sender_dependent_authentication = yes
sender_dependent_relayhost_maps = hash:/etc/postfix/sender_relay
```

## **Step 2 — Set Password for Email:**

Edit the password file **/etc/postfix/sasl\_passwd**

For Office 365 Email-ID use like below

**vim /etc/postfix/sasl\_passwd**

```bash
[smtp.office365.com]:587 email_1@mail.com:PASSWORD
```

## **Step 3 — Configure Multiple Emails \[Optional\]**

if you need multiple mails add like below

**vim /etc/postfix/sasl\_passwd**

```bash
[smtp.office365.com]:587 email_1@mail.com:PASSWORD
[smtp.office365.com]:587 email_2@mail.com:PASSWORD
[smtp.office365.com]:587 email_3@mail.com:PASSWORD
```

## **Step 4— Configure the Sender Relay \[ Required only for multiple Emails\]**

Edit **/etc/postfix/sender\_relay** add like below

**vim /etc/postfix/sender\_relay**

```bash
email_1@mail.com                         [smtp.office365.com]:587
email_2@mail.com                            email_2@mail.com
email_2@mail.com                            email_2@mail.com
```

## **Step 5— map the files to postfix**

Once all done, map the files into postfix. Run the below commands

```bash
$ postmap  main.cf
$ postmap  sasl_passwd
$ postmap  sender_relay
```

## **Step 6— Send Email**

For send Email ,run like below command.

```bash
$ echo  "This is the Test Email" | mailx -r "sender_email@mail.com"  -s "This test mail 98" recevier_email@mail.com
```

## **Step 6 — Check Logs \[Optional\]**

For debugging log file located on **/var/log/maillog.**

Open log file: **tail -f /var/log/maillog**

# **✅Mailx Usage:**

* \-a → add attachment
    
* \-b → add Bcc Email
    
* \-c → add CC Email
    
* \-r → From Email Address
    
* \-s → Subject of the Email
    

## **Taking the message from a file**

```bash
$ mailx -s "Test Mail by mailx" person@example.com < file.txt
```

## **Sending same Mail to Multiple Recipients:**

We can send the same email to multiple receivers (not by cc or bcc) as follows:

```bash
$ mailx - s "Test Mail by mailx" email_1@example.com, email_2@example.com < file.txt
```

## **Adding Attachments**

```bash
$ mailx - s "Test Mail by mailx" email_1@example.com -a File.txt
```

## **Adding CC & BCC**

```bash
$ mail - s "A mail sent using mailx" email_0@example.com -c email_cc@example.com -b email_bcc@example.com
```

Thanks for reading & Follow for More ✌️

Medium — [https://medium.com/@karthidkk123  
LinkedIn](https://medium.com/@karthidkk123) — [https://www.linkedin.com/in/karthick-dkk/  
Instagram](https://medium.com/@karthidkk123) — [https://www.instagram.com/karthick\_dkk\_dk/  
GitHub](https://medium.com/@karthidkk123) — [https://github.com/karthick-dkk](https://medium.com/@karthidkk123)

[By Me Coffee](https://www.buymeacoffee.com/karthidkk1Q) 👇

![](https://miro.medium.com/v2/resize:fit:510/0*5tQrzrL-SahOjV4K.jpeg align="center")