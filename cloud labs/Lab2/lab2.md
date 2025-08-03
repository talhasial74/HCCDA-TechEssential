# Lab 2: Deploying WordPress on a LAMP Stack

![WordPress Install](images/S2)

## Objective

Set up and run WordPress on a CentOS ECS instance using the LAMP stack (Linux, Apache, MySQL, PHP), with an RDS MySQL database as the backend.

---

## Step 1: Install LAMP Components on the ECS

SSH into your ECS instance and execute:

```bash
yum install -y httpd php php-fpm php-mysql mysql
```

### Start and enable Apache and PHP services:

```bash
systemctl start httpd
systemctl enable httpd
systemctl start php-fpm
systemctl enable php-fpm
```

---

## Step 2: Configure Apache

Open the Apache configuration file:

```bash
vim /etc/httpd/conf/httpd.conf
```

Add the following line at the bottom:

```bash
ServerName localhost:80
```

Restart Apache to apply changes:

```bash
systemctl restart httpd
```

---

## Step 3: Download and Install WordPress

Retrieve the WordPress package:

```bash
wget -c https://koolabsfiles.obs.ap-southeast-3.myhuaweicloud.com:443/20220731/wordpress-4.9.10.tar.gz
```

Extract it to the Apache web directory:

```bash
tar -zxvf wordpress-4.9.10.tar.gz -C /var/www/html
chmod -R 777 /var/www/html
```

---

## Step 4: Create a Database in RDS

From the RDS Console, open SQL Query and run:

```sql
CREATE DATABASE wordpress;
```

Ensure that your ECS security group allows access to the RDS instance over port **3306**.

---

## Step 5: Complete WordPress Setup via Browser

Open your browser and navigate to:

```
http://<ECS_Public_IP>/wordpress
```

Enter the following database information when prompted:

* **Database Name**: wordpress
* **Username**: root
* **Password**: Huawei!@#\$
* **Database Host**: `<RDS_Floating_IP>`

Click **Submit** and follow the remaining setup steps to complete the WordPress installation.

---

