# Lab 3: Setting Up Elastic Load Balancer (ELB) and Auto Scaling on Huawei Cloud

![ELB Setup](images/S3)

## Objective

Enhance the availability and scalability of your web application by deploying an Elastic Load Balancer along with Auto Scaling using a custom ECS image.

---

## Step 1: Provision a Load Balancer (ELB)

* Go to **Service List > Networking > Elastic Load Balance**
* Select **Buy Load Balancer**

  * **Type**: Shared
  * **Network Type**: Public
  * **Region**: AP-Singapore
  * **VPC**: Choose the same VPC as your ECS
  * **EIP**: Auto-assign (2 Mbps is sufficient)
  * **Name**: `elb-mp`
* Click **Submit**

---

## Step 2: Configure Listener and Backend

* After the ELB is created, open its **Details Page**
* Add a **Listener**:

  * **Protocol**: HTTP
  * **Port**: 80
  * **Backend Group**: Attach your existing ECS instance

---

## Step 3: Create a Private ECS Image

* Stop your current ECS
* Navigate to **Compute > Image Management > Create Image**

  * **Image Type**: System Disk Image
  * **Source**: Select the configured ECS
  * **Name**: `image-mp`
* Click **Submit**

---

## Step 4: Set Up Auto Scaling (AS)

* Go to **Compute > Auto Scaling**
* Click **Create AS Configuration**

  * **Name**: `as-mp`
  * **Image**: Select `image-mp`
  * **Login Credentials**: Use the same password (e.g., `Huawei@123!`)
  * **Network**: Choose the same VPC (do not bind EIP)
  * **Add to Load Balancer**: Enable and select `elb-mp`
* Save the configuration

---

## Step 5: Create Auto Scaling Group and Policies

* Create an **AS Group**:

  * **Min Instances**: 1
  * **Max Instances**: 3
  * **Desired Capacity**: 1
  * **Health Check**: ELB
* Add **Scaling Policies**:

  * **Scale Out**: Add one ECS when CPU usage exceeds 60% for 5 minutes
  * **Scale In**: Remove one ECS when CPU usage drops below 20% for 5 minutes

Once configured, the Auto Scaling group will dynamically adjust the number of ECS instances based on workload.

---
