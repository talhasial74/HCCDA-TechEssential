# Deploying Enterprise on web

An enterprise intends to deploy their website on HUAWEI CLOUD and they have the
following requirements:

1. Database nodes and service nodes are deployed on separate ECSs.
2. ECSs are added or removed as incoming traffic changes over time.

## Prerequisites:

Log in to HUAWEI CLOUD.Go to the [Lab Desktop] and open the Google
Chrome browser to access the HUAWEI CLOUD login page. Select IAM User Login. In the
login dialog box, enter the assigned HUAWEI CLOUD lab account and password to log in to
HUAWEI CLOUD, as shown in the following figure.

![huawei Login](https://support.huaweicloud.com/intl/en-us/usermanual-iam/en-us_image_0000001211231610.png)

Note: For details about the account information, see the upper part of the lab manual. Do not use
your HUAWEI CLOUD account to log in.
### 1.Tasks
#### 1. 1 Creating a VPC

#### Step 1 Switch to the management console, and select the AP-Singapore region. In the left
navigation pane, choose Service List > Networking > Virtual Private Cloud.

![vpc](images/screen1.png)

#### Step 2 Click Create VPC.

![Create VPC](images/screen2.png)

#### Step 3 Configure the parameters as follows, and click Create Now.
- Region: AP-Singapore
- Name: vpc-mp (Change it as needed.)
- Retain the default settings for other parameters.

![Create VPC Details](images/screen3.png)

#### Step 4 View the created VPC in the VPC list.
![VPC lists](images/screen4.png)

#### 1.2 Creating and Configuring a Security Group
#### Step 1 On the Network Console, choose Access Control > Security Groups and create a security group.
![Security Group](images/screen4.png)

#### Step 2 Click the security group name.
#### Step 3 Click Inbound Rules and then Add Rule to add an inbound rule with the following parameter settings:
- **Protocol & Port: All**
- IP address in Source: 0.0.0.0/0
![Create Security Group](images/screen6.png)

